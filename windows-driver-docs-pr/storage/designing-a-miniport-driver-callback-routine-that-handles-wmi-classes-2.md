---
title: WMI クラスを処理するミニポートドライバーコールバックルーチンを設計する
description: メソッドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計
ms.assetid: f5a0331a-1daa-4ef5-bf99-14b3a3393956
keywords:
- WMI SRBs WDK storage、コールバックルーチンの設計
- コールバックルーチン WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79102ecf3ebc9b77766eb177a41f6c87b6c65a15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845183"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-methods"></a>メソッドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


このセクションでは、WMI メソッドを含む WMI クラスの例を使用し、対応するミニポートドライバーのコールバックルーチンの外観について説明します。 WMI メソッドを実行するミニポートドライバーのコールバックルーチンの詳細については、「 [**HwScsiWmiExecuteMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)」を参照してください。

次の WMI クラスの例には、WMI メソッドが含まれています。

```cpp
class MSFC_HBAAdapterMethods
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Implemented,
     WmiMethodId(1)
    ]
    void GetDiscoveredPortAttributes(
            [in ] uint32 PortIndex,
            [in ] uint32 DiscoveredPortIndex,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
            [out, HBAType("HBA_PORTATTRIBUTES") ] 
                MSFC_HBAPortAttributesResults PortAttributes
            );
    [
     Implemented,
     WmiMethodId(2)
    ]
    void GetPortAttributesByWWN(
            [in, HBAType("HBA_WWN")] uint8 wwn[8],
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
          [out, HBAType("HBA_PORTATTRIBUTES") ] 
                MSFC_HBAPortAttributesResults PortAttributes
            );
};
class MSFC_HBAFCPInfo
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Implemented,
     WmiMethodId(1)
    ]
    void GetFcpTargetMapping(
            [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
            [in ] uint32 InEntryCount,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
            [out] uint32 TotalEntryCount,
            [out] uint32 OutEntryCount,
            [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry  
                 Entry[]
            );
};
```

**Msfc\_HBAAdapterMethods**クラスには、 **GetDiscoveredPortAttributes**と**getport属性 bywwn**の2つのメソッドが含まれています。 MSFC\_HBAFCPInfo クラスには、 **GetFcpTargetMapping**という1つのメソッドが含まれています。

SCSI ポート WMI ライブラリディスパッチルーチンがミニポートドライバーの execute メソッドコールバックルーチンを呼び出すと、WMI クラスを識別する*Guidindex*値、クラス内のメソッドを識別する*MethodId*値、および処理するクラスの複数の潜在的なインスタンスを識別する InstanceIndex 値。 コールバックルーチンは、クラス、メソッド、およびクラスのインスタンスの任意の組み合わせに対して適切なアクションを実行する必要があります。

次の例は、execute メソッドのコールバックルーチンが、前の例のメソッドを処理する方法を示しています。

```cpp
HwScsiWmiExecuteMethod (
    IN PVOID Context,
    IN PSCSIWMI_REQUEST_CONTEXT DispatchContext,
    IN ULONG GuidIndex,
    IN ULONG InstanceIndex,
    IN ULONG MethodId,
    IN ULONG InBufferSize,
    IN ULONG OutBufferSize,
    IN OUT PUCHAR Buffer
    )

  switch(GuidIndex) { 
    case MSFC_HBAAdapterMethodsGuidIndex:
    {
      switch(MethodId) {
      case GetDiscoveredPortAttributes:
        // handle method here 
        Switch(InstanceIndex) {
        case 1:
          // handle instance 1
          PGetDiscoveredPortAttributes_IN In;
          PGetDiscoveredPortAttributes_OUT Out;
          // note: input and output parameters use the same buffer
          In = (PGetDiscoveredPortAttributes_IN)Buffer;
          Out = (PGetDiscoveredPortAttributes_OUT)Buffer;
          // put code for method here
          break;
        case 2:
       // handle instance 2
        default:
          break;
        }
      case GetPortAttributesByWWN:
        // handle method here 
      default:
        break;
    }
    case MSFC_HBAFCPInfoGuidIndex:
    {
      switch(MethodId) {
      case GetFcpTargetMapping:
        // handle method here 
      default:
        break;
      }
    }
```

WMI ツールスイート (**mofcomp.exe**と**wmimofck**) を使用すると、バイナリタイプライブラリと、各 WMI クラス GUID インデックスと各メソッド識別子のシンボル定数を定義するヘッダーファイルを自動的に生成することで、このルーチンを作成するタスクを簡略化できます。 これらのツールの使用方法の詳細については、「[ドライバーの MOF ファイルのコンパイル](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)と[wmimofck の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)」を参照してください。

**Wmimofck**ツールは、 **mofcomp.exe**によって生成された、bmf バイナリファイルから .h ファイルを生成します。 これは、"GuidIndex" というサフィックスを WMI クラスの名前に連結することによって、クラスインデックスのシンボル定数の名前を形成します。 たとえば、 **msfc\_FibrePortHBAMethods**クラスを使用すると、このツールは、そのクラスの GUID インデックスを表す**Msfc\_FibrePortHBAMethodsGuidIndex**という名前のシンボル定数を作成します。 同様の方法で、ツールはメソッド名を使用して、メソッドを表すシンボリック定数を作成しますが、サフィックスを追加する必要はありません。 メソッドのシンボル定数の名前は、メソッドの名前にすぎません。 この例では、switch ステートメントによって、メソッド識別子の値がテストされます。 Switch ステートメントの各ケースは、メソッド名に対応しています。

WMI クラスのメソッドを定義するために使用される MOF 構文はルーチンに似ています。ただし、WMI メソッドはルーチンではありません。 **Mofcomp.exe**および**WMIMOFCK**ツールが MOF ファイル内のメソッド定義を処理すると、メソッドに対して2つの異なる C 言語構造の宣言が生成されます。 1つの構造は、MOF ファイルで "\[\]" プレフィックスによって入力パラメーターとして識別されるパラメーターと、"\[out\]" プレフィックスによって出力パラメーターとして識別されるパラメーターの別の構造体です。

**Wmimofck**ツールは、メソッドの名前に "\_IN" のサフィックスを連結することによって、メソッドの入力パラメーターを含む構造体の名前を形成します。 たとえば、メソッドの名前が**GetDiscoveredPortAttributes**の場合、 **WMIMOFCK**は、で GetDiscoveredPortAttributes\_という名前の構造体の宣言を自動的に生成します。 同様に、 **wmimofck**は、メソッドの出力パラメーターを保持する GETDISCOVEREDPORTATTRIBUTES\_OUT という名前の構造体の宣言を生成します。

次のコードスニペットは、execute メソッドのコールバックルーチンが、 **Msfc\_HBAPortMethods**というクラスで**GetDiscoveredPortAttributes**という名前のメソッドの入力バッファーと出力バッファーのサイズを検証する方法を示しています。

```cpp
case MSFC_HBAPortMethodsGuidIndex:
  switch(MethodId) {
    case GetDiscoveredPortAttributes:
  {
      BOOLEAN bInputBigEnough = (InBufferSize >= 
              sizeof(GetDiscoveredPortAttributes_IN))
      BOOLEAN bOutputBigEnough = (OutBufferSize >= 
              sizeof(GetDiscoveredPortAttributes_OUT))
      if (bInputBigEnough && bOutputBigEngough) {
        PGetDiscoveredPortAttributes_IN In;
        PGetDiscoveredPortAttributes_OUT Out;

        In = (PGetDiscoveredPortAttributes_IN)Buffer;
         Out = (PGetDiscoveredPortAttributes_OUT)Buffer;
        // 
        // process method here
      //
        status = SRB_STATUS_SUCCESS;
      } else {
        status = SRB_STATUS_DATA_OVERRUN;
      }
    }
```

を返す前に、コールバックルーチンは[**ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)を呼び出す必要があります。 この SCSI ポート WMI ライブラリルーチンは、要求の状態や返されるデータのサイズなどの情報で要求コンテキストを更新します。 要求コンテキストに格納されている情報の詳細については、「 [**SCSIWMI\_request\_context**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)」を参照してください。

 

 





---
title: WMI クラスを処理するためにデザイン ミニポート ドライバー コールバック ルーチン
description: WMI クラスとメソッドを処理するミニポート ドライバー コールバック ルーチンの設計
ms.assetid: f5a0331a-1daa-4ef5-bf99-14b3a3393956
keywords:
- WMI される Srb WDK の記憶域、コールバック ルーチンの設計
- コールバック ルーチン WDK WMI される Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8114a2b9aa0a79d9bdd529605055a07a95494bb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529184"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-methods"></a>WMI クラスとメソッドを処理するミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


このセクションでは、WMI メソッドが含まれている例の WMI クラスを使用し、対応するミニポート ドライバー コールバック ルーチンがどのようにについて説明します。 WMI メソッドを実行するミニポート ドライバー コールバック ルーチンの詳細については、[ **HwScsiWmiExecuteMethod**](https://msdn.microsoft.com/library/windows/hardware/ff557332)を参照してください。

次の例の WMI クラスには、WMI メソッドが含まれます。

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

**MSFC\_HBAAdapterMethods**クラスには、2 つのメソッドが含まれています。 **GetDiscoveredPortAttributes**と**GetPortAttributesByWWN**します。 MSFC\_HBAFCPInfo クラスには、1 つのメソッドが含まれています。 **GetFcpTargetMapping**します。

SCSI ポート WMI ライブラリのディスパッチ ルーチンは、ミニポート ドライバーを呼び出すときにメソッドのコールバック ルーチンの実行、渡します、 *GuidIndex* 、WMI クラスを識別する値を*メソッド Id*値クラス内のメソッドを識別して、 *InstanceIndex*の可能性を処理するためのクラスの複数のインスタンスを識別する値。 コールバック ルーチンでは、クラス、メソッド、およびクラスのインスタンスの組み合わせの適切な処置を実行する必要があります。

次の例では、execute メソッドのコールバック ルーチンが、前の例のメソッドを処理する方法を示します。

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

WMI ツールのスイート (**mofcomp**と**wmimofck**) のバイナリのタイプ ライブラリと各 WMI のシンボリック定数を定義するヘッダー ファイルを自動的に生成することによってこのルーチンを記述するタスクを簡略化クラス GUID のインデックスと各メソッドの識別子。 これらのツールを使用する方法の詳細については、[ドライバーの MOF ファイルをコンパイルする](https://msdn.microsoft.com/library/windows/hardware/ff542012)と[wmimofck.exe を使用して](https://msdn.microsoft.com/library/windows/hardware/ff565588)を参照してください。

**Wmimofck**ツールによって生成された .bmf バイナリ ファイルから .h ファイルを生成する**mofcomp**します。 WMI クラスの名前に"GuidIndex"のサフィックスを連結して、クラスのインデックスのシンボリック定数の名前を形成します。 たとえば、 **MSFC\_FibrePortHBAMethods**クラス、ツールと呼ばれるシンボリック定数が作成されます**MSFC\_FibrePortHBAMethodsGuidIndex**を表す、そのクラスの GUID のインデックス。 同様の方法で、ツールはメソッド名のサフィックスを追加することがなくフォーム メソッドを表す記号定数を使用します。 メソッドのシンボリック定数の名前は、メソッドの名前だけです。 例では、switch ステートメントは、メソッドの識別子の値をテストします。 Switch ステートメント内の各ケースでは、メソッド名に対応します。

WMI クラスのメソッドを定義するために使用する MOF 構文に似ています、ルーチンただし、WMI メソッドは、ルーチンではありません。 ときに、 **mofcomp**と**wmimofck**ツール、MOF ファイル内のメソッド定義を処理する、2 つ個別 C 言語構造体の宣言、メソッドを生成します。 1 つの構造は、MOF で指定されているパラメーターのファイルの入力としてパラメーターを"\[で\]"プレフィックス、および別の構造によって出力パラメーターとして指定されているパラメーターの"\[アウト\]"プレフィックスです。

**Wmimofck**ツールのフォームのサフィックスを連結してメソッドを含む構造体の名前の入力パラメーター"\_IN"メソッドの名前にします。 たとえば、メソッドの名前が場合**GetDiscoveredPortAttributes**、 **wmimofck** GetDiscoveredPortAttributes という名前の構造体の宣言が自動的に生成\_in です。 同様に、 **wmimofck** GetDiscoveredPortAttributes という名前の構造体の宣言を生成\_メソッドの出力パラメーターを保持する出力。

次のコード スニペットは、execute メソッドのコールバック ルーチンが呼び出されるメソッドの入力と出力バッファーのサイズを検証する方法を示しています**GetDiscoveredPortAttributes**というクラスに**MSFC\_ 。HBAPortMethods**:

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

、戻る前に、コールバック ルーチンを呼び出す必要があります[ **ScsiPortWmiPostProcess**](https://msdn.microsoft.com/library/windows/hardware/ff564796)します。 この SCSI ポート WMI ライブラリ ルーチンでは、要求の状態と戻り値のデータのサイズなどの情報を要求コンテキストを更新します。 要求コンテキストに格納されている情報の詳細については、[ **SCSIWMI\_要求\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff564946)を参照してください。

 

 





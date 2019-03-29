---
title: SCSI ポート WMI ライブラリの使用
description: SCSI ポート WMI ライブラリの使用
ms.assetid: cb55bbb3-39bb-491f-a6d2-50dceace4a86
keywords:
- WMI される Srb WDK ストレージ、SCSI ポート WMI ライブラリ
- SCSI ポート WMI ライブラリ WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3e97a86daa24747a9ad08c4b641d8bf16157ca0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574475"
---
# <a name="using-the-scsi-port-wmi-library"></a>SCSI ポート WMI ライブラリの使用


## <span id="ddk_using_the_scsi_port_wmi_library_kg"></span><span id="DDK_USING_THE_SCSI_PORT_WMI_LIBRARY_KG"></span>


WMI プロバイダーとして機能する記憶域ミニポート ドライバーでは、SCSI ポート WMI ライブラリを使用して、WMI コマンドが含まれている SCSI 要求ブロック (される Srb) の処理のタスクを簡略化します。 ミニポート ドライバーの I/O ルーチンを開始する[ **HwScsiStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff557323)への呼び出しによって、処理の SCSI ポート WMI ライブラリに WMI SRB の関連情報を渡します、 [ **ScsiPortWmiDispatchFunction** ](https://msdn.microsoft.com/library/windows/hardware/ff564766)ライブラリのディスパッチ ルーチン。 ミニポート ドライバーでは、次のデータをディスパッチ ルーチンを渡します。

-   *WmiLibInfo*パラメーター: [ **SCSI\_WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565395)ミニポート ドライバーのコールバック ルーチンへのポインターを含む構造体。

-   *WMISubFunction*パラメーター: の値、 **WMISubFunction** SRB のメンバー。

-   *DeviceContext*パラメーター: デバイスの拡張機能へのポインター。

-   *RequestContext*パラメーター: 型の要求コンテキストの構造体[ **SCSIWMI\_要求\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff564946)を SCSI ポート WMI返される状態とデータのサイズなど、情報を記録するライブラリを使用します。

-   *データパス*パラメーター: の値、**データパス**SRB のメンバー。

-   *BufferSize*パラメーター: の値、 **DataTransferLength** SRB のメンバー。

-   *バッファー*パラメーター: の値、 **DataBuffer** SRB のメンバー。

これを入力する必要があります、ミニポート ドライバーが初期化されると、 [ **SCSI\_WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565395)必要ミニポート ドライバーのコールバック ルーチンへのポインターを使用した構造しドライバーの拡張機能など、ミニポート ドライバー固有のストレージ領域で、構造を格納します。 説明に従って、マイナー IRP 番号に対応する各ミニポート ドライバー コールバック ルーチン[方法、ポート ドライバー プロセスの WMI 要求](how-the-port-driver-processes-wmi-requests.md)します。 ミニポート ドライバー コールバック ルーチンへの設計方法については、次を参照してください[WMI ミニポートのドライバー コールバック ルーチンを設計。](designing-wmi-miniport-driver-callback-routines.md)

**GuidList** SCSI のメンバー\_WMILIB\_CONTEXT 構造は、型の要素の配列を指す必要があります[ **SCSIWMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff564941)ですについては、MOF ファイルで定義されている、サポートされている WMI クラスを一意に識別する Guid を含めることができます。 次のコード スニペットは、このような要素の配列の定義を示しています。

```cpp
SCSIWMIGUIDREGINFO GuidList[] = 
{
  {
    &HBAStatisticsGUID,  // Guid
    3,  // number of instances of this class
    0  // flags
  },
  {
    &HBAAttributesGUID, // guid
    1,  // number of instances of this class
    0  // flags
  }
};
```

配列には、2 つの WMI クラスの Guid に関する情報が含まれています。 **HBAStatistics**と**HBAAttributes**します。 Guid のシンボリック定数は、WMI ツール スイートでは、2 つのクラスを定義する MOF ファイルのコンパイルによって生成されたヘッダー ファイルから取得されました (、 **mofcomp**と**wmimofck**ツール)。 これらのツールを使用する方法の詳細については、次を参照してください。[ドライバーの MOF ファイルをコンパイルする](https://msdn.microsoft.com/library/windows/hardware/ff542012)と[wmimofck.exe を使用して](https://msdn.microsoft.com/library/windows/hardware/ff565588)します。

WMI ツールのスイートでは、WMI クラスの名前に"GUID"のサフィックスを連結して、GUID のシンボリック定数の名前を生成します。 クラスのインスタンス、 **HBAStatistics、** と呼ばれるシンボリック定数は、ツールで作成**HBAStatisticsGUID**そのクラスの GUID を表します。

 

 





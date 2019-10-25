---
title: SCSI ポート WMI ライブラリの使用
description: SCSI ポート WMI ライブラリの使用
ms.assetid: cb55bbb3-39bb-491f-a6d2-50dceace4a86
keywords:
- WMI SRBs WDK storage、SCSI ポート WMI ライブラリ
- SCSI ポート WMI ライブラリ WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 530e9ae66d20a5f212183be07d89d2543e788133
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845588"
---
# <a name="using-the-scsi-port-wmi-library"></a>SCSI ポート WMI ライブラリの使用


## <span id="ddk_using_the_scsi_port_wmi_library_kg"></span><span id="DDK_USING_THE_SCSI_PORT_WMI_LIBRARY_KG"></span>


WMI プロバイダーとして機能する記憶域ミニポートドライバーは、SCSI ポート WMI ライブラリを使用して、WMI コマンドを含む SCSI 要求ブロック (SRBs) を処理するタスクを簡略化できます。 ミニポートドライバーの開始 i/o ルーチン[**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))は、wmi SRB の関連情報を、 [**ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)ライブラリのディスパッチルーチンの呼び出しによって処理するために、SCSI ポート wmi ライブラリに渡します。 ミニポートドライバーは、次のデータをディスパッチルーチンに渡します。

-   *WmiLibInfo*パラメーターでは、 [**SCSI\_wmは**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context)、ミニポートドライバーのコールバックルーチンへのポインターを含むコンテキスト構造\_します。

-   *WMISubFunction*パラメーターの場合: SRB の**WMISubFunction**メンバーの値。

-   *Devicecontext*パラメーターに、デバイス拡張機能へのポインターを指定します。

-   *RequestContext*パラメーター: SCSIWMI 型の要求コンテキスト構造は、SCSI ポート WMI ライブラリが情報 (返されたデータの状態やサイズなど) を記録するために使用する[**コンテキスト\_要求\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)です。

-   *データパス*パラメーターの場合: SRB の**データパス**メンバーの値。

-   *BufferSize*パラメーターで、SRB の**Datatransの長さ**のメンバーの値。

-   *Buffer*パラメーターで、SRB の**DataBuffer**メンバーの値。

ミニポートドライバーが初期化されるときに、必要なミニポートドライバーコールバックルーチンへのポインターを使用して[**SCSI\_WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-_scsiwmilib_context)構造に入力し、その構造をミニポートドライバー固有のストレージ領域に格納する必要があります (例:)。ドライバーの拡張機能。 各ミニポートドライバーコールバックルーチンは、「[ポートドライバーが WMI 要求を処理する方法](how-the-port-driver-processes-wmi-requests.md)」で説明されているように、小さな IRP 番号に対応します。 ミニポートドライバーのコールバックルーチンをデザインする方法については、「 [WMI ミニポートドライバーのコールバックルーチンの設計](designing-wmi-miniport-driver-callback-routines.md)」を参照してください。

SCSI\_WM/b の**Guidlist**メンバー\_コンテキスト構造体は、 [**SCSIWMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmiguidreginfo)型の要素の配列を指す必要があります。これには、「」で定義されているサポート対象の WMI クラスを一意に識別する guid に関する情報が含まれていなければなりません。MOF ファイル。 次のコードスニペットは、このような要素の配列の定義を示しています。

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

配列には、2つの WMI クラス ( **Hbastatistics**および**hbastatistics**) の guid に関する情報が含まれています。 Guid のシンボル定数は、WMI ツールスイート ( **mofcomp.exe**および**wmimofck**ツール) を使用して2つのクラスを定義する MOF ファイルをコンパイルして生成されたヘッダーファイルから取得されました。 これらのツールの使用方法の詳細については、「[ドライバーの MOF ファイルのコンパイル](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)と[wmimofck の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-wmimofck-exe)」を参照してください。

WMI ツールスイートは、"GUID" のサフィックスを WMI クラスの名前に連結することによって、GUID のシンボル定数の名前を生成します。 たとえば、クラス**Hbastatistics**の場合、ツールは**HBAStatisticsGUID**という名前のシンボル定数を作成します。これは、そのクラスの GUID を表します。

 

 





---
title: 記憶域ミニポート ドライバーでの WMI SRB の処理
description: 記憶域ミニポート ドライバーでの WMI SRB の処理
ms.assetid: 92b78611-7e6f-4d77-9133-635df96584f0
keywords:
- ストレージ ミニポート ドライバー WDK、WMI される Srb
- WMI される Srb のミニポート ドライバー WDK ストレージ
- WMI される Srb についての WMI される Srb WDK ストレージ
- WMI される Srb WDK ストレージ
- SRB の WMI のサポートを WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a9688bacbd63525814c0fe60a68289f45467f26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372336"
---
# <a name="handling-wmi-srbs-in-storage-miniport-drivers"></a>記憶域ミニポート ドライバーでの WMI SRB の処理


## <span id="ddk_handling_wmi_srbs_in_storage_miniport_drivers_kg"></span><span id="DDK_HANDLING_WMI_SRBS_IN_STORAGE_MINIPORT_DRIVERS_KG"></span>


WMI は、ホスト バス アダプター (HBA) に関する情報を報告するをインターフェイスまたは HBA の記憶域ミニポート ドライバーとの対話、通常は WMI プロバイダとして機能するミニポート ドライバーを必要とする WMI クライアントを使用できます。 ストレージ ミニポート ドライバーは、WMI プロバイダーとして登録して後の SCSI 要求ブロック (SRB) の Windows Management Instrumentation (WMI) の SCSI 要求のブロックと呼ばれる特殊なを処理する準備する必要があります ([**SCSI\_WMI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_wmi_request_block))。

WMI される Srb を処理するために、記憶域ミニポート ドライバーを準備するには、次の手順を完了します。

1.  デザインし、システム提供の MOF ファイルで定義されていない WMI スキーマの部分を説明する管理オブジェクト フォーマット (MOF) ファイルをコンパイルします。

    MOF 構文については、次を参照してください。 [WMI データとイベント ブロックの MOF 構文](https://docs.microsoft.com/windows-hardware/drivers/kernel/mof-syntax-for-wmi-data-and-event-blocks)します。

2.  ミニポート ドライバー コールバック ルーチンを実装します。

    SCSI ポート WMI ライブラリには、WMI される Srb のミニポート ドライバーの処理が簡略化します。 SCSI ポート WMI ライブラリを使用して、実装、 *HwScsiWmiXxx*で説明されているコールバック ルーチン[SCSI ミニポート ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

3.  ミニポート ドライバーに必要なコードを追加[ **SCSI ミニポート ドライバーの DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチン。

4.  ミニポート ドライバーに必要なコードを追加[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチン。

5.  ミニポート ドライバーに必要なコードを追加[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチン。

前の手順を実装する方法の詳細については、このセクションで、次のトピックを参照してください。

[ポートのドライバーが WMI 要求を処理する方法](how-the-port-driver-processes-wmi-requests.md)

[SCSI ポート WMI ライブラリの使用](using-the-scsi-port-wmi-library.md)

[設計の WMI のミニポート ドライバー コールバック ルーチン](designing-wmi-miniport-driver-callback-routines.md)

[WMI される Srb をサポートする記憶域ミニポート ドライバー、ルーチンの変更](modifying-storage-miniport-driver-routines-to-support-wmi-srbs.md)

 

 





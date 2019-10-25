---
title: 記憶域ミニポート ドライバーでの WMI SRB の処理
description: 記憶域ミニポート ドライバーでの WMI SRB の処理
ms.assetid: 92b78611-7e6f-4d77-9133-635df96584f0
keywords:
- 記憶域ミニポートドライバー WDK、WMI SRBs
- ミニポートドライバー WDK 記憶域、WMI SRBs
- Wmi SRBs WDK storage、WMI SRBs について
- WMI SRBs WDK storage
- SRB WMI での WDK ストレージのサポート
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5ec04a24d0e48a0acc2f7323cd7de543aafe625d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838005"
---
# <a name="handling-wmi-srbs-in-storage-miniport-drivers"></a>記憶域ミニポート ドライバーでの WMI SRB の処理

ホストバスアダプター (HBA) に関する情報を報告したり、WMI クライアントが HBA の記憶域ミニポートドライバーと対話できるようにする WMI インターフェイスは、通常、ミニポートドライバーを WMI プロバイダーとして機能させる必要があります。 記憶域ミニポートドライバーが WMI プロバイダーとして登録された後、Windows Management Instrumentation (WMI) SCSI 要求ブロック ([SCSI_WMI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_wmi_request_block)) と呼ばれる特殊な種類の scsi 要求ブロック (SRB) を処理できるように準備する必要があります。

WMI SRBs を処理するように記憶域ミニポートドライバーを準備するには、次の手順を実行します。

1. システム提供の MOF ファイルで定義されていない WMI スキーマの部分を記述する管理オブジェクトフォーマット (MOF) ファイルを設計およびコンパイルします。

    MOF 構文の詳細については、「 [WMI データおよびイベントブロックの Mof 構文](https://docs.microsoft.com/windows-hardware/drivers/kernel/mof-syntax-for-wmi-data-and-event-blocks)」を参照してください。

2. ミニポートドライバーコールバックルーチンを実装します。

    SCSI ポート WMI ライブラリを使用すると、ミニポートドライバーの WMI SRBs の処理が簡単になります。 SCSI ポート WMI ライブラリを使用するには、「 [Scsi ミニポートドライバールーチン](scsi-miniport-driver-routines.md)」に記載されている*HwScsiWmiXxx*コールバックルーチンを実装します。

3. [**SCSI ミニポートドライバールーチンの**](driverentry-of-scsi-miniport-driver.md)ミニポートドライバーの driverentry に必要なコードを追加します。

4. ミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンに必要なコードを追加します。

5. ミニポートドライバーの[*HwScsiStartIo*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンに必要なコードを追加します。

前の手順の実装の詳細については、次のトピックを参照してください。

- [ポートドライバーが WMI 要求を処理する方法](how-the-port-driver-processes-wmi-requests.md)

- [SCSI ポート WMI ライブラリの使用](using-the-scsi-port-wmi-library.md)

- [WMI ミニポートドライバーコールバックルーチンの設計](designing-wmi-miniport-driver-callback-routines.md)

- [WMI SRBs をサポートするためのストレージミニポートドライバールーチンの変更](modifying-storage-miniport-driver-routines-to-support-wmi-srbs.md)

---
title: HwScsiStartIo からの戻り値
description: HwScsiStartIo からの戻り値
ms.assetid: e3d5e21a-4dc2-41bf-97a2-9ac2aa5a1af2
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- 戻り値 WDK SCSI
- 状態値 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3178ad26c7ccac2e0ee808f1a1d898d58ca92f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842689"
---
# <a name="return-from-hwscsistartio"></a>HwScsiStartIo からの戻り値


## <span id="ddk_return_from_hwscsistartio_kg"></span><span id="DDK_RETURN_FROM_HWSCSISTARTIO_KG"></span>


すべての[**HwScsiStartIo**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンは、入力要求が処理されたことを示す**TRUE**を返す必要があります。

*HwScsiStartIo*ルーチンが呼び出されたときに要求された操作を実行できない場合、 *HwScsiStartIo*は次の操作を行う必要があります。

1.  入力 SRB の**Srbstatus**を SRB\_STATUS\_BUSY に設定します。

2.  *NotificationType * * * RequestComplete** と入力 SRB を使用して[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出します。

3.  *NotificationType * * * nextrequest** を使用して**ScsiPortNotification**を呼び出します。ドライバーは、完了した SRB にあるものとは異なるターゲット論理ユニットへの要求を受け入れることができます。

4.  **TRUE**を返します。

ポートドライバーは、 **Srbstatus**値 SRB\_STATUS\_で返されたすべての要求をミニポートドライバーの*HwScsiStartIo*ルーチンに後で再送信します。

最終的には、各ミニポートドライバーは、 *HwScsiStartIo*ルーチンへの SRB 入力ごとに**ScsiPortNotification**を2回呼び出す必要があります。まず、要求を完了するために (*NotificationType ***requestcomplete**)、2番目はポートドライバーに指示します。次の SRB (* NotificationType ***Nextrequest**または**Nextlurequest**) を使用して HwScsiStartIo ルーチンをもう一度呼び出すこと。

ポーリングによって HBA を排他的に管理するミニポートドライバーの*HwScsiStartIo*ルーチンは、 *NotificationType * * * requesttimercall** を使用して**ScsiPortNotification**を呼び出し、 *HwScsiTimer*ルーチンへのポインターを呼び出します。 *HwScsiTimer*ルーチンの詳細については、「 [SCSI ミニポートドライバーの HwScsiTimer ルーチン](scsi-miniport-driver-s-hwscsitimer-routine.md)」を参照してください。

 

 





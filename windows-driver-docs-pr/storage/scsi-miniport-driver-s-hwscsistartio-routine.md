---
title: SCSI ミニポート ドライバーの HwScsiStartIo ルーチン
description: SCSI ミニポート ドライバーの HwScsiStartIo ルーチン
ms.assetid: cb818e5f-b91f-44cb-972b-22f75459edeb
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- 受信の I/O 要求の WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0244f798a433b05f5cb46fb9b523addfb991c931
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386495"
---
# <a name="scsi-miniport-drivers-hwscsistartio-routine"></a>SCSI ミニポート ドライバーの HwScsiStartIo ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsistartio_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSISTARTIO_ROUTINE_KG"></span>


名前のとおり、 [ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))ルーチンは、HBA ドリブン バス上の周辺機器のデバイスへの着信要求のエントリ ポイント。 *HwScsiStartIo*は SCSI 要求ブロック (SRB) して、ミニポート ドライバーのデバイスの拡張機能を伴うの HBA 状態に対して呼び出されます。 構文については、この日常的な参照の**HwScsiStartIo**します。

場合、ミニポート ドライバーの**DriverEntry**ルーチンでは、そのメモリも要求された論理ユニットの拡張機能を割り当てられません (を参照してください[呼び出す ScsiPortInitialize](calling-scsiportinitialize.md))、 *HwScsiStartIo*ルーチンの呼び出し**ScsiPortGetLogicalUnit**入力デバイスの拡張機能のポインターを使用し、 **PathId**、 **TargetId**、および**Lun** SRB の入力からの値。

場合、 **DriverEntry**ルーチンにはそのメモリが要求される SRB の拡張機能に割り当てられる、 **SrbExtension**各 SRB のメンバーには、ミニポート ドライバーの要求ごとの記憶域へのポインターが含まれています。 注ミニポート ドライバーがそのメモリを要求する必要がありますに割り当てられる**SrbExtension**s 要求ごとの状態情報を保持する場合。 このため、SRB は使用できません。

 

 





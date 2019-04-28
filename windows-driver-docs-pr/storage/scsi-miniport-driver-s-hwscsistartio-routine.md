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
ms.openlocfilehash: 5c6ef75d1a193c1a9df1df8aa483a313f21b5bcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378950"
---
# <a name="scsi-miniport-drivers-hwscsistartio-routine"></a>SCSI ミニポート ドライバーの HwScsiStartIo ルーチン


## <span id="ddk_scsi_miniport_drivers_hwscsistartio_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSISTARTIO_ROUTINE_KG"></span>


名前のとおり、 [ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)ルーチンは、HBA ドリブン バス上の周辺機器のデバイスへの着信要求のエントリ ポイント。 *HwScsiStartIo*は SCSI 要求ブロック (SRB) して、ミニポート ドライバーのデバイスの拡張機能を伴うの HBA 状態に対して呼び出されます。 構文については、この日常的な参照の**HwScsiStartIo**します。

場合、ミニポート ドライバーの**DriverEntry**ルーチンでは、そのメモリも要求された論理ユニットの拡張機能を割り当てられません (を参照してください[呼び出す ScsiPortInitialize](calling-scsiportinitialize.md))、 *HwScsiStartIo*ルーチンの呼び出し**ScsiPortGetLogicalUnit**入力デバイスの拡張機能のポインターを使用し、 **PathId**、 **TargetId**、および**Lun** SRB の入力からの値。

場合、 **DriverEntry**ルーチンにはそのメモリが要求される SRB の拡張機能に割り当てられる、 **SrbExtension**各 SRB のメンバーには、ミニポート ドライバーの要求ごとの記憶域へのポインターが含まれています。 注ミニポート ドライバーがそのメモリを要求する必要がありますに割り当てられる**SrbExtension**s 要求ごとの状態情報を保持する場合。 このため、SRB は使用できません。

 

 





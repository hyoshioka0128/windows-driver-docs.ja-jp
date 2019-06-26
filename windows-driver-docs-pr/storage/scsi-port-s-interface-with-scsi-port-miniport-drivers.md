---
title: SCSI ポートと SCSI ポート ミニポート ドライバーとのインターフェイス
description: SCSI ポートと SCSI ポート ミニポート ドライバーとのインターフェイス
ms.assetid: e6bd9861-5b89-40cc-92ab-0d23f18ba805
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7116916442b45bee369da9b1a155647dc596951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386487"
---
# <a name="scsi-ports-interface-with-scsi-port-miniport-drivers"></a>SCSI ポートと SCSI ポート ミニポート ドライバーとのインターフェイス


## <span id="ddk_scsi_port_s_interface_with_scsi_port_miniport_drivers_kg"></span><span id="DDK_SCSI_PORT_S_INTERFACE_WITH_SCSI_PORT_MINIPORT_DRIVERS_KG"></span>


SCSI ポート ドライバーと SCSI ポート ミニポート ドライバー間の通信が行わによって SCSI 要求のブロック (される Srb) およびミニポート ドライバー コールバック ルーチン。 SCSI ポート ミニポート ドライバー コールバック ルーチンの詳細については、次を参照してください。 [SCSI ミニポート ドライバー](scsi-miniport-drivers.md)します。

概要と SRB の個々 の関数、SRB フラグ、および SRB 状態の値の定義については、次を参照してください。 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)します。

ミニポート ドライバーが SRB 関数に対応する方法に関する話題は、次を参照してください。 [SCSI ミニポート ドライバー HwScsiStartIo ルーチン](scsi-miniport-driver-s-hwscsistartio-routine.md)します。

SCSI ポートは、同期的に、アダプターがタグ付けされたキューがサポートする場合を除くされる Srb を SCSI ポート ミニポート ドライバーに転送します。 タグが付けられたキューをサポートするホスト バス アダプターでは、内部要求キューに配置でき、それらを SCSI ポートを各要求に割り当てることのタグで示される順序で処理することができます。 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block) (SRB) 構造体には、SCSI ポート ドライバーを使用してホスト アダプターの内部キューでされる Srb を順序付けする方法を指定する 2 つのメンバーが含まれています。:**QueuedTag**と**QueueAction**します。 SCSI ポート割り当ての数、または *「タグ」* 値に、 **QueuedTag**アダプターが、パケットを処理する順序を示す各 SRB のメンバー。 タグの値では、SCSI ポートされる Srb が正常に完了してされる Srb がタイムアウトしたかを追跡することもできます。

**QueueAction**値は次のいずれかのメンバーが割り当てられます。

SRB\_単純\_タグ\_要求

SRB\_ヘッド\_の\_キュー\_タグ\_要求

SRB\_ORDERED\_キュー\_タグ\_要求

これらの値の詳細については、デバイスの 2 つの仕様を参照してください。

 

 





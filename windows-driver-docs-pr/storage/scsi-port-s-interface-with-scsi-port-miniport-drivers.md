---
title: SCSI ポートと SCSI ポート ミニポート ドライバーとのインターフェイス
description: SCSI ポートと SCSI ポート ミニポート ドライバーとのインターフェイス
ms.assetid: e6bd9861-5b89-40cc-92ab-0d23f18ba805
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3970c3b476fee912d124b1dc539c2388226fe1ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842655"
---
# <a name="scsi-ports-interface-with-scsi-port-miniport-drivers"></a>SCSI ポートと SCSI ポート ミニポート ドライバーとのインターフェイス


## <span id="ddk_scsi_port_s_interface_with_scsi_port_miniport_drivers_kg"></span><span id="DDK_SCSI_PORT_S_INTERFACE_WITH_SCSI_PORT_MINIPORT_DRIVERS_KG"></span>


Scsi ポートドライバーと SCSI ポートミニポートドライバーの間の通信は、SCSI 要求ブロック (SRBs) とミニポートドライバーのコールバックルーチンによって行われます。 SCSI ポートミニポートドライバーのコールバックルーチンの詳細については、「 [Scsi ミニポートドライバー](scsi-miniport-drivers.md)」を参照してください。

個々の SRB functions、SRB flags、SRB status 値の概要と定義については、「 [**SCSI\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)」を参照してください。

個々の SRB 関数にミニポートドライバーが応答する方法については、「 [SCSI ミニポートドライバーの HwScsiStartIo ルーチン](scsi-miniport-driver-s-hwscsistartio-routine.md)」を参照してください。

SCSI ポートは、アダプターがタグ付きキューをサポートしている場合を除き、SRBs を SCSI ポートミニポートドライバーに同期的に転送します。 タグ付きキューをサポートするホストバスアダプターは、要求を内部でキューに置いて、SCSI ポートが各要求に割り当てたタグによって示されている順序で処理することができます。 [**Scsi\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) (SRB) 構造体には、ホストアダプターの内部キュー ( **QueuedTag**と**Queueaction**) での SRBs の順序を指定するために scsi ポートドライバーが使用する2つのメンバーが含まれています。 SCSI ポートは、アダプターがパケットを処理する順序を示すカウント ( *"tag"* 値) を各 SRB の**QueuedTag**メンバーに割り当てます。 また、タグ値を使用して、正常に完了した SRBs とタイムアウトした SRBs を SCSI ポートで追跡することもできます。

**Queueaction**メンバーには、次のいずれかの値が割り当てられます。

SRB\_単純\_タグ\_要求

SRB\_ヘッド\_\_キュー\_タグ\_要求

SRB\_順序付けられた\_キュー\_タグ\_要求

これらの値の詳細については、「SCSI 2 の仕様」を参照してください。

 

 





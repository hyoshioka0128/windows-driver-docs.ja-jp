---
title: SCSI ポート ドライバーのキューの管理
description: SCSI ポート ドライバーのキューの管理
ms.assetid: ddcbd016-8d8b-4bbc-9c71-b7a5eaa61205
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01d1a53c7085d316aa659a26aee4dc43accaa222
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532457"
---
# <a name="scsi-port-drivers-queue-management"></a>SCSI ポート ドライバーのキューの管理


## <span id="ddk_scsi_port_driver_s_queue_management_kg"></span><span id="DDK_SCSI_PORT_DRIVER_S_QUEUE_MANAGEMENT_KG"></span>


SCSI ホスト アダプターは、処理できる I/O 要求のボリュームで大きく異なります。 特定のホスト アダプターの機能を過負荷を回避するには、記憶域クラス ドライバーまたは記憶域ポート ドライバーできる必要があります I/O 要求のフローを制御します。

Microsoft Windows 記憶域アーキテクチャでは、SCSI ポート ドライバーは、I/O のフロー制御のほとんどの側面を処理します。 記憶域クラス ドライバーは I/O 要求の任意の数を特定のアダプターの制限をテストすることがなく SCSI ポートに転送したがってできます。 SCSI ポートでは、キューの処理を停止する記憶域クラス ドライバーからの明示的な要求も受け付けます。

SCSI ポート ドライバーは、「固定」I/O 要求キュー基になるハードウェアによって報告されたエラー状態への応答キューに置かれた要求の処理を停止するたびと呼ばれます。 クラス ドライバーまたはその他のいくつかのより高度なドライバーが明示的に要求に応答の処理を停止するたびに、I/O 要求のキューを「ロック」する SCSI ポートといいます。

次のセクションでは、SCSI ポートのキューのステータスを変更する条件について説明します。 SCSI ポートの内部の I/O 要求キューに制御をより高度なドライバーが使用できるされる Srb についても説明します。

 

 





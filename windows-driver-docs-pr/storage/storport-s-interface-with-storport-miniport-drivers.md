---
title: Storport ミニポート ドライバー、Storport のインターフェイス
description: Storport ミニポート ドライバー、Storport のインターフェイス
ms.assetid: 8e09d6a6-7e4f-44fc-a2b0-5f21b4ac0593
ms.date: 06/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7b94d8738922399f4fb7f13c020264f758aad05c
ms.sourcegitcommit: d5e42ba5e760f3f993007c698a0169a893a81546
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "67253361"
---
# <a name="storports-interface-with-storport-miniport-drivers"></a>Storport ミニポート ドライバー、Storport のインターフェイス

Storport ドライバー、Storport ミニポート ドライバーの間の通信が行わによって SCSI 要求のブロック (される Srb) およびミニポート ドライバー コールバック ルーチン。 Storport ミニポート ドライバー コールバック ルーチンの詳細については、次を参照してください。 [Storport ドライバー ミニポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver-miniport-routines)します。

概要と SRB の個々 の関数、SRB フラグ、および SRB 状態の値の定義については、次を参照してください。 [ **SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)します。

ミニポート ドライバーが SRB 関数に対応する方法に関する話題は、次を参照してください。 [ **HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)します。

Storport は、される Srb を Storport ミニポート ドライバーで非同期処理のために転送します。 通常、ミニポート ドライバーには、実際には、要求を完了するまでに時間がかかります。 タグが付けられたキューをサポートするホスト バス アダプター (Hba) では、内部要求キューに配置でき、Storport を各要求に割り当てることのタグで示される順序で処理することができます。 [ **SCSI_REQUEST_BLOCK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio) (SRB) 構造体には、Storport およびミニポート ドライバーが使用される Srb がホスト アダプターの内部キューで順序付けする方法を指定する 2 つのメンバーが含まれています。

* **QueueTag**:Storport 割り当てます、カウントまたは *「タグ」* 値に、 **QueuedTag**各 SRB のメンバー。 このタグは、アダプターが、パケットを処理する順序を示します。 タグの値では、Storport これが、正常に完了される Srb は未解決のまま、およびこれがタイムアウトしたかを追跡することもできます。

* **QueueAction**: SRB_FLAGS_QUEUE_ACTION_ENABLE フラグが設定されている場合に使用されるタグ付けされたキュー メッセージを示す**SRB します。SrbFlags**します。 ミニポートの使用の**QueueAction**ミニポートに固有です。 HBA がサポートされている場合、SCSI ベース ミニポートは SCSI の仕様に準拠できます。 **QueueAction**値は次のいずれかを指定できます。

| Value | 説明 |
| ----- | ------- |
| SRB_SIMPLE_TAG_REQUEST | 要求はキューにし、すべての古い SRB_HEAD_OF_QUEUE_TAG_REQUEST と SRB_ORDERED_QUEUE_TAG_REQUEST 要求が終了した後は、任意の順序で実行します。 |
| SRB_ORDERED_QUEUE_TAG_REQUEST | すべての古い SRB_HEAD_OF_QUEUE_TAG_REQUEST と以前のすべての要求が完了した後にのみ、要求を実行します。 |
| SRB_HEAD_OF_QUEUE_TAG_REQUEST | キューの先頭にある要求を配置し、すべて他 SRB_HEAD_OF_QUEUE_TAG_REQUEST タグ付けされた要求を含む、キュー内の他のすべての要求の前に実行します。 |

詳細については、SCSI の仕様を参照してください。
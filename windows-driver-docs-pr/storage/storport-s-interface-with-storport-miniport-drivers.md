---
title: Storport ミニポートドライバーを使用した storport のインターフェイス
description: Storport ミニポートドライバーを使用した storport のインターフェイス
ms.assetid: 8e09d6a6-7e4f-44fc-a2b0-5f21b4ac0593
ms.date: 06/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 606c73f81cd052c83707bffa24a11cba821bd972
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844455"
---
# <a name="storports-interface-with-storport-miniport-drivers"></a>Storport ミニポートドライバーを使用した storport のインターフェイス

Storport ドライバーと Storport ミニポートドライバーの間の通信は、SCSI 要求ブロック (SRBs) とミニポートドライバーのコールバックルーチンによって行われます。 Storport ミニポートドライバーのコールバックルーチンの詳細については、「 [Storport ミニポートドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-driver-routines)」を参照してください。

個々の SRB 関数、SRB flags、および SRB status 値の概要と定義については、「 [**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)」を参照してください。

各 SRB 関数にミニポートドライバーが応答する方法については、 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)を参照してください。

Storport は、非同期処理のために SRBs を Storport ミニポートドライバーに転送します。 通常、ミニポートドライバーは、要求を実際に完了するまでに少し時間がかかります。 タグ付きキューをサポートするホストバスアダプター (Hba) は、要求を内部でキューに置いて、Storport が各要求に割り当てるタグによって示されている順序で処理することができます。 [**SCSI_REQUEST_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) (SRB) 構造体には、Storport およびミニポートドライバーがホストアダプターの内部キューで SRBs を並べ替える方法を指定するために使用する2つのメンバーが含まれています。

* **Queuetag**: Storport は、各 SRB の**QueuedTag**メンバーにカウント ( *"tag"* 値) を割り当てます。 このタグは、アダプターがパケットを処理する順序を示します。 また、タグ値を使用すると、Storport が正常に完了し、タイムアウトした SRBs を追跡することもできます。

* **Queueaction**: SRB で SRB_FLAGS_QUEUE_ACTION_ENABLE フラグが設定されている場合に使用されるタグ付きキューメッセージを示します **。SrbFlags**。 ミニポートの**Queueaction**の使用はミニポートに固有です。 SCSI ベースのミニポートは、HBA でサポートされていれば、SCSI 仕様に従うことができます。 **Queueaction**には、次のいずれかの値を指定できます。

| Value | 意味 |
| ----- | ------- |
| SRB_SIMPLE_TAG_REQUEST | すべての古い SRB_HEAD_OF_QUEUE_TAG_REQUEST および SRB_ORDERED_QUEUE_TAG_REQUEST 要求が終了したら、要求をキューに置いて任意の順序で実行します。 |
| SRB_ORDERED_QUEUE_TAG_REQUEST | 以前のすべての SRB_HEAD_OF_QUEUE_TAG_REQUEST とすべての古い要求が完了した後にのみ、要求を実行します。 |
| SRB_HEAD_OF_QUEUE_TAG_REQUEST | 要求をキューの先頭に配置し、他のすべての SRB_HEAD_OF_QUEUE_TAG_REQUEST タグ付き要求を含め、キュー内の他のすべての要求の前に実行します。 |

詳細については、SCSI の仕様を参照してください。
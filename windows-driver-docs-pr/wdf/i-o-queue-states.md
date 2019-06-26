---
title: I/O キューの状態
description: I/O キューの状態
ms.assetid: 99519d1c-20e5-4a32-8462-19ec9f907506
keywords:
- I/O は、WDK KMDF、状態をキューします。
- WDK の I/O キューを状態します。
- 現在の I/O キュー状態 WDK KMDF
- アイドル状態の I/O キューの状態 WDK KMDF
- WDK KMDF I/O キューの状態を準備します。
- 停止している I/O キューの状態 WDK KMDF
- WDK KMDF I/O キューの状態のドレイン
- WDK KMDF I/O キューの状態を消去
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec6ae9821b679d72821af5d10228bda4c8c530f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382827"
---
# <a name="io-queue-states"></a>I/O キューの状態


フレームワークには、次の状態の I/O キューを定義します。

<a href="" id="idle"></a>*アイドル状態します。*  
I/O キューに、I/O 要求が含まれていないと、ドライバーが I/O キューから受信したすべての要求を処理していません。

<a href="" id="ready"></a>*準備完了*  
I/O キューが、framework から I/O 要求を受信できるし、I/O 要求のドライバーに提供できます。

<a href="" id="stopped"></a>*停止*  
I/O キューは、framework からの I/O 要求を受信することができますが、ドライバーに I/O 要求を配信、ことはできませんし、ドライバーが I/O キューから受信したすべての要求を処理していません。

<a href="" id="drained"></a>*ドレインされます。*  
I/O キューが空で、フレームワークから新しい I/O 要求を受信することはできないことおよびドライバーに配信された I/O キューに含まれていたすべての I/O 要求。

<a href="" id="purged"></a>*消去*  
I/O キューが空、フレームワークから新しい I/O 要求を受信することはできないこと、および I/O キューに含まれていたすべての I/O 要求が取り消されました。

フレームワークは、ドライバーの呼び出し後準備完了状態に新しい I/O キューを設定することができます[ **WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)します。 ただし、[電源管理対象の I/O キュー](using-power-managed-i-o-queues.md)準備完了状態、デバイスの作業 (D0) 状態にある場合にのみを入力してください。

ドライバーでの I/O キューの状態を変更できます。

-   呼び出す[ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)または[ **WdfIoQueueStopSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)その停止状態でキューを配置します。

-   呼び出す[ **WdfIoQueueDrain** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain)または[ **WdfIoQueueDrainSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)のドレインされた状態でキューを配置します。

-   呼び出す[ **WdfIoQueuePurge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)または[ **WdfIoQueuePurgeSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)のパージされた状態でキューを配置します。

-   呼び出す[ **WdfIoQueueStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestart)にキューをその準備完了状態に戻ります。

I/O キューの現在の状態を取得するには、ドライバーを呼び出すことができます[ **WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuegetstate)します。

 

 






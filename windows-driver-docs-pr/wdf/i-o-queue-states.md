---
title: I/O キューの状態
description: I/O キューの状態
ms.assetid: 99519d1c-20e5-4a32-8462-19ec9f907506
keywords:
- I/o キュー WDK KMDF、状態
- 状態 WDK i/o キュー
- 現在の i/o キューの状態 WDK KMDF
- アイドル状態の i/o キューの状態 WDK KMDF
- ready i/o queue state WDK KMDF
- 停止した i/o キュー状態 WDK KMDF
- ドレインを行う i/o キューの状態 WDK KMDF
- 削除された i/o キュー状態 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0408d8aeaca95d4ad65b4ab7e1f8024a45e2c5db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845211"
---
# <a name="io-queue-states"></a>I/O キューの状態


このフレームワークは、i/o キューの次の状態を定義します。

<a href="" id="idle"></a>*退席*  
I/o キューに i/o 要求が含まれておらず、i/o キューから受信した要求がドライバーによって処理されていません。

<a href="" id="ready"></a> *」*  
I/o キューは、フレームワークから i/o 要求を受け取ることができ、ドライバーに i/o 要求を配信できます。

<a href="" id="stopped"></a>*なく*  
I/o キューは、フレームワークから i/o 要求を受信できますが、ドライバーに i/o 要求を配信できません。また、i/o キューから受信した要求はドライバーによって処理されません。

<a href="" id="drained"></a>*ドレインされ*  
I/o キューは空で、フレームワークからの新しい i/o 要求を受信できません。また、i/o キューにあったすべての i/o 要求がドライバーに配信されています。

<a href="" id="purged"></a>*さ*  
I/o キューが空で、フレームワークからの新しい i/o 要求を受信できず、i/o キューにあったすべての i/o 要求が取り消されています。

このフレームワークでは、ドライバーが[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)を呼び出した後に、新しい i/o キューを準備完了状態に設定できます。 ただし、[電源管理の i/o キュー](using-power-managed-i-o-queues.md)は、デバイスが動作中 (D0) 状態の場合にのみ、準備完了状態になります。

ドライバーは、次の方法で i/o キューの状態を変更できます。

-   キューを停止状態にするには、 [**Wdfioqueuestop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)または[**Wdfioqueuestopを同期的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)に呼び出します。

-   キューをドレインされた状態にするには、 [**Wdfioqueuedrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)または[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)を呼び出します。

-   削除された状態にキューを配置するには、 [**Wdfioqueuepurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)または[**WdfIoQueuePurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)を呼び出します。

-   [**Wdfioqueuestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)を呼び出して、キューを準備完了状態に戻します。

I/o キューの現在の状態を取得するために、ドライバーは[**WdfIoQueueGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuegetstate)を呼び出すことができます。

 

 






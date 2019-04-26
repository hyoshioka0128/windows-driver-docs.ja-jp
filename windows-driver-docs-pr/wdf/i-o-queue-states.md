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
ms.openlocfilehash: c3363f4eb48f76790b786eabc2a20af492449464
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341183"
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

フレームワークは、ドライバーの呼び出し後準備完了状態に新しい I/O キューを設定することができます[ **WdfIoQueueCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547401)します。 ただし、[電源管理対象の I/O キュー](using-power-managed-i-o-queues.md)準備完了状態、デバイスの作業 (D0) 状態にある場合にのみを入力してください。

ドライバーでの I/O キューの状態を変更できます。

-   呼び出す[ **WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)または[ **WdfIoQueueStopSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548489)その停止状態でキューを配置します。

-   呼び出す[ **WdfIoQueueDrain** ](https://msdn.microsoft.com/library/windows/hardware/ff547406)または[ **WdfIoQueueDrainSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff547412)のドレインされた状態でキューを配置します。

-   呼び出す[ **WdfIoQueuePurge** ](https://msdn.microsoft.com/library/windows/hardware/ff548442)または[ **WdfIoQueuePurgeSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548449)のパージされた状態でキューを配置します。

-   呼び出す[ **WdfIoQueueStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548478)にキューをその準備完了状態に戻ります。

I/O キューの現在の状態を取得するには、ドライバーを呼び出すことができます[ **WdfIoQueueGetState**](https://msdn.microsoft.com/library/windows/hardware/ff548437)します。

 

 






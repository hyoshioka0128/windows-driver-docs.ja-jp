---
title: システムのワーカー スレッド
description: システムのワーカー スレッド
ms.assetid: 01ae1c1b-0cb0-4b9b-bd74-341b7c289fd4
keywords:
- 実行ワーカー スレッドの WDK カーネル
- 作業項目の WDK カーネル
- スレッド オブジェクトの WDK カーネル
- 作業項目
- WorkItemEx
- ワーカー スレッドの WDK カーネル
- ワーカー スレッド コールバック ルーチン WDK カーネル
- コールバック ルーチン WDK ワーカー スレッド
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf3ce35dd4cafaa2cc890874199c6ceb77323031
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532331"
---
# <a name="system-worker-threads"></a>システムのワーカー スレッド





遅延の処理が必要なドライバーを使用して、*作業項目*、実際の処理を実行するドライバー コールバック ルーチンへのポインターが含まれています。 ドライバーは、作業項目をキューと*システム ワーカー スレッド*キューから作業項目を削除して、ドライバーのコールバック ルーチンを実行します。 システムでは、これらは一度に 1 つの作業項目を処理の各システムのスレッド システム ワーカー スレッドのプールを保持します。

ドライバー associates、 [ *WorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff566380)作業項目とコールバック ルーチン。 システムのワーカー スレッドが作業項目を処理するとき、関連付けられている呼び出し*WorkItem*ルーチン。 Windows Vista および以降のバージョンの Windows では、ドライバーは関連付けることが代わりに、 [ *WorkItemEx* ](https://msdn.microsoft.com/library/windows/hardware/ff566381)作業項目と日常的な。 *WorkItemEx*パラメーターとは異なるパラメーターを*作業項目*かかります。

*作業項目*と*WorkItemEx*ルーチンは、システム スレッドのコンテキストで実行します。 ドライバーのディスパッチ ルーチンは、ユーザー モード スレッドのコンテキストで実行できる場合、そのルーチンを呼び出すことができます、 *WorkItem*または*WorkItemEx*システム スレッドのコンテキストを必要とする操作を実行するルーチン。

作業項目を使用するには、ドライバーは、次の手順を実行します。

1.  割り当てし、新しい作業項目を初期化します。

    システムを使用して、 [ **IO\_WORKITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff550679)作業項目を保持する構造体。 新しい割り当てに**IO\_WORKITEM**構造体し作業項目として初期化、ドライバーを呼び出すことができます[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)します。 Windows Vista および Windows の以降のバージョンでは、ドライバーまたはを割り当てることが、独自**IO\_WORKITEM**構造、および呼び出し[ **IoInitializeWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549349)作業項目として構造体を初期化します。 (ドライバーを呼び出す必要があります[ **IoSizeofWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff550352)を作業項目を保持するために必要なバイト数を決定します)。

2.  コールバック ルーチンを作業項目に関連付けるし、システムのワーカー スレッドが処理されるように、作業項目をキューします。

    関連付ける、 *WorkItem*ドライバーの呼び出す必要があります、作業項目キュー作業項目と日常的な[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)。 関連付ける代わりに、 *WorkItemEx*ドライバーの呼び出す必要があります、作業項目キュー作業項目と日常的な[ **IoQueueWorkItemEx**](https://msdn.microsoft.com/library/windows/hardware/ff549474)します。

3.  作業項目が必要でなくなった後は、それを解放します。

    割り当てられた作業項目**IoAllocateWorkItem**によって解放する必要があります[ **IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)します。 によって初期化された作業項目**IoInitializeWorkItem**で初期化する必要があります[ **IoUninitializeWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff550392)解放できる前にします。

    作業項目は初期化されていないか、作業項目が現在キューにないときに解放のみできます。 そのため、作業項目のコールバック ルーチンを呼び出す前に、システムは、作業項目をデキュー **IoFreeWorkItem**と**IoUninitializeWorkItem**コールバック内から呼び出すことができます。

DPC 時間のかかる処理が必要ですか、ブロッキング呼び出しを実行する処理タスクを開始する必要があるには、1 つまたは複数の作業項目にタスクの処理を委任する必要があります。 DPC の実行中のすべてのスレッドは実行をされません。 さらに、DPC、IRQL でを実行するディスパッチ =\_レベル、ブロッキング呼び出しを行う必要がありません。 ただし、IRQL で作業項目を処理するシステム ワーカー スレッドが実行される = パッシブ\_レベル。 したがって、作業項目は、ブロッキング呼び出しを含めることができます。 たとえば、システム ワーカー スレッドは、ディスパッチャー オブジェクトで待機できます。

システム ワーカー スレッドのプールが、限られたリソースであるため*WorkItem*と*WorkItemEx*ルーチンを短時間のかかる操作に対してのみ使用できます。 かどうか (たとえば、無限ループがある) 場合、長時間実行されるこれらのルーチンのいずれかまたは長すぎる、システムの間、待機がデッドロックことができます。 そのため、ドライバーは、長時間の遅延の処理を必要とする場合に呼び出す必要があります代わりに[ **PsCreateSystemThread** ](https://msdn.microsoft.com/library/windows/hardware/ff559932)独自のシステム スレッドを作成します。

呼び出さない**IoQueueWorkItem**または**IoQueueWorkItemEx**キューにある作業項目をキューに登録します。 チェック ビルドは、このエラーが原因で、バグ チェックします。 製品版ビルドでエラーが検出されないがシステムの破損をデータ構造ができます。 特定のドライバーのルーチンが実行、ドライバーは毎回同じ作業項目をキューは、キューが既にいる場合は、2 番目の時間、作業項目のキューを避け、次の手法を使用することができます。

-   ドライバーは、ワーカーの日常のタスクの一覧を保持します。
-   このタスクの一覧は、ワーカーのルーチンに渡されるコンテキストで使用できます。 ワーカー ルーチンとタスクの一覧を変更するすべてのドライバー ルーチンは、リストへのアクセスを同期します。
-   ワーカーの日常的な実行されるたびに、一覧で、すべてのタスクを実行し、タスクが完了すると、各タスクを一覧から削除します。
-   新しいタスクが到着すると、ドライバーは、このタスクを一覧に追加します。 タスク一覧が空になる場合にのみ、ドライバーは、作業項目をキューします。

システムのワーカー スレッドは、ワーカー スレッドを呼び出す前に、キューから作業項目を削除します。 そのため、ドライバーのスレッドに安全にキューに配置できます作業項目もう一度ワーカー スレッドが実行を開始するとすぐにします。

 

 





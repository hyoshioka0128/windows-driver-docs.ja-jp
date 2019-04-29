---
title: ワーク キューのディスパッチ メカニズム
description: ワーク キューのディスパッチ メカニズム
ms.assetid: d4ce929f-2d84-4194-9afa-e00629594c36
keywords:
- RDBSS WDK ファイル システムでは、作業のキューのディスパッチ
- リダイレクトされたバッファリング サブシステム WDK のドライブのファイル システムでは、作業のキューのディスパッチ
- WDK RDBSS をディスパッチする作業キュー
- ワーク キュー WDK RDBSS のディスパッチ
- メモリ割り当て WDK RDBSS
- 重要な作業キュー WDK RDBSS
- 遅延作業キュー WDK RDBSS
- HyperCritical 作業キュー WDK RDBSS
- ブックキーピング WDK RDBSS
- WDK RDBSS の統計情報
- WDK RDBSS キュー
- WDK RDBSS を状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048e3de725fe96da64cc97e96bf208aa49cc6d5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322182"
---
# <a name="work-queue-dispatching-mechanisms"></a>ワーク キューのディスパッチ メカニズム


## <span id="ddk_work_queue_dispatching_mechanisms_if"></span><span id="DDK_WORK_QUEUE_DISPATCHING_MECHANISMS_IF"></span>


RDBSS では、Windows カーネルの作業キューを使用して、後で実行する複数のスレッドで操作をディスパッチします。 ネットワークのミニ リダイレクター ドライバーでは、後で実行するディスパッチ操作 RDBSS によって管理される作業のキューを使用できます。

RDBSS は、RDBSS で使用されるディスパッチ メカニズムを実装するいくつかのルーチンを提供します。 これらのルーチンは、ネットワークのミニ リダイレクター ドライバーによっても使用できます。

RDBSS は、デバイス オブジェクトごとに作業項目の追跡を保持します。 これにより、読み込みとアンロードのネットワークのミニ リダイレクターに関連付けられている競合状態を処理するために RDBSS できます。 これには、RDBSS で一定でないすべてのリソースを使用してから 1 つのネットワークのミニ リダイレクターを回避するためのメカニズムも提供します。

作業のディスパッチはどの項目は避けられません特定のシナリオがあります。 頻繁にメモリの割り当てを回避して、作業のこれらのシナリオでの操作を解放する\_キュー\_項目が別のデータの一部として割り当てられます。 ディスパッチはまれな他のシナリオで必要になるまで、メモリの割り当てを回避するためによいでしょう。 RDBSS 作業キューの実装は、ディスパッチ、および作業のキューの要求の送信の形式でこれらのシナリオの両方を提供します。 使用してディスパッチの場合、 [ **RxDispatchToWorkerThread** ](https://msdn.microsoft.com/library/windows/hardware/ff554398)ルーチン、作業のメモリが\_キュー\_項目は、呼び出し元によって割り当てられる必要があります。 使用してをポストするため、 [ **RxPostToWorkerThread** ](https://msdn.microsoft.com/library/windows/hardware/ff554620)ルーチン、作業メモリ\_キュー\_項目は、呼び出し元によって割り当てられる必要があります。

ワーカー スレッドにディスパッチ操作の 2 つの一般的なケースがあります。

-   非常に頻度の低い操作では、使用、 **RxDispatchToWorkerThread**ルーチンを動的に割り当てと作業キュー項目のメモリを解放して、必要な場合で、メモリ使用量を節約します。

-   操作が繰り返しディスパッチするときを使用して、 **RxPostToWorkerThread**ルーチンは、作業を事前に割り当てることによって時間を節約するために\_キュー\_ディスパッチするデータ構造の一部として項目.

2 つのディスパッチ操作間のトレードオフは、容量 (メモリ使用量) との時間です。

RDBSS でディスパッチ メカニズムは、プロセッサごとの作業キューの複数のレベルを提供します。 現在サポートされている作業のキューの次のレベル:

-   重大

-   遅延

-   HyperCritical

重大と遅延の違いでは、優先度の 1 つです。 HyperCritical レベルは、そのルーチンをブロックしないでください (任意のリソースを待機します)、その他の 2 つと異なります。 ディスパッチ メカニズムの有効性は、クライアントの暗黙的な連携に依存していますので、この要件を適用できません。

RDBSS での作業キューの実装が KQUEUE 実装が構築されています。 追加のサポートには、作業項目をアクティブに待機しているスレッド数の規則が含まれます。 各作業のキューのデータ構造体では非ページ プール メモリから割り当てられたであり、独自の同期メカニズム (スピンロック)。

RDBSS には、ブックキーピング情報 (キューの状態および型など) に加えは作業キューの有効期間にわたって収集された統計情報も保持されます。 これにより、チューニング作業キューに価値ある情報。 処理があるが処理された項目の数、項目の数と、累積的なキューの長さは structureed します。 累積的なキューの長さは、重要な指標であり、追加の作業項目がキューに登録するたびに処理を待機している項目の数の合計を表します。 処理された項目の合計数と処理する項目の数の合計で除算する累積的なキューの長さは、キューの平均長を示す値を示します。 1 よりもはるかに大きい値では、ワーク キューに関連付けられているワーカー スレッドの最小数を大きくできることを示します。 もずっと少ない 1 つの値は、キューに関連付けられている作業スレッドの最大数を削減できることを示します。

通常、作業のキューは、アクティブな状態で起動し、か回復できないような状況が発生した (例については、システム リソースの不足) または非アクティブの状態に遷移したときにするまで続行します。 ランダウンが開始されると、ランダウン中の状態に遷移します。

スレッドをスピン ダウンされているときに、作業キューの内訳は完了しません。 スレッドの終了は、データ構造を破棄する前にすることを確認する必要があります。 RDBSS での作業キューの実装では、ランダウンのコンテキスト内のスレッド オブジェクトへの参照を保存ダウンがスピンオフされるスレッドの各プロトコルに従います。 (これは作業キューに属さない) スレッドを発行ランダウンは、すべてのデータ構造を破棄する前に休止スレッドの完了を待機します。

現在の実装**RxDispatchToWorkerThread**と**RxPostToWorkerThread**キューは、同じプロセッサを呼び出し元に機能します。

作業キューをディスパッチするため、次の RDBSS ルーチンが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554398" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554398)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカー スレッドのコンテキスト内のルーチンを呼び出します。 WORK_QUEUE_ITEM 用のメモリは、このルーチンによって割り当てられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554620" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554620)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカー スレッドのコンテキストでルーチンを呼び出します。 呼び出し元によって、WORK_QUEUE_ITEM のメモリを割り当てる必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554734" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554734)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>このルーチンのネットワークのミニ リダイレクター ディスパッチャー コンテキストを廃棄します。</p>
<p>このルーチンは、Windows Server 2003 および Windows XP で使用可能なだけに注意してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





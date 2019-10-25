---
title: ワークキューのディスパッチメカニズム
description: ワークキューのディスパッチメカニズム
ms.assetid: d4ce929f-2d84-4194-9afa-e00629594c36
keywords:
- RDBSS WDK ファイルシステム、ワークキューのディスパッチ
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、ワークキューのディスパッチ
- ワークキューのディスパッチ (WDK RDBSS)
- 作業キュー WDK RDBSS をディスパッチしています
- メモリ割り当て (WDK RDBSS)
- 重要な作業キュー WDK RDBSS
- 遅延作業キュー WDK RDBSS
- ハイパークリティカル作業キュー WDK RDBSS
- 簿記 (WDK RDBSS)
- 統計 WDK RDBSS
- キュー WDK RDBSS
- 状態 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6af47ab5c37c94b426044fac2490d8b5b3e8c461
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840930"
---
# <a name="work-queue-dispatching-mechanisms"></a>ワークキューのディスパッチメカニズム


## <span id="ddk_work_queue_dispatching_mechanisms_if"></span><span id="DDK_WORK_QUEUE_DISPATCHING_MECHANISMS_IF"></span>


RDBSS は、Windows カーネルワークキューを使用して、後で実行するために複数のスレッドで操作をディスパッチします。 ネットワークミニリダイレクタードライバーは、RDBSS によって管理される作業キューを使用して、後で実行するためのディスパッチ操作を行うことができます。

RDBSS には、RDBSS で使用されるディスパッチ機構を実装するいくつかのルーチンが用意されています。 これらのルーチンは、ネットワークミニリダイレクタードライバーでも使用できます。

RDBSS は、作業項目をデバイス単位で追跡します。 これにより、RDBSS はネットワークミニリダイレクターの読み込みとアンロードに関連する競合状態を処理できます。 これは、すべてのリソースを使用して起因が1つのネットワークミニリダイレクターを防ぐことができるように、RDBSS のメカニズムを提供します。

作業項目のディスパッチが避けられない特定のシナリオがあります。 このようなシナリオでは、メモリの割り当てが頻繁に行われず、操作が解放されるのを防ぐために、WORK\_QUEUE\_ITEM が別のデータの一部として割り当てられます。 ディスパッチがあまり行われない他のシナリオでは、必要になるまでメモリの割り当てが行われないようにします。 RDBSS work queue の実装では、これらの両方のシナリオを、作業キュー要求のディスパッチとポスティングの形式で提供します。 [**RxDispatchToWorkerThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread)ルーチンを使用してディスパッチする場合は、作業\_キュー\_項目のメモリが、呼び出し元によって割り当てられる必要があります。 [**RxPostToWorkerThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread)ルーチンを使用して投稿する場合、WORK\_QUEUE\_ITEM のメモリは、呼び出し元によって割り当てられる必要があります。

ワーカースレッドへの操作のディスパッチには、次の2つの一般的なケースがあります。

-   非常に頻度の低い操作の場合は、 **RxDispatchToWorkerThread**ルーチンを使用して、必要に応じて作業キュー項目のメモリを動的に割り当てたり解放したりすることによって、メモリの使用量を節約します。

-   操作を繰り返しディスパッチする場合は、 **RxPostToWorkerThread**ルーチンを使用して、ディスパッチされるデータ構造の一部として作業\_キュー\_項目を事前に割り当てて、時間を節約します。

2つのディスパッチ操作の間のトレードオフは、時間と領域 (メモリ使用) です。

RDBSS のディスパッチメカニズムは、プロセッサごとに複数のレベルの作業キューを提供します。 現在サポートされている作業キューのレベルは次のとおりです。

-   重大

-   遅延

-   ハイパークリティカル

Critical と遅延の区別は、優先度の1つです。 ハイパークリティカルレベルは他の2つとは異なり、ルーチンはブロックしないでください (任意のリソースを待機する必要があります)。 この要件を強制することはできないため、ディスパッチメカニズムの有効性は、クライアントの暗黙的な連携に依存します。

RDBSS でのワークキューの実装は、KQUEUE 実装に基づいて構築されています。 追加のサポートには、作業項目をアクティブに待機している多数のスレッドの規則が含まれます。 各ワークキューのデータ構造は、非ページプールのメモリから割り当てられ、独自の同期機構 (スピンロック) を持ちます。

RDBSS では、ブックの情報 (キューの状態と種類など) だけでなく、ワークキューの有効期間に収集される統計も保持されます。 これにより、ワークキューのチューニングに関する有益な情報を得ることができます。 処理された項目の数、処理する必要がある項目の数、および累積キューの長さは構造になります。 累積キューの長さは重要なメトリックであり、追加の作業項目がキューに登録されるたびに処理を待機している項目の数の合計を表します。 累積キューの長さは、処理された項目の合計数と処理される項目の数の合計で割った値によって、キューの長さの平均が示されます。 値が1以上の場合は、ワークキューに関連付けられているワーカースレッドの最小数を増やすことができます。 1未満の値は、キューに関連付けられている作業スレッドの最大数を減らすことができることを示します。

ワークキューは通常、アクティブな状態で開始し、回復不可能な状況 (システムリソースの不足など) が発生するか、非アクティブな状態に遷移するまで続行されます。 ランダウンが開始されると、進行状況のランダウン状態に遷移します。

スレッドがスピンダウンされた場合、作業キューのランダウンは完了しません。 データ構造を破棄する前に、スレッドの終了を確認する必要があります。 RDBSS の作業キューの実装は、スピンダウンする各スレッドがランダウンコンテキストでスレッドオブジェクトへの参照を保存するプロトコルに従います。 ランダウン実行スレッド (ワークキューに属していない) は、データ構造を細分化する前に、すべてのスレッドの完了を待機します。

**RxDispatchToWorkerThread**および**RxPostToWorkerThread**キューの現在の実装は、呼び出し元と同じプロセッサ上で動作します。

作業キューのディスパッチに関する次の RDBSS ルーチンには、が含まれます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカースレッドのコンテキストでルーチンを呼び出します。 WORK_QUEUE_ITEM のメモリは、このルーチンによって割り当てられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカースレッドのコンテキストでルーチンを呼び出します。 WORK_QUEUE_ITEM のメモリは、呼び出し元によって割り当てられる必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクターのディスパッチャーコンテキストを破棄します。</p>
<p>このルーチンは、Windows Server 2003 および Windows XP でのみ使用できます。</p></td>
</tr>
</tbody>
</table>

 

 

 





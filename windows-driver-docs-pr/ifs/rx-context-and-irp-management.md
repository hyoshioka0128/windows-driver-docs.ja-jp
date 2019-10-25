---
title: RX_CONTEXT と IRP 管理
description: RX_CONTEXT と IRP 管理
ms.assetid: 74ca681d-2599-442c-aebe-3556d6354f7f
keywords:
- RDBSS WDK ファイルシステム、Irp
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、Irp
- RX_CONTEXT 構造体
- データ構造の WDK ファイルシステム
- RDBSS WDK ファイルシステム、接続およびファイル構造
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、接続とファイルの構造
- 接続構造 (WDK RDBSS)
- ファイル構造の WDK RDBSS
- 構造の WDK RDBSS
- 接続情報 WDK RDBSS
- Irp WDK RDBSS
- I/o 要求パケット WDK RDBSS
- コンテキスト WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f08b93c8535bf2c782d20e8902e0852ab59e36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840982"
---
# <a name="rx_context-and-irp-management"></a>RX\_コンテキストと IRP 管理


## <span id="ddk_rx_context_and_irp_management_if"></span><span id="DDK_RX_CONTEXT_AND_IRP_MANAGEMENT_IF"></span>


RX\_コンテキスト構造は、i/o 要求パケット (IRP) を管理するために RDBSS とネットワークミニリダイレクターによって使用される基本的なデータ構造の1つです。 RX\_コンテキスト構造は、処理中の IRP を記述し、IRP の完了時にグローバルリソースを解放するための状態情報を格納します。 RX\_CONTEXT データ構造体は、RDBSS、ネットワークミニリダイレクター、およびファイルシステムで使用される IRP をカプセル化します。 RX\_コンテキスト構造体には、単一の IRP へのポインターと、IRP を処理するために必要なすべてのコンテキストが含まれます。

RX\_コンテキスト構造は、Windows Driver Kit (WDK) のヘッダーファイルおよびネットワークミニリダイレクタードライバーの開発に使用されるその他のリソースで、IRP コンテキストまたは RxContext と呼ばれることがあります。

RX\_コンテキストは、さまざまなネットワークミニリダイレクターによって提供される追加情報が接続されるデータ構造です。 設計の観点からは、この追加情報は次のいずれかの方法で処理できます。

-   コンテンツを格納するためにネットワークミニリダイレクターが使用する、RX\_コンテキストの一部としてコンテキストポインターを定義できるようにします。 これは、RX\_コンテキスト構造が割り当てられ破棄されるたびに、ネットワークミニリダイレクタードライバーは、追加のネットワークミニリダイレクターを含むメモリブロックの割り当てまたは破棄を個別に実行する必要があることを意味します。参照. RX\_コンテキスト構造は作成され、大きな数値で破棄されるため、パフォーマンスの観点からは許容できるソリューションではありません。

-   もう1つの方法は、各 RX\_コンテキスト構造のサイズを、各ネットワークミニリダイレクターの事前に指定された量だけ割り当てることで構成されます。これは、ミニリダイレクターで使用するために予約されます。 このような方法を採用すると、追加の割り当てと破棄が回避されますが、RDBSS の RX\_コンテキスト管理コードが複雑になります。

-   3番目の方法では、事前に指定された領域を割り当てます。これは、各 RX\_コンテキストの一部として、すべてのネットワークミニリダイレクターで同じです。 これは、さまざまなネットワークミニリダイレクターによって必要な構造を設定できる、フォーマットされていない領域です。 このようなアプローチでは、以前のアプローチに関連する欠点を克服できます。 これは、RDBSS で現在実装されているアプローチです。

3番目の方法は、RDBSS によって使用されるスキームです。 そのため、ネットワークミニリダイレクタードライバーの開発者は、RX\_コンテキストデータ構造で定義されているこの事前指定領域に適合するように、関連付けられているプライベートコンテキストを試して定義する必要があります。 この規則に違反するネットワークミニリダイレクタードライバーは、大幅なパフォーマンスの低下を伴います。

ネットワークミニリダイレクターによってエクスポートされる多くの RDBSS ルーチンおよびルーチンは、受信側のスレッドまたはルーチンによって使用されるその他のスレッドで、RX\_のコンテキスト構造を参照します。 したがって、RX\_のコンテキスト構造は参照カウントされ、非同期操作の使用を管理します。 参照カウントがゼロになると、RX\_コンテキスト構造を終了し、最後の逆参照操作で解放できます。

RDBSS は、RX\_コンテキスト構造および関連する IRP を操作するために使用される多くのルーチンを提供します。 これらのルーチンは、RX\_コンテキスト構造の割り当て、初期化、および削除に使用されます。 これらのルーチンは、RX\_コンテキストに関連付けられている IRP を完了し、RX\_コンテキストのキャンセルルーチンを設定するためにも使用されます。

次のルーチンは、RX\_コンテキスト構造体を操作します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造に関連付けられている IRP を完了するために使用されます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造に関連付けられている IRP を完了するために使用されます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>このルーチンは、新しい RX_CONTEXT 構造体を割り当て、データ構造体を初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体を逆参照し、参照カウントがゼロになると、指定された RX_CONTEXT 構造体を RDBSS のメモリ内データ構造から解放し、削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>このルーチンは、新しく割り当てられた RX_CONTEXT 構造体を初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>このルーチンは、以前に実行されたすべての操作固有の割り当てと買収をリセットすることによって、再利用できるように RX_CONTEXT 構造を準備します。 IRP から取得したパラメーターは変更されません。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>このルーチンは、シリアル化されたブロッキング i/o キューで次の待機中のスレッド (存在する場合) をウェイクアップします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>ルーチンは、RX_CONTEXT 構造体のネットワークミニリダイレクターのキャンセルルーチンを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>このルーチンは、ブロッキング i/o を同じ作業キューに同期するために使用されます。 このルーチンは、名前付きパイプ操作を同期するために RDBSS によって内部的に使用されます。 ネットワークミニリダイレクターはこのルーチンを使用して、ネットワークミニリダイレクターによって管理されている別のキューで操作を同期します。</p>
<p>このルーチンは、Windows Server 2003 でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>このルーチンは、ブロッキング i/o を同じ作業キューに同期するために使用されます。 このルーチンは、名前付きパイプ操作を同期するために RDBSS によって内部的に使用されます。 ネットワークミニリダイレクターはこのルーチンを使用して、ネットワークミニリダイレクターによって管理されている別のキューで操作を同期します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、前の表に示したルーチンを呼び出す*rxcontx*ヘッダーファイルで定義されています。 これらのマクロは、通常、これらのルーチンを直接呼び出す代わりに使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>、<em>FCB</em>、<em>ioqueue</em>)</p></td>
<td align="left"><p>このマクロは、ブロッキング i/o 要求を同じ作業キューに同期します。 Windows Server 2003 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>FALSE</strong>に設定して<strong>__RxSynchronizeBlockingOperations</strong>ルーチンを呼び出します。</p>
<p>Windows XP および Windows 2000 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>FALSE</strong>に設定して<strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>、<em>FCB</em>、<em>ioqueue</em>)</p></td>
<td align="left"><p>このマクロは、ブロッキング i/o 要求を同じ作業キューに同期します。 Windows Server 2003 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>TRUE</strong>に設定して<strong>__RxSynchronizeBlockingOperations</strong>ルーチンを呼び出します。</p>
<p>Windows XP および Windows 2000 では、このマクロは<em>Dropfcblock</em>パラメーターを<strong>TRUE</strong>に設定して<strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong>ルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 





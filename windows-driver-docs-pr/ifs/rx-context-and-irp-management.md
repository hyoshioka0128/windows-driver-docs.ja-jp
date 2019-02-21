---
title: RX_CONTEXT と IRP の管理
description: RX_CONTEXT と IRP の管理
ms.assetid: 74ca681d-2599-442c-aebe-3556d6354f7f
keywords:
- Irp、RDBSS WDK ファイル システム
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、Irp
- RX_CONTEXT 構造体
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
- Irp WDK RDBSS
- I/O 要求パケット WDK RDBSS
- WDK RDBSS コンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 699a5743801eb94dc6a5a7ea1ade1ccb3bb9c2f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532408"
---
# <a name="rxcontext-and-irp-management"></a>RX\_コンテキストと IRP の管理


## <span id="ddk_rx_context_and_irp_management_if"></span><span id="DDK_RX_CONTEXT_AND_IRP_MANAGEMENT_IF"></span>


RX\_CONTEXT 構造は RDBSS によって使用される、基本的なデータ構造のいずれかと、I/O を管理するネットワークのミニ-リダイレクター要求パケット (IRP)。 RX\_CONTEXT 構造は、処理中であり、グローバル リソースを IRP が完了すると解放を許可する状態情報が含まれています、IRP をについて説明します。 RX\_コンテキスト データ構造にカプセル化 IRP RDBSS を使用して、ネットワークのミニ リダイレクター、およびファイル システム。 RX\_CONTEXT 構造に 1 つの IRP とそのすべての IRP の処理に必要なコンテキストへのポインターが含まれています。

RX\_CONTEXT 構造は IRP コンテキストまたは RxContext Windows Driver Kit (WDK) のヘッダー ファイルとネットワーク ミニ リダイレクター ドライバーの開発に使用されるその他のリソースとして呼ばします。

RX\_コンテキストはさまざまなネットワークのミニ リダイレクターによって提供される追加情報が接続されているデータ構造体。 設計の観点からは、この追加情報をいくつかの方法のいずれかで処理できます。

-   RX の一部として定義するコンテキスト ポインターでは、\_コンテキストで、ネットワークのミニ リダイレクターを使用して情報を格納できます。 つまり、たびに、RX\_CONTEXT 構造体が割り当てられ、破棄、ネットワークのミニ リダイレクター ドライバーには、関連付けられている別の割り当てまたは追加のネットワークを保持するメモリ ブロックの破棄を実行する必要がありますミニ リダイレクター情報。 RX 以降\_コンテキスト構造が作成され、多数の破棄、これはパフォーマンスの観点から適切な解決策ではありません。

-   別の方法では各 RX のサイズの割り当てを\_の各ネットワーク ミニ リダイレクター、ミニ リダイレクターを使用し、予約されている、事前に指定したコンテキストの構造体。 このアプローチは、追加の割り当てを回避でき、破棄は、RX が複雑になります。\_RDBSS で管理コードのコンテキスト。

-   3 番目のアプローチは、各 RX の一部としてすべてのネットワーク ミニ リダイレクターは、同じ指定済みの領域を割り当てる\_コンテキスト。 これは、書式設定されていない領域をその上には、すべての必要な構造をさまざまなネットワークのミニ リダイレクターによって課されることができます。 このアプローチは、以前のアプローチの欠点を克服しています。 これは、現在 RDBSS で実装されているアプローチです。

3 番目のアプローチは、RDBSS によって使用されるスキームです。 その結果、ネットワーク ミニ リダイレクター ドライバーの開発者を再試行してくださいし、RX で定義されているこの指定済みの領域に収まるように関連付けられているプライベート コンテキストを定義する必要があります\_コンテキスト データ構造体。 このルールに違反しているネットワーク ミニ リダイレクター ドライバーには、著しいパフォーマンスの低下が発生します。

多くの RDBSS ルーチンやネットワークのミニ リダイレクターによってエクスポートされたルーチンが RX への参照を\_発信側のいずれかのスレッドまたは他のルーチンで使用されるスレッド コンテキストの構造体。 そのため、RX\_CONTEXT 構造体は非同期操作の使用を管理するカウントされた参照。 参照カウントがゼロ、RX になったときに\_CONTEXT 構造の作成が完了し、最後にリリースできる操作を逆参照します。

RDBSS、RX の操作に使用するルーチンのいくつか提供されます\_CONTEXT 構造体と関連付けられている IRP します。 これらのルーチンを割り当て、初期化、および、RX の削除に使用\_CONTEXT 構造体。 これらのルーチンは、RX に関連付けられている IRP の完了にも使用\_コンテキストと、RX のキャンセル ルーチンを設定\_コンテキスト。

次のルーチン操作 RX\_CONTEXT 構造体。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554340" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554340)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体に関連付けられている IRP の完了に使用されます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554348" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554348)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体に関連付けられている IRP の完了に使用されます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554367" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554367)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>このルーチンでは、新しい RX_CONTEXT 構造、データ構造体を初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554393" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554393)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体を逆参照し、参照カウントがゼロにする場合の割り当てを解除し、RDBSS インメモリ データ構造体から指定した RX_CONTEXT 構造を削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554502" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554502)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>このルーチンでは、新しく割り当てられた RX_CONTEXT 構造体を初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554643" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554643)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>このルーチンは、すべての操作に固有の割り当てと以前に行った買収をリセットして再利用するため、RX_CONTEXT 構造を準備します。 IRP から得られるパラメーターは変更されません。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554701" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554701)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>このルーチンは、シリアル化されたブロッキング I/O キューに存在する場合、次の待機スレッドをウェイクします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554722" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554722)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>ネットワークのミニ リダイレクターを日常的な設定は、RX_CONTEXT 構造体のルーチンをキャンセルします。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff557377" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557377)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>このルーチンは、同じ作業キューにブロッキング I/O を同期に使用されます。 このルーチンが、名前付きパイプ操作を同期する RDBSS によって内部的に使用されます。 このルーチンは、ネットワーク ミニリダイレクターによって保持されている別のキューに対する操作を同期するネットワークのミニ リダイレクターを使用できます。</p>
<p>ルーチンは、Windows Server 2003 にできるだけです。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff557382" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557382)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>このルーチンは、同じ作業キューにブロッキング I/O を同期に使用されます。 このルーチンが、名前付きパイプ操作を同期する RDBSS によって内部的に使用されます。 このルーチンは、ネットワーク ミニリダイレクターによって保持されている別のキューに対する操作を同期するネットワークのミニ リダイレクターを使用できます。</p>
<p>ルーチンは、Windows XP および Windows 2000 にできるだけです。</p></td>
</tr>
</tbody>
</table>

 

次のマクロが定義されている、 *rxcontx.h*前の表に、ルーチンを呼び出して、ヘッダー ファイルが一覧表示します。 これらのマクロは、通常これらのルーチンを直接呼び出す代わりに使用されます。

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
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>このマクロは、同じ作業キューにブロッキング I/O 要求を同期します。 Windows Server 2003 では、このマクロを呼び出す、 <strong>__RxSynchronizeBlockingOperations</strong>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>FALSE</strong>します。</p>
<p>Windows XP および Windows 2000 では、このマクロを呼び出し、 <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>FALSE</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>このマクロは、同じ作業キューにブロッキング I/O 要求を同期します。 Windows Server 2003 では、このマクロを呼び出す、 <strong>__RxSynchronizeBlockingOperations</strong>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>TRUE</strong>します。</p>
<p>Windows XP および Windows 2000 では、このマクロを呼び出し、 <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong>ルーチン、 <em>DropFcbLock</em>パラメーターに設定<strong>TRUE</strong>.</p></td>
</tr>
</tbody>
</table>

 

 

 





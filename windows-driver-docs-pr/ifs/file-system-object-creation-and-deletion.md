---
title: ファイル システム オブジェクトの作成と削除
description: ファイル システム オブジェクトの作成と削除
ms.assetid: 71e342cf-455f-4b01-af55-12568bf06728
keywords:
- ミニリダイレクター WDK、オブジェクトの作成
- ミニリダイレクター WDK、オブジェクトの削除
- ファイルオブジェクト WDK ミニリダイレクター
- オブジェクト WDK ミニリダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcc313d55a7ca43bf52697599455ea37c78d7199
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841420"
---
# <a name="file-system-object-creation-and-deletion"></a>ファイル システム オブジェクトの作成と削除


ネットワークミニリダイレクターによって実装されるルーチンの多くは、ファイルの作成と削除を対象としています。 RDBSS では、SRV\_OPEN、FCB、FOBX 構造体を含む複数の構造体を作成して、このプロセスを抽象化しています。これには参照カウントが含まれます。 通常、ファイルシステムオブジェクトを作成または開くには、SRV\_OPEN、FCB、および FOBX 構造体を作成する必要があります。 通常の手順では、RDBSS がネットワークミニリダイレクターによって実装された[**MRxCreate**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)ルーチンを呼び出して、これらの構造体に情報を入力します。 また、 [**MRxShouldTryToCollapseThisOpen**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)ルーチンと[**MRxCollapseOpen**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)ルーチンを使用して、既存の SRV\_オープン構造の open/create file 要求を折りたたむこともできます。

ネットワークリダイレクターのコンテキストでは、ファイルオブジェクトはファイル制御ブロック (FCB) 構造体とファイルオブジェクト拡張 (FOBX) 構造体を参照します。 ファイルオブジェクトと FOBXs の間には1対1の対応があります。 多くのファイルオブジェクトは、リモートサーバー上の1つのファイルを表す同じ FCB 構造体を参照します。 クライアントは、同じ FCB で複数の異なる open requests (NtCreateFile requests) を持つことができ、これらはそれぞれ新しいファイルオブジェクトを作成します。 RDBSS とネットワークミニリダイレクターは、受信された NtCreateFile 要求よりも[**MRxCreate**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)要求を送信することを選択できます。これは、サーバーオープン要求 (SRV\_open) を複数の FOBXs で共有する場合に有効です。

RDBSS とネットワークミニリダイレクターは、ユーザーがファイルを閉じたときに、必ずしも SRV\_開いている構造を閉じるとは限りません。 RDBSS は、サーバーとの接続がなくても、開いている構造とデータを SRV\_再利用することができます。 一部の Windows アプリケーションでは、ファイルを開いて読み取り、閉じ、同じファイルをすばやく開くことができます。 このような場合は、SRV\_開いている構造体を再利用すると、パフォーマンスが向上します。

これらのデータ構造を閉じて最終処理するために使用されるルーチンがいくつかあります。また、不要になったときに使用されるメモリやその他のリソースを解放します。 これらのルーチンには、 [**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))、 [**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)、 [**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)、 [**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)、および[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)が含まれます。

次の表に、ファイルシステムオブジェクトの作成および削除操作のためにネットワークミニリダイレクターで実装できるルーチンを示します。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>2つの FCB オブジェクトが同じファイルを表している場合、RDBSS はこのルーチンを呼び出してネットワークミニリダイレクターを照会します。 RDBSS は、同じように見える2つのファイルを処理するときにこのルーチンを呼び出しますが、名前は異なります (MS-DOS の短い名前と長い名前など)。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトの拡張を閉じることを要求します。 RDBSS は、ファイルオブジェクトに対して IRP_MJ_CLEANUP を受け取ることに応答して、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが SRV_OPEN オブジェクトを閉じることを要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターが開いているファイルシステム要求を既存の SRV_OPEN に折りたたんでいることを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトを作成するように要求します。 この呼び出しは、IRP_MJ_CREATE の受信に応答して RDBSS によって発行されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターによって FCB が割り当て解除されるように要求します。 この呼び出しは、ファイルシステムオブジェクトを閉じる要求に応答しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターに FOBX の割り当てを解除するように要求します。 この呼び出しは、ファイルシステムオブジェクトを閉じる要求に応答しています。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ファイルがキャッシュマネージャーによってキャッシュされるときに、ネットワークミニリダイレクターがファイルを拡張することを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ファイルがキャッシュマネージャーによってキャッシュされていない場合に、ネットワークミニリダイレクターがファイルを拡張することを要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトをフラッシュすることを要求します。 RDBSS は、IRP_MJ_FLUSH_BUFFERS の受信に応答してこの呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS はこのルーチンを呼び出して、ネットワークミニリダイレクターが強制的に閉じることを要求します。 このルーチンは、SRV_OPEN の条件が適切でない場合、または SRV_OPEN が closed とマークされている場合に呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、この NET_ROOT でバイト範囲ロックがサポートされているかどうかをネットワークミニリダイレクターが示していることを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、RDBSS が開いている要求を既存のファイルシステムオブジェクトに対して試行するかどうかを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ネットワークミニリダイレクターがファイルシステムオブジェクトを切り捨てることを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出して、ファイルサイズが FCB の有効なデータ長よりも大きい場合に、ファイルがクリーンアップ時にいっぱいになるファイルシステムオブジェクトをネットワークミニリダイレクターが拡張するように要求します。</p></td>
</tr>
</tbody>
</table>

 

 

 





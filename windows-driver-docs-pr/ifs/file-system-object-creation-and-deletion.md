---
title: ファイル システム オブジェクトの作成と削除
description: ファイル システム オブジェクトの作成と削除
ms.assetid: 71e342cf-455f-4b01-af55-12568bf06728
keywords:
- ミニ リダイレクター WDK、オブジェクトの作成
- ミニ リダイレクター WDK、オブジェクトの削除
- ファイル オブジェクト WDK のミニ リダイレクター
- WDK のミニ リダイレクター オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c6df811a7e802e836f7a19a86cc8eb60570b825
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369273"
---
# <a name="file-system-object-creation-and-deletion"></a>ファイル システム オブジェクトの作成と削除


さまざまなネットワークのミニ リダイレクターによって実装されるルーチンはファイルの作成および削除です。 RDBSS、SRV をなど、いくつかの構造を作成してこのプロセスを抽象化\_構造体にオープン、FCB、および FOBX 参照がカウントされます。 作成またはファイル システム オブジェクトを正常に開く SRV を作成する必要が\_オープン、FCB、および FOBX 構造体。 呼び出す RDBSS の通常の手順になります、 [ **MRxCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)ルーチンがこれらの構造体に情報を入力するネットワークのミニ リダイレクターによって実装されます。 既存の SRV でファイルを開くか作成要求を縮小することも\_オープン構造体を使用して、 [ **MRxShouldTryToCollapseThisOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)と[ **MRxCollapseOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)ルーチン。

ネットワーク リダイレクターのコンテキストでは、ファイル オブジェクトは、ファイル制御ブロック (FCB) 構造とファイル オブジェクトの拡張機能 (FOBX) 構造を参照します。 ファイル オブジェクトと FOBXs、一対一で対応があります。 多くのファイル オブジェクトは、同じの FCB の構造は、リモート サーバー上のどこか 1 つのファイルを表すを参照してください。 クライアントが同じ FCB のいくつかの異なるオープン要求 (NtCreateFile 要求) を持つことができ、これらの新しいファイル オブジェクトが作成されます。 少ない送信 RDBSS とネットワークのミニ リダイレクターできます[ **MRxCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate) NtCreateFile 要求を受信すると、有効なサーバーのオープン要求を共有するよりも要求 (SRV\_開きます)いくつかの FOBXs 間。

RDBSS とネットワークのミニ リダイレクターは必ずしも閉じないで、SRV\_構造体の開くファイルを閉じるとします。 SRV を再利用しようとする RDBSS\_オープンの構造と、サーバーとの接続なしデータ。 一部の Windows アプリケーションは、開き、読み取り、ファイルを閉じると、同じファイルを迅速に再度開くできます。 このような場合、SRV を再利用\_構造体の開くには、パフォーマンスが向上します。

終了、これらのデータ構造の最終処理し、メモリを解放するために使用する複数のルーチンまたは不要になったときに使用されるその他のリソースがあります。 これらのルーチンに[ **MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))、 [ **MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown)、 [ **MRxDeallocateForFcb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb)、 [ **MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx)、および[ **MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown)します。

次の表では、ファイル システム オブジェクトの作成と削除操作のため、ネットワーク ミニ リダイレクターで実装できるルーチンを示します。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkfcb_calldown" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkfcb_calldown)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>RDBSS は、FCB の 2 つのオブジェクトが同じファイルを表す場合は、ネットワークのミニ リダイレクターを照会するには、このルーチンを呼び出します。 別の名前 (MS-DOS の短い名前と例については、長い名前) がある同じにするファイルの 2 つの処理時にこのルーチン RDBSS 呼び出しが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトの拡張機能を閉じることを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_CLEANUP ファイル オブジェクトへの応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが SRV_OPEN オブジェクトを閉じることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが既存の SRV_OPEN に開いているファイル システムの要求を折りたたむことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトを作成することを要求するには、このルーチンを呼び出します。 この呼び出しは、受信、irp_mj_create 用への応答 RDBSS によって発行されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS は、FCB の割り当てを解除するネットワークのミニ リダイレクターを要求するには、このルーチンを呼び出します。 この呼び出しでは、ファイル システム オブジェクトを閉じる要求に応答します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS、FOBX の割り当てを解除するネットワークのミニ リダイレクターを要求するには、このルーチンを呼び出します。 この呼び出しでは、ファイル システム オブジェクトを閉じる要求に応答します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extendfile_calldown" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extendfile_calldown)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS では、ファイルはキャッシュ マネージャーによってキャッシュされているときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS では、キャッシュ マネージャーによって、ファイルがキャッシュされていないときに、ネットワークのミニ リダイレクターがファイルを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトをフラッシュすることを要求するには、このルーチンを呼び出します。 RDBSS では、受信、IRP_MJ_FLUSH_BUFFERS への応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターが終了を強制することを要求するには、このルーチンを呼び出します。 このルーチンは、SRV_OPEN の条件が適切でないか、SRV_OPEN がクローズとしてマークされるときに呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_is_lock_realizable" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_is_lock_realizable)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがこの NET_ROOT でバイト範囲ロックはサポートされているかどうかを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS は、RDBSS がお試しくださいし、既存のファイル システム オブジェクトに、オープンの要求を折りたたむかどうかにネットワークのミニ リダイレクターを示すことを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがファイル システム オブジェクトを切り捨てることを要求するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターがクリーンアップ時に 0 で、ファイルの入力ファイルのサイズが、FCB の有効なデータの長さより大きい場合、ファイル システム オブジェクトを拡張することを要求するには、このルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 





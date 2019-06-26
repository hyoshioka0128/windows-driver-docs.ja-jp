---
title: 接続とファイル制御ブロック管理ルーチン
description: 接続とファイル制御ブロック管理ルーチン
ms.assetid: e56c0cba-7352-4964-b067-57bc90c7f911
keywords:
- WDK RDBSS をブロックします。
- データ構造体の WDK ファイル システム
- RDBSS WDK ファイル システム、接続およびファイル構造
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、接続およびファイル構造
- 接続が WDK RDBSS 構造体します。
- ファイル構造 WDK RDBSS
- WDK RDBSS 構造体
- WDK RDBSS の接続情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414ed62521169f21b5ac1a06f9813c0912785e9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378977"
---
# <a name="connection-and-file-control-block-management-routines"></a>接続とファイル制御ブロック管理ルーチン


接続し、ファイル制御ブロック管理ルーチンは、接続およびファイル制御ブロックを表すために使用する構造の管理に RDBSS によって使用されます。

RDBSS は、接続とネットワーク ミニ リダイレクター ドライバーで使用できるファイル制御ブロックの管理を次のルーチンを提供します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfcb" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfcb)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化すると、し、この FCB が開かれる NET_ROOT 構造のインメモリ データ構造に新しい FCB 構造を挿入します。 割り当てられている構造体は、SRV_OPEN と FOBX 構造体の領域を持ちます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfobx" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfobx)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化し、新しいファイルのオブジェクトの拡張機能 (FOBX) 構造を挿入します。 ネットワークのミニ リダイレクターの最後に、FOBX を作成するには、このルーチンを呼び出す必要がありますが成功した操作を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetroot" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetroot)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造体を表すし、関連付けられているデバイス オブジェクト ネット名のテーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvcall" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvcall)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、サーバー呼び出しのコンテキストを表し、RDBSS によって保持されるネットワーク名のテーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvopen" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvopen)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化すると、し、RDBSS によって使用されるメモリ内データ構造に新しい SRV_OPEN 構造を挿入します。 新しい構造体を割り当てる必要がある場合、FOBX 構造用の領域があります。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatevnetroot" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatevnetroot)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、V_NET_ROOT 構造体を表すし、net 名前テーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>RDBSS で使用する参照カウントのデータ構造体のいくつかのインスタンスをこのルーチンに、参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizeconnection" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizeconnection)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、共有への接続を削除します。 Force が指定のレベルによっては、接続の開いているファイルが閉じられます。 ネットワークのミニ リダイレクターは、接続の終了を強制するいくつかのオプションが指定されていない場合、トランスポート接続をパフォーマンス上の理由から、開いたままにできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizenetfcb)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FCB 構造体を終了します。 呼び出し元に関連付けられたこの FCB NET_ROOT 構造に排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetfobx" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetfobx)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FOBX 構造体を終了します。 呼び出し元によっては、この FOBX に関連付けられている FCB の排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetroot" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetroot)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された NET_ROOT 構造体を終了します。 呼び出し元によっては、(を通じて SRV_CALL 構造) には、この NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルに排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvcall" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvcall)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_CALL 構造体を終了します。 呼び出し元によっては、この SRV_CALL 構造に関連付けられたデバイス オブジェクトの NetName テーブルにロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvopen" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvopen)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_OPEN 構造体を終了します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizevnetroot" data-raw-source="[&lt;strong&gt;RxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizevnetroot)"><strong>RxFinalizeVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された V_NET_ROOT 構造体を終了します。 呼び出し元によっては、この V_NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルでロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinishfcbinitialization" data-raw-source="[&lt;strong&gt;RxFinishFcbInitialization&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinishfcbinitialization)"><strong>RxFinishFcbInitialization</strong></a></p></td>
<td align="left"><p>このルーチンは、作成操作が正常に完了した後、FCB の初期化を完了してネットワーク ミニリダイレクターによって使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxforcefinalizeallvnetroots" data-raw-source="[&lt;strong&gt;RxForceFinalizeAllVNetRoots&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxforcefinalizeallvnetroots)"><strong>RxForceFinalizeAllVNetRoots</strong></a></p></td>
<td align="left"><p>この日常的な力は、指定された NET_ROOT 構造に関連付けられている V_NET_ROOT 構造体のすべてを終了します。 呼び出し元によっては、この V_NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルでロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxgetfilesizewithlock" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxgetfilesizewithlock)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB ヘッダーの 64 ビット値が一貫して読み込まれることを確認するロックを使用するファイルのサイズを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxinferfiletype" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxinferfiletype)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体のフィールドからのファイルの種類 (ディレクトリまたはディレクトリ以外) を推測を試みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlockenumerator" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlockenumerator)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>このルーチンは、ファイルの FCB のロックを列挙するために、ネットワーク ミニ リダイレクターから呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>この日常的な参照をデクリメント FCB を終了するとします。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降にのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferencenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferencenetfcb)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>FCB の参照カウントをこの日常的なデクリメント。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpreferencenetfcb" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpreferencenetfcb)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをインクリメントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxreference" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxreference)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS で使用されるデータの参照カウントの構造体のいくつかのインスタンスの参照カウントをインクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxsetsrvcalldomainname" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxsetsrvcalldomainname)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のサーバー (SRV_CALL 構造) に関連付けられているドメイン名を設定します。</p></td>
</tr>
</tbody>
</table>

 

多くのマクロも定義されてラッパーを提供する、 [ **RxReference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxreference)と[ **RxDeference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference)のルーチンデバッグします。 これらのマクロの詳細については、次を参照してください。[の診断およびデバッグ](diagnostics-and-debugging.md)します。

 

 





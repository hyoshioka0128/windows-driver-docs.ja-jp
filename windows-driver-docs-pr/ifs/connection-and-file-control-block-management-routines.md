---
title: 接続とファイル制御ブロック管理ルーチン
description: 接続とファイル制御ブロック管理ルーチン
ms.assetid: e56c0cba-7352-4964-b067-57bc90c7f911
keywords:
- WDK RDBSS をブロックする
- データ構造の WDK ファイルシステム
- RDBSS WDK ファイルシステム、接続およびファイル構造
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、接続とファイルの構造
- 接続構造 (WDK RDBSS)
- ファイル構造の WDK RDBSS
- 構造の WDK RDBSS
- 接続情報 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fe739accc0f2c9da4b0fa3ef55f62b7612c5d4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841464"
---
# <a name="connection-and-file-control-block-management-routines"></a>接続とファイル制御ブロック管理ルーチン


接続とファイル制御ブロックの管理ルーチンは、接続とファイル制御ブロックを表すために使用される構造を管理するために RDBSS によって使用されます。

RDBSS は、ネットワークミニリダイレクタードライバーで使用できる接続とファイル制御ブロックの管理について、次のルーチンを提供します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfcb" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfcb)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、この FCB が開かれている NET_ROOT 構造体のメモリ内データ構造に新しい FCB 構造体を割り当て、初期化し、挿入します。 割り当てられた構造体には、SRV_OPEN および FOBX 構造体の領域があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfobx" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfobx)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、新しいファイルオブジェクト拡張 (FOBX) 構造体を割り当て、初期化し、挿入します。 ネットワークミニリダイレクターは、このルーチンを呼び出して、作成操作が正常に終了した時点で FOBX を作成する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetroot" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetroot)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造体を表すノードを構築し、関連付けられているデバイスオブジェクトの NET name テーブルに名前を挿入します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvcall" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvcall)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、サーバー呼び出しコンテキストを表すノードを構築し、RDBSS によって管理される net name テーブルに名前を挿入します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvopen" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvopen)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS によって使用されるメモリ内データ構造に新しい SRV_OPEN 構造体を割り当て、初期化し、挿入します。 新しい構造体を割り当てる必要がある場合は、FOBX 構造体の領域があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatevnetroot" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatevnetroot)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、V_NET_ROOT 構造体を表すノードを構築し、その名前を NET name テーブルに挿入します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS によって使用されるいくつかの参照カウントデータ構造体のインスタンスの参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizeconnection" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizeconnection)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、共有への接続を削除します。 接続で開いたファイルは、指定された force レベルに応じて閉じられます。 ネットワークミニリダイレクターは、接続の終了を強制するオプションが指定されていない限り、トランスポート接続をパフォーマンス上の理由から開いたままにしておくことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizenetfcb)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FCB 構造体を終了します。 呼び出し元には、この FCB に関連付けられている NET_ROOT 構造体の排他ロックが必要です。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetfobx" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetfobx)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FOBX 構造体を終了します。 呼び出し元は、この FOBX に関連付けられた FCB に排他ロックを保持している必要があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetroot" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetroot)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された NET_ROOT 構造体を終了します。 呼び出し元には、この NET_ROOT 構造体に関連付けられているデバイスオブジェクトのネットテーブル (SRV_CALL 構造体を通じて) に排他ロックが設定されている必要があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvcall" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvcall)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_CALL 構造体を終了します。 呼び出し元には、この SRV_CALL 構造体に関連付けられているデバイスオブジェクトのネットテーブルのロックに対する排他アクセス権が必要です。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvopen" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvopen)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_OPEN 構造体を終了します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizevnetroot" data-raw-source="[&lt;strong&gt;RxFinalizeVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizevnetroot)"><strong>RxFinalizeVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された V_NET_ROOT 構造体を終了します。 呼び出し元には、この V_NET_ROOT 構造体に関連付けられているデバイスオブジェクトのネットテーブルのロックに対する排他アクセスが必要です。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinishfcbinitialization" data-raw-source="[&lt;strong&gt;RxFinishFcbInitialization&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinishfcbinitialization)"><strong>RxFinishFcbInitialization</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクターによる作成操作が正常に完了した後に、FCB の初期化を完了するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxforcefinalizeallvnetroots" data-raw-source="[&lt;strong&gt;RxForceFinalizeAllVNetRoots&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxforcefinalizeallvnetroots)"><strong>RxForceFinalizeAllVNetRoots</strong></a></p></td>
<td align="left"><p>このルーチンは、特定の NET_ROOT 構造体に関連付けられているすべての V_NET_ROOT 構造体を強制的に終了します。 呼び出し元には、この V_NET_ROOT 構造体に関連付けられているデバイスオブジェクトのネットテーブルのロックに対する排他アクセスが必要です。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxgetfilesizewithlock" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxgetfilesizewithlock)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>このルーチンは、64ビット値が一貫して読み取られるようにロックを使用して、FCB ヘッダー内のファイルサイズを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxinferfiletype" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxinferfiletype)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体のフィールドからファイルの種類 (ディレクトリまたはディレクトリ以外) を推論しようとします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlockenumerator" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlockenumerator)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB のファイルロックを列挙するために、ネットワークミニリダイレクターから呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>このルーチンは、参照カウントをデクリメントし、FCB を終了します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferencenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferencenetfcb)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpreferencenetfcb" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpreferencenetfcb)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをインクリメントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS によって使用されるいくつかの参照カウントデータ構造体のインスタンスの参照カウントをインクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxsetsrvcalldomainname" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxsetsrvcalldomainname)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のサーバー (SRV_CALL 構造) に関連付けられているドメイン名を設定します。</p></td>
</tr>
</tbody>
</table>

 

デバッグのために[**RxReference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference)ルーチンと[**RxDeference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)ルーチンのラッパーを提供する多くのマクロも定義されていることに注意してください。 これらのマクロの詳細については、「[診断とデバッグ](diagnostics-and-debugging.md)」を参照してください。

 

 





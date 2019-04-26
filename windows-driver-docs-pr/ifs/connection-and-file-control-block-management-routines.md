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
ms.openlocfilehash: 33b9241ada099d4a45015a829de53e679116eed5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351436"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554356" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554356)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化すると、し、この FCB が開かれる NET_ROOT 構造のインメモリ データ構造に新しい FCB 構造を挿入します。 割り当てられている構造体は、SRV_OPEN と FOBX 構造体の領域を持ちます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554358" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554358)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化し、新しいファイルのオブジェクトの拡張機能 (FOBX) 構造を挿入します。 ネットワークのミニ リダイレクターの最後に、FOBX を作成するには、このルーチンを呼び出す必要がありますが成功した操作を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554366" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554366)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造体を表すし、関連付けられているデバイス オブジェクト ネット名のテーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554370" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554370)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、サーバー呼び出しのコンテキストを表し、RDBSS によって保持されるネットワーク名のテーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554376" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554376)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化すると、し、RDBSS によって使用されるメモリ内データ構造に新しい SRV_OPEN 構造を挿入します。 新しい構造体を割り当てる必要がある場合、FOBX 構造用の領域があります。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554380" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554380)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、V_NET_ROOT 構造体を表すし、net 名前テーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554388" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554388)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>RDBSS で使用する参照カウントのデータ構造体のいくつかのインスタンスをこのルーチンに、参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554409" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554409)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、共有への接続を削除します。 Force が指定のレベルによっては、接続の開いているファイルが閉じられます。 ネットワークのミニ リダイレクターは、接続の終了を強制するいくつかのオプションが指定されていない場合、トランスポート接続をパフォーマンス上の理由から、開いたままにできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554412" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554412)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FCB 構造体を終了します。 呼び出し元に関連付けられたこの FCB NET_ROOT 構造に排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554418" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554418)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FOBX 構造体を終了します。 呼び出し元によっては、この FOBX に関連付けられている FCB の排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554421" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554421)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された NET_ROOT 構造体を終了します。 呼び出し元によっては、(を通じて SRV_CALL 構造) には、この NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルに排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554426" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554426)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_CALL 構造体を終了します。 呼び出し元によっては、この SRV_CALL 構造に関連付けられたデバイス オブジェクトの NetName テーブルにロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554432" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554432)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_OPEN 構造体を終了します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554450" data-raw-source="[&lt;strong&gt;RxFinalizeVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554450)"><strong>RxFinalizeVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された V_NET_ROOT 構造体を終了します。 呼び出し元によっては、この V_NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルでロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554454" data-raw-source="[&lt;strong&gt;RxFinishFcbInitialization&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554454)"><strong>RxFinishFcbInitialization</strong></a></p></td>
<td align="left"><p>このルーチンは、作成操作が正常に完了した後、FCB の初期化を完了してネットワーク ミニリダイレクターによって使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554463" data-raw-source="[&lt;strong&gt;RxForceFinalizeAllVNetRoots&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554463)"><strong>RxForceFinalizeAllVNetRoots</strong></a></p></td>
<td align="left"><p>この日常的な力は、指定された NET_ROOT 構造に関連付けられている V_NET_ROOT 構造体のすべてを終了します。 呼び出し元によっては、この V_NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルでロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554478" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554478)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB ヘッダーの 64 ビット値が一貫して読み込まれることを確認するロックを使用するファイルのサイズを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554493" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554493)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体のフィールドからのファイルの種類 (ディレクトリまたはディレクトリ以外) を推測を試みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554511" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554511)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>このルーチンは、ファイルの FCB のロックを列挙するために、ネットワーク ミニ リダイレクターから呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff554603" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554603)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>この日常的な参照をデクリメント FCB を終了するとします。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降にのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554608" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554608)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>FCB の参照カウントをこの日常的なデクリメント。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554627" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554627)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをインクリメントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554688" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554688)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS で使用されるデータの参照カウントの構造体のいくつかのインスタンスの参照カウントをインクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554728" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554728)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のサーバー (SRV_CALL 構造) に関連付けられているドメイン名を設定します。</p></td>
</tr>
</tbody>
</table>

 

多くのマクロも定義されてラッパーを提供する、 [ **RxReference** ](https://msdn.microsoft.com/library/windows/hardware/ff554688)と[ **RxDeference** ](https://msdn.microsoft.com/library/windows/hardware/ff554388)のルーチンデバッグします。 これらのマクロの詳細については、次を参照してください。[の診断およびデバッグ](diagnostics-and-debugging.md)します。

 

 





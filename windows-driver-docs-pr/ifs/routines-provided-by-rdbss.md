---
title: RDBSS が提供するルーチン
description: RDBSS が提供するルーチン
ms.assetid: 37631760-ac89-4ef0-ad7c-ed3e68aa1ceb
keywords:
- RDBSS WDK ファイル システム、ルーチン
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、ルーチン
- WDK RDBSS ルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789f2bc6b3365c2d39ce547ce2b95aaa841ce6e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380022"
---
# <a name="routines-provided-by-rdbss"></a>RDBSS が提供するルーチン


## <span id="ddk_functions_provided_by_rdbss_if"></span><span id="DDK_FUNCTIONS_PROVIDED_BY_RDBSS_IF"></span>


次のルーチンは、RDBSS によってエクスポートされます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このリソースの取得のルーチンでは、排他モードでのファイル制御ブロック (FCB) リソースを取得します。 このルーチンは無料になるため、リソースが取得されるまでこのルーチンは制御を返しません FCB リソース待機します。 このルーチンは、この FCB に関連付けられている RX_CONTEXT が取り消された場合でも、FCB のリソースを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このリソースの取得のルーチンでは、共有モードで FCB のリソースを取得します。 このルーチンは、FCB のリソースを排他的に取得された以前の場合は、空きリソースが取得されるまでこのルーチンは制御を返しませんして待機します。 このルーチンは、この FCB に関連付けられている RX_CONTEXT が取り消された場合でも、FCB のリソースを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>このリソースの取得のルーチンでは、共有モードで FCB のリソースを取得します。 このルーチンは FCB リソースが排他的に取得した場合、解放を待機します。 このルーチンでは、リソースが取得されるまで、コントロールは返されません。 このルーチンは、この FCB に関連付けられている RX_CONTEXT が取り消された場合でも、FCB のリソースを取得します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降にのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>このルーチンは、assert 文字列 RDBSS チェックがインストールされている場合、カーネル デバッガーにビルドを送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された非透過のコンテキストで、使用可能な multiplex ID (MID) MID_ATLAS データ構造体からを関連付けます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxcanceltimerrequest" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxcanceltimerrequest)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、タイマーの要求をキャンセルします。 要求をキャンセルするのには、ルーチンとコンテキストによって識別されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceallocateirpwithmdl" data-raw-source="[&lt;strong&gt;RxCeAllocateIrpWithMDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceallocateirpwithmdl)"><strong>RxCeAllocateIrpWithMDL</strong></a></p></td>
<td align="left"><p>このルーチンは IRP を使用するため接続エンジンによって割り当てし、MDL を IRP に関連付けます。</p>
<p>このルーチンでは、Windows XP でのみです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildaddress" data-raw-source="[&lt;strong&gt;RxCeBuildAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildaddress)"><strong>RxCeBuildAddress</strong></a></p></td>
<td align="left"><p>このルーチンは、トランスポート バインディングを使用したトランスポート アドレスを関連付けます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildconnection" data-raw-source="[&lt;strong&gt;RxCeBuildConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildconnection)"><strong>RxCeBuildConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、ローカル RDBSS 接続アドレスと、特定のリモート アドレス間の接続を確立します。 システムのワーカー スレッドのコンテキストでは、このルーチンを呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildconnectionovermultipletransports" data-raw-source="[&lt;strong&gt;RxCeBuildConnectionOverMultipleTransports&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildconnectionovermultipletransports)"><strong>RxCeBuildConnectionOverMultipleTransports</strong></a></p></td>
<td align="left"><p>このルーチンは、ローカル RDBSS 接続アドレスと、特定のリモート アドレスの間の接続を確立し、複数のトランスポートをサポートします。 一連のローカル アドレスを指定し、このルーチンは、すべてのローカル アドレスに関連付けられたトランスポートを使用して、ターゲット サーバーに接続を試行します。 1 つの接続は、接続オプションに応じて優勝者として選択されます。 このルーチンは、システム ワーカー スレッドのコンテキストで呼び出される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildtransport" data-raw-source="[&lt;strong&gt;RxCeBuildTransport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildtransport)"><strong>RxCeBuildTransport</strong></a></p></td>
<td align="left"><p>このルーチンは、指定したトランスポートの名前に、RDBSS トランスポートをバインドします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildvc" data-raw-source="[&lt;strong&gt;RxCeBuildVC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcebuildvc)"><strong>RxCeBuildVC</strong></a></p></td>
<td align="left"><p>このルーチンは、指定した接続に仮想回線を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcecancelconnectrequest" data-raw-source="[&lt;strong&gt;RxCeCancelConnectRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcecancelconnectrequest)"><strong>RxCeCancelConnectRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、以前に発行された接続要求をキャンセルします。</p>
<p>このルーチンが現在実装されていないことに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcefreeirp" data-raw-source="[&lt;strong&gt;RxCeFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcefreeirp)"><strong>RxCeFreeIrp</strong></a></p></td>
<td align="left"><p>このルーチンは、接続のエンジンによって使用される IRP を解放します。</p>
<p>このルーチンでは、Windows XP でのみです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceinitiatevcdisconnect" data-raw-source="[&lt;strong&gt;RxCeInitiateVCDisconnect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceinitiatevcdisconnect)"><strong>RxCeInitiateVCDisconnect</strong></a></p></td>
<td align="left"><p>このルーチンは、仮想回線で接続が切断を開始します。 このルーチンは、システム ワーカー スレッドのコンテキストで呼び出される必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequeryadapterstatus" data-raw-source="[&lt;strong&gt;RxCeQueryAdapterStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequeryadapterstatus)"><strong>RxCeQueryAdapterStatus</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のトランスポートの ADAPTER_STATUS 構造を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequeryinformation" data-raw-source="[&lt;strong&gt;RxCeQueryInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequeryinformation)"><strong>RxCeQueryInformation</strong></a></p></td>
<td align="left"><p>指定した仮想回線に関する情報を日常的なクエリがこのです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequerytransportinformation" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequerytransportinformation)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のトランスポートの接続の数とサービスの品質に関する情報を照会します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcesend" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcesend)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>このルーチンは、仮想回線で接続を指定した方向トランスポートのサービスのデータ ユニット (TSDU) を送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcesenddatagram" data-raw-source="[&lt;strong&gt;RxCeSendDatagram&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcesenddatagram)"><strong>RxCeSendDatagram</strong></a></p></td>
<td align="left"><p>このルーチンでは、指定したトランスポート アドレスを TSDU を送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardownaddress" data-raw-source="[&lt;strong&gt;RxCeTearDownAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardownaddress)"><strong>RxCeTearDownAddress</strong></a></p></td>
<td align="left"><p>このルーチンは、トランスポート バインドからトランスポート アドレスを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardownconnection" data-raw-source="[&lt;strong&gt;RxCeTearDownConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardownconnection)"><strong>RxCeTearDownConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、特定の接続を破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardowntransport" data-raw-source="[&lt;strong&gt;RxCeTearDownTransport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardowntransport)"><strong>RxCeTearDownTransport</strong></a></p></td>
<td align="left"><p>このルーチンは、指定されたトランスポートからバインド解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardownvc" data-raw-source="[&lt;strong&gt;RxCeTearDownVC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxceteardownvc)"><strong>RxCeTearDownVC</strong></a></p></td>
<td align="left"><p>このルーチンは、仮想接続を破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxchangebufferingstate" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxchangebufferingstate)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンは、バッファリング状態の変更要求の処理に呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体に関連付けられている IRP の完了に使用されます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest_real" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest_real)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体に関連付けられている IRP の完了に使用されます。 このルーチンは、ネットワークのミニ リダイレクターによって使用する必要がありますされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンでは、MID_ATLAS データ構造体の新しいインスタンス、それを初期化します。 RDBSS では、すべての接続で同時にアクティブな要求の間 (ミニリダイレクター) のネットワーク クライアントとサーバーの両方を識別する手段として、このデータ構造体で定義されている multiplex ID (MID) を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfcb" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfcb)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化すると、し、この FCB の開いている NET_ROOT 構造のインメモリ データ構造に新しい FCB 構造を挿入します。 割り当てられている構造体は、SRV_OPEN と FOBX 構造体の領域を持ちます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfobx" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetfobx)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化し、新しいファイルのオブジェクトの拡張機能 (FOBX) 構造を挿入します。 ネットワークのミニ リダイレクターの最後に、FOBX を作成するには、このルーチンを呼び出す必要がありますが成功した操作を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetroot" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatenetroot)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは NET_ROOT 構造体を表すノードをビルドし、名前を関連付けられているデバイスのオブジェクトで net 名前テーブルに挿入します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxcreaterxcontext" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxcreaterxcontext)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>このルーチンでは、新しい RX_CONTEXT 構造、データ構造体を初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvcall" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvcall)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、サーバー呼び出しのコンテキストを表し、RDBSS によって保持されるネットワーク名のテーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvopen" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatesrvopen)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、割り当て、初期化すると、し、RDBSS によって使用されるメモリ内データ構造に新しい SRV_OPEN 構造を挿入します。 新しい構造に割り当てられる場合は、FOBX 構造体の領域があります。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatevnetroot" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxcreatevnetroot)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、V_NET_ROOT 構造体を表すし、net 名前テーブルに名前を挿入するノードを構築します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>このルーチンは、インストールされている場合は、カーネル デバッガーによって処理される例外を発生させます。それ以外の場合、デバッグ、システムによって処理されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdereference)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>RDBSS で使用する参照カウントのデータ構造体のいくつかのインスタンスをこのルーチンに、参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>このルーチンは RX_CONTEXT 構造体を逆参照し、参照カウントがゼロにする場合の割り当てを解除し、RDBSS インメモリ データ構造体から指定した RX_CONTEXT 構造を削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンは MID_ATLAS データ構造体の既存のインスタンスを破棄し、割り当てられたメモリを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxworkq/nf-rxworkq-rxdispatchtoworkerthread" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxworkq/nf-rxworkq-rxdispatchtoworkerthread)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカー スレッドのコンテキスト内のルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdriverentry" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdriverentry)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>このルーチンからモノリシック ネットワーク ミニ リダイレクター ドライバーによって呼び出されます。 その<strong>DriverEntry</strong> RDBSS を初期化します。</p>
<p>モノリシック以外のドライバーの初期化ルーチンは等しく、 <strong>DriverEntry</strong>の日常的な<em>rdbss.sys</em>デバイス ドライバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizeconnection" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizeconnection)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、共有への接続を削除します。 Force が指定のレベルによっては、接続の開いているファイルが閉じられます。 ネットワークのミニ リダイレクターは、接続の終了を強制するいくつかのオプションが指定されていない場合、トランスポート接続をパフォーマンス上の理由から、開いたままにできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfinalizenetfcb)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FCB 構造体を終了します。 呼び出し元に関連付けられた FCB NET_ROOT 構造に排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetfobx" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetfobx)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FOBX 構造体を終了します。 呼び出し元によっては、この FOBX に関連付けられている FCB の排他ロックが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetroot" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizenetroot)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された NET_ROOT 構造体を終了します。 呼び出し元 (SRV_CALL 構造) を通じてこの NET_ROOT 構造に関連付けられたデバイス オブジェクトの NetName テーブルでロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvcall" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvcall)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_CALL 構造体を終了します。 呼び出し元によっては、この SRV_CALL 構造に関連付けられたデバイス オブジェクトの NetName テーブルにロックへの排他アクセスが必要です。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvopen" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxfinalizesrvopen)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_OPEN 構造体を終了します。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxfsddispatch" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxfsddispatch)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O 要求パケット (IRP) を処理する RDBSS のファイル システム ドライバー (FSD) ディスパッチを実装します。 このルーチンは、要求の RDBSS 処理を開始するためにドライバー ディスパッチ ルーチンで、ネットワーク ミニ リダイレクターによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfsdpostrequest" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxfsdpostrequest)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>このルーチンはキュー、ファイル システムのプロセス (FSP) して処理するためのワーカー キューに RX_CONTEXT 構造体で指定された I/O 要求パケット (IRP) です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxgetfilesizewithlock" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxgetfilesizewithlock)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>このルーチンは、64 ビット値が一貫して読み込まれることを確認するロックを使用する FCB 構造から、ファイルのサイズを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxgetrdbssprocess" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxgetrdbssprocess)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS カーネルのプロセスによって使用されるメイン スレッドのプロセスにポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンはバッファリング状態変更要求 (oplock 中断を示す値、たとえば) 後で処理するための登録と呼ばれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンはバッファリング状態変更要求 (oplock 中断を示す値、たとえば) 後で処理するための登録と呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxinferfiletype" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxinferfiletype)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>このルーチンを推論しようファイルの種類 (ディレクトリまたは非ディレクトリ) から、 <strong>CreateOptions</strong> ( <strong>Create.NtCreateParameters.CreateOptions</strong>) RX_CONTEXT 構造体のフィールド。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxinitializecontext" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxinitializecontext)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>このルーチンでは、新しく割り当てられた RX_CONTEXT 構造体を初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxisthisacscagentopen" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxisthisacscagentopen)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、開いているファイルがユーザー モードのクライアント側キャッシュ エージェントによって行われたかどうかを決定します。</p>
<p>このルーチンは、Windows Server 2003 にできるだけです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlockenumerator" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlockenumerator)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>このルーチンは、ファイルの FCB のロックを列挙するために、ネットワーク ミニ リダイレクターから呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O エラー ログにエラーをログに呼び出されます。 推奨されます、 <strong>RxLogEvent</strong>または<strong>RxLogFailure</strong>このルーチンを直接呼び出す代わりにマクロを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventwithannotation" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventwithannotation)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>このルーチンは、エラー ログの I/O 構造体を割り当て、ログの構造を設定し、I/O エラーのログにこの構造体を書き込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O エラー ログにエラーをログに呼び出されます。 このルーチンは、I/O エラーのログの構造に格納されているデータのバッファーに行番号と状態をエンコードします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiocompletion" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiocompletion)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>このルーチンはルーチンは最初に保留中返された場合、処理が完了するととき、ネットワーク ミニ リダイレクター ドライバーの低い I/O ルーチンによって呼び出される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiogetbufferaddress" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiogetbufferaddress)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>このルーチンから MDL に対応するバッファーを返します、 <strong>LowIoContext</strong> RX_CONTEXT 構造体の構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxmakelatedeviceavailable" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxmakelatedeviceavailable)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>このルーチンは、"遅延"デバイスのデバイス オブジェクトを変更します。 使用可能な。 遅延のデバイスは、いずれかのドライバーの読み込みルーチンでは作成されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS データ構造に関連付けられているそのコンテキストに、MID をマップし、コンテキストから MID の関連付けを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を MID_ATLAS データ構造に関連付けられているそのコンテキストにマップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxmapsystembuffer" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxmapsystembuffer)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O 要求パケット (IRP) からシステムのバッファーのアドレスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheactivateentry" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheactivateentry)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、名のキャッシュ エントリを取得し、有効期限の時間とネットワーク ミニリダイレクター コンテキストを更新します。 アクティブ リストのエントリが置かれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecheckentry" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecheckentry)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、有効性を NAME_CACHE エントリを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecreateentry" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachecreateentry)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>このルーチンでは、割り当て、指定した名前の文字列を含む NAME_CACHE 構造体を初期化します。 呼び出し元が名前のキャッシュ コンテキストの追加のネットワーク ミニリダイレクター要素を初期化し、名前キャッシュ アクティブ リストにエントリを配置が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentry" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentry)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、フリー リストに NAME_CACHE エントリを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentrywithshortname" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheexpireentrywithshortname)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>このルーチンでは、すべて名前プレフィックスには、指定した短いファイル名が一致する NAME_CACHE エントリの有効期限です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefetchentry" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefetchentry)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリの指定した名前の文字列での一致を検索します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefinalize" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefinalize)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE_CONTROL 構造に関連付けられた NAME_CACHE エントリのすべての記憶域を解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefreeentry" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecachefreeentry)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>このルーチンは NAME_CACHE エントリの記憶域を解放し、デクリメント NAME_CACHE_CONTROL 構造に関連付けられているエントリをキャッシュする NAME_CACHE の数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheinitialize" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/namcache/nf-namcache-rxnamecacheinitialize)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>このルーチンは NAME_CACHE 構造体を初期化し、NAME_CACHE_CONTROL 構造で関連付けます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、低い I/O に使用されるユーザー バッファーのアドレスを返します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockexclusive" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockexclusive)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>このルーチンは、カタログ SRV_CALL と NET_ROOT 名に使用されるプレフィックス テーブルに対する排他ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockshared" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpacquireprefixtablelockshared)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>このルーチンは、カタログ SRV_CALL と NET_ROOT 名に使用されるプレフィックス テーブルに対する共有ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>このルーチンは、参照カウントを逆参照し、FCB を終了します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降にのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferencenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpdereferencenetfcb)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>FCB の参照カウントをこの日常的なデクリメント。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostoneshottimerrequest" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostoneshottimerrequest)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、1 回限りのタイマー要求を初期化するために、ドライバーによって使用されます。 このルーチンに渡されるワーカー スレッド ルーチンは、タイマーが期限切れにすると呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンを使用して、定期的なタイマー要求を初期化します。 このルーチンに渡されるワーカー スレッド ルーチンが一定の間隔と呼ばれるこのルーチンへの入力パラメーターに基づいた繰り返しタイマーが起動されるときにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxworkq/nf-rxworkq-rxposttoworkerthread" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxworkq/nf-rxworkq-rxposttoworkerthread)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカー スレッドのコンテキストでルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpreferencenetfcb" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxpreferencenetfcb)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをインクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxprefixtablelookupname)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>ルーチンは、カタログ SRV_CALL に使用されるプレフィックスのテーブルの名前と NET_ROOT 名を検索し、基になるポインターから、包含構造体に変換します。</p>
<p>このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpreleaseprefixtablelock" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prefix/nf-prefix-rxpreleaseprefixtablelock)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>このルーチンは、カタログ SRV_CALL と NET_ROOT 名に使用されるプレフィックス テーブルのロックを解放します。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクター ドライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxpreparecontextforreuse" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxpreparecontextforreuse)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>このルーチンは、すべての操作に固有の割り当てと行われた買収をリセットして再利用するため、RX_CONTEXT 構造を準備します。 IRP から得られるパラメーターは変更されません。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>このルーチンは、再解析を容易にするために、ファイル オブジェクトの名前を設定します。 このルーチンは、シンボリック リンクを通過するネットワークのミニ リダイレクターによって使用されます。 このルーチンは RDBSS によって内部的に使用され、ネットワークのミニ リダイレクターは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackdereference" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackdereference)"><strong>RxpTrackDereference</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX FCB、逆参照する要求を追跡するために使用し、チェックで SRV_OPEN 構造を構築します。 これらのログの要求を逆参照のログ記録システムと WMI によってアクセスできます。</p>
<p>製品版ビルドでは、このルーチンは何もしません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackreference" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fcb/nf-fcb-rxptrackreference)"><strong>RxpTrackReference</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX FCB を参照する要求を追跡するために使用し、チェックで SRV_OPEN 構造を構築します。 これらの参照要求のログは、ログ記録システムおよび WMI でアクセスできます。</p>
<p>製品版ビルドでは、このルーチンは何もしません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>ルーチンは、RDBSS でドライバーを登録解除 RDBSS 登録の内部テーブルから登録情報を削除するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpurgeallfobxs" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxpurgeallfobxs)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークのミニ リダイレクターに関連付けられているすべての FOBX 構造を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxpurgerelatedfobxs" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxpurgerelatedfobxs)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造に関連付けられている FOBX 構造体のすべてを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>このルーチンは、代替のコンテキストで、MID を再関連付けします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxreference" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxreference)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS で使用されるデータの参照カウントの構造体のいくつかのインスタンスの参照カウントをインクリメントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS で、内部の登録の表に、登録情報を追加、ドライバーに登録するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。 RDBSS もネットワーク ミニリダイレクターのデバイス オブジェクトを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンを使用して取得 FCB のリソースを解放する<strong>RxAcquireExclusiveFcbResourceInMRx</strong>または<strong>RxAcquireSharedFcbResourceInMRx</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>このルーチンを使用して取得 FCB のリソースを解放する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"> <strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降にのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>このルーチンは、シリアル化されたブロッキング I/O キューに存在する場合、次の待機スレッドをウェイクします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxscavengeallfobxs" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxscavengeallfobxs)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のネットワークのミニ リダイレクター デバイス オブジェクトに関連付けられた FOBX 構造体のすべてを清掃です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxscavengefobxsfornetroot" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scavengr/nf-scavengr-rxscavengefobxsfornetroot)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは清掃 NET_ROOT の指定された構造体に関連する FOBX 構造体のすべてです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxsetdomainformailslotbroadcast" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>このルーチンは、メール スロットがドライバーによってサポートされている場合は、"メール スロット"ブロードキャストに使用するドメインを設定するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体にネットワーク ミニリダイレクター キャンセル ルーチンを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxsetsrvcalldomainname" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxsetsrvcalldomainname)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のサーバー (SRV_CALL 構造) に関連付けられているドメイン名を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxworkq/nf-rxworkq-rxspindownmrxdispatcher" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxworkq/nf-rxworkq-rxspindownmrxdispatcher)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>このルーチンのネットワークのミニ リダイレクター ディスパッチャー コンテキストを廃棄します。</p>
<p>このルーチンは、Windows XP で以降のみです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、自身を登録するために呼び出さネットワーク ・ mini-リダイレクターを開始します。 ドライバーを UNC 名のサポートを示している場合 RDBSS は汎用名前付け規則 (UNC) プロバイダーの複数 UNC プロバイダー (MUP) としてもネットワーク ミニ リダイレクター ドライバーを登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークのミニ リダイレクター ドライバーを停止します。 停止しているドライバーは新しいコマンドを使用できなくなります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、インライン関数で定義されている<em>rxstruc.h</em> RDBSS でドライバーを登録解除 RDBSS 登録の内部テーブルから登録情報を削除するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。 <strong>RxUnregisterMinirdr</strong>インライン関数を内部的に呼び出します<strong>RxpUnregisterMinirdr</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリの問題のインスタンスを検出するときに使用できるブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。</p>
<p>推奨されます、 <strong>RxAllocatePoolWithTag</strong>このルーチンを直接呼び出す代わりにマクロを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>このルーチンは、特別な RX_POOL_HEADER ヘッダーの署名のメモリ ブロックを確認します。 ルーチンを使用するには、ネットワークのミニ リダイレクター ドライバーはメモリにこの特別な署名ブロックを追加する必要がありますので注意が割り当てられます。</p>
<p>この特殊なヘッダー ブロックが実装されていないために、このルーチンを使用しない必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリ プールを解放します。</p>
<p>推奨されます、 <strong>RxFreePool</strong>このルーチンを直接呼び出す代わりにマクロを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>このルーチンは、パラメーターの形式の文字列と変数の数を受け取るし、I/O エラーのログ エントリのログ記録する場合は、有効になっている structureing の出力文字列を書式設定します。</p>
<p>推奨されます、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxlog/nf-rxlog-_rxlog)"> <strong>RxLog</strong> </a>このルーチンを直接呼び出す代わりにマクロを使用します。</p>
<p>このルーチンでは、Windows Server 2003、Windows XP、および Windows 2000 RDBSS のチェック ビルドで使用できるのみです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、高速な I/O ディスパッチ ベクトル通常のディスパッチ I/O ベクターと一致するように入力し、渡されるデバイス オブジェクトに関連付けられているドライバー オブジェクトにインストールします。</p>
<p>このルーチンは、モノリシックではないドライバーに対してだけは実装され、モノリシックなドライバーは何もしません。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>このルーチンは、同じ作業キューにブロッキング I/O を同期に使用されます。 このルーチンが、名前付きパイプ操作を同期する RDBSS によって内部的に使用されます。 このルーチンは、ネットワーク ミニリダイレクターによって保持されている別のキューに対する操作を同期するネットワークのミニ リダイレクターを使用できます。</p>
<p>このルーチンは、Windows Server 2003 にできるだけです。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>このルーチンは、同じ作業キューにブロッキング I/O を同期に使用されます。 このルーチンが、名前付きパイプ操作を同期する RDBSS によって内部的に使用されます。 このルーチンは、ネットワーク ミニリダイレクターによって保持されている別のキューに対する操作を同期するネットワークのミニ リダイレクターを使用できます。</p>
<p>このルーチンは、Windows XP および Windows 2000 にできるだけです。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: RDBSS が提供するルーチン
description: RDBSS が提供するルーチン
ms.assetid: 37631760-ac89-4ef0-ad7c-ed3e68aa1ceb
keywords:
- RDBSS WDK ファイルシステム、ルーチン
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、ルーチン
- ルーチン WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c861353def68ec082281153b17aa26ddf4e6ca35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840978"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このリソース取得ルーチンは、排他モードでファイル制御ブロック (FCB) リソースを取得します。 このルーチンは、FCB リソースが解放されるのを待機します。そのため、このルーチンはリソースが取得されるまで制御を返しません。 このようなルーチンは、この FCB に関連付けられている RX_CONTEXT がキャンセルされた場合でも、FCB リソースを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このリソース取得ルーチンは、共有モードで FCB リソースを取得します。 このルーチンは、既に排他的に取得されている場合、FCB リソースが解放されるのを待機します。そのため、このルーチンはリソースが取得されるまで制御を返しません。 このようなルーチンは、この FCB に関連付けられている RX_CONTEXT がキャンセルされた場合でも、FCB リソースを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>このリソース取得ルーチンは、共有モードで FCB リソースを取得します。 このルーチンは、以前に排他的に取得された FCB リソースが解放されるまで待機します。 このルーチンは、リソースが取得されるまで制御を返しません。 このようなルーチンは、この FCB に関連付けられている RX_CONTEXT がキャンセルされた場合でも、FCB リソースを取得します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS checked ビルドでアサート文字列をカーネルデバッガーに送信します (インストールされている場合)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された不透明なコンテキストを、MID_ATLAS データ構造体の使用可能な多重 ID (MID) に関連付けます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、タイマー要求をキャンセルします。 キャンセルされる要求は、ルーチンとコンテキストによって識別されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceallocateirpwithmdl" data-raw-source="[&lt;strong&gt;RxCeAllocateIrpWithMDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceallocateirpwithmdl)"><strong>RxCeAllocateIrpWithMDL</strong></a></p></td>
<td align="left"><p>このルーチンは、接続エンジンによって使用される IRP を割り当て、MDL を IRP に関連付けます。</p>
<p>このルーチンは、Windows XP でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildaddress" data-raw-source="[&lt;strong&gt;RxCeBuildAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildaddress)"><strong>RxCeBuildAddress</strong></a></p></td>
<td align="left"><p>このルーチンは、トランスポートアドレスをトランスポートバインドに関連付けます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnection" data-raw-source="[&lt;strong&gt;RxCeBuildConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnection)"><strong>RxCeBuildConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、ローカルの RDBSS 接続アドレスと指定されたリモートアドレスとの間の接続を確立します。 このルーチンは、システムワーカースレッドのコンテキストで呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnectionovermultipletransports" data-raw-source="[&lt;strong&gt;RxCeBuildConnectionOverMultipleTransports&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnectionovermultipletransports)"><strong>RxCeBuildConnectionOverMultipleTransports</strong></a></p></td>
<td align="left"><p>このルーチンは、ローカルの RDBSS 接続アドレスと指定されたリモートアドレスとの間の接続を確立し、複数のトランスポートをサポートします。 ローカルアドレスのセットが指定され、このルーチンは、ローカルアドレスに関連付けられているすべてのトランスポートを使用して対象サーバーに接続しようとします。 接続オプションに応じて、1つの接続が勝者として選択されます。 このルーチンは、システムワーカースレッドのコンテキストで呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildtransport" data-raw-source="[&lt;strong&gt;RxCeBuildTransport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildtransport)"><strong>RxCeBuildTransport</strong></a></p></td>
<td align="left"><p>このルーチンは、指定されたトランスポート名に RDBSS transport をバインドします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildvc" data-raw-source="[&lt;strong&gt;RxCeBuildVC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildvc)"><strong>RxCeBuildVC</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された接続に仮想回線を追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcecancelconnectrequest" data-raw-source="[&lt;strong&gt;RxCeCancelConnectRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcecancelconnectrequest)"><strong>RxCeCancelConnectRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、以前に発行された接続要求をキャンセルします。</p>
<p>このルーチンは現在実装されていないことに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcefreeirp" data-raw-source="[&lt;strong&gt;RxCeFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcefreeirp)"><strong>RxCeFreeIrp</strong></a></p></td>
<td align="left"><p>このルーチンは、接続エンジンによって使用される IRP を解放します。</p>
<p>このルーチンは、Windows XP でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceinitiatevcdisconnect" data-raw-source="[&lt;strong&gt;RxCeInitiateVCDisconnect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceinitiatevcdisconnect)"><strong>RxCeInitiateVCDisconnect</strong></a></p></td>
<td align="left"><p>このルーチンは、仮想回線で切断を開始します。 このルーチンは、システムワーカースレッドのコンテキストで呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryadapterstatus" data-raw-source="[&lt;strong&gt;RxCeQueryAdapterStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryadapterstatus)"><strong>RxCeQueryAdapterStatus</strong></a></p></td>
<td align="left"><p>このルーチンは、指定されたトランスポートの ADAPTER_STATUS 構造体を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryinformation" data-raw-source="[&lt;strong&gt;RxCeQueryInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryinformation)"><strong>RxCeQueryInformation</strong></a></p></td>
<td align="left"><p>このルーチンは、特定の仮想回線に関する情報を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のトランスポートに対して、サービスの接続数と品質に関する情報を照会します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された接続に沿ったトランスポートサービスデータユニット (TSDU) を仮想回線に送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesenddatagram" data-raw-source="[&lt;strong&gt;RxCeSendDatagram&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesenddatagram)"><strong>RxCeSendDatagram</strong></a></p></td>
<td align="left"><p>このルーチンは、指定されたトランスポートアドレスに TSDU を送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownaddress" data-raw-source="[&lt;strong&gt;RxCeTearDownAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownaddress)"><strong>RxCeTearDownAddress</strong></a></p></td>
<td align="left"><p>このルーチンは、トランスポートバインドからトランスポートアドレスを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownconnection" data-raw-source="[&lt;strong&gt;RxCeTearDownConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownconnection)"><strong>RxCeTearDownConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、特定の接続を破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardowntransport" data-raw-source="[&lt;strong&gt;RxCeTearDownTransport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardowntransport)"><strong>RxCeTearDownTransport</strong></a></p></td>
<td align="left"><p>このルーチンは、指定されたトランスポートからバインドを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownvc" data-raw-source="[&lt;strong&gt;RxCeTearDownVC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownvc)"><strong>RxCeTearDownVC</strong></a></p></td>
<td align="left"><p>このルーチンは、仮想接続を破棄します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンは、バッファリング状態の変更要求を処理するために呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造に関連付けられている IRP を完了するために使用されます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造に関連付けられている IRP を完了するために使用されます。 このルーチンは、ネットワークミニリダイレクターでは使用しないでください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS データ構造体の新しいインスタンスを割り当て、それを初期化します。 RDBSS は、このデータ構造で定義されている多重 ID (MID) を使用します。これは、ネットワーククライアント (ミニリダイレクター) とサーバーの両方が、任意の接続で同時にアクティブになっている要求を区別できるようにするためのものです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfcb" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfcb)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、この FCB が開かれている NET_ROOT 構造体のメモリ内データ構造に新しい FCB 構造体を割り当て、初期化し、挿入します。 割り当てられた構造体には、SRV_OPEN および FOBX 構造体の領域があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>このルーチンは、新しい RX_CONTEXT 構造体を割り当て、データ構造体を初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvcall" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvcall)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、サーバー呼び出しコンテキストを表すノードを構築し、RDBSS によって管理される net name テーブルに名前を挿入します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvopen" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvopen)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS によって使用されるメモリ内データ構造に新しい SRV_OPEN 構造体を割り当て、初期化し、挿入します。 新しい構造体を割り当てる必要がある場合は、FOBX 構造体の領域があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatevnetroot" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatevnetroot)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、V_NET_ROOT 構造体を表すノードを構築し、その名前を NET name テーブルに挿入します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>このルーチンは、カーネルデバッガーによって処理される例外を発生させます (カーネルデバッガーがインストールされている場合)。それ以外の場合は、デバッグシステムによって処理されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS によって使用されるいくつかの参照カウントデータ構造体のインスタンスの参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体を逆参照し、参照カウントがゼロになると、指定された RX_CONTEXT 構造体を RDBSS のメモリ内データ構造から解放し、削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS データ構造体の既存のインスタンスを破棄し、割り当てられたメモリを解放します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカースレッドのコンテキストでルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS を初期化するために、その<strong>Driverentry</strong>からモノリシックネットワークミニリダイレクタードライバーによって呼び出されます。</p>
<p>モノリシックでないドライバーの場合、この初期化ルーチンは、 <em>rdbss</em>デバイスドライバーの<strong>driverentry</strong>ルーチンに相当します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizeconnection" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizeconnection)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>このルーチンは、共有への接続を削除します。 接続で開いたファイルは、指定された force レベルに応じて閉じられます。 ネットワークミニリダイレクターは、接続の終了を強制するオプションが指定されていない限り、トランスポート接続をパフォーマンス上の理由から開いたままにしておくことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizenetfcb)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FCB 構造体を終了します。 呼び出し元には、FCB に関連付けられている NET_ROOT 構造体の排他ロックが必要です。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetfobx" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetfobx)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された FOBX 構造体を終了します。 呼び出し元は、この FOBX に関連付けられた FCB に排他ロックを保持している必要があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetroot" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetroot)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された NET_ROOT 構造体を終了します。 呼び出し元は、この NET_ROOT 構造体に関連付けられているデバイスオブジェクトの、SRV_CALL 構造体を介して、そのロックに排他的にアクセスできる必要があります。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvcall" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvcall)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_CALL 構造体を終了します。 呼び出し元には、この SRV_CALL 構造体に関連付けられているデバイスオブジェクトのネットテーブルのロックに対する排他アクセス権が必要です。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvopen" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvopen)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された SRV_OPEN 構造体を終了します。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o 要求パケット (IRP) を処理するための RDBSS のファイルシステムドライバー (FSD) ディスパッチを実装しています。 このルーチンは、要求の RDBSS 処理を開始するために、ドライバーディスパッチルーチンのネットワークミニリダイレクターによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体によって指定された i/o 要求パケット (IRP) を、ファイルシステムプロセス (FSP) による処理のためにワーカーキューにキューに置いています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxgetfilesizewithlock" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxgetfilesizewithlock)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>このルーチンは、64ビット値が一貫して読み取られるようにロックを使用して、FCB 構造体からファイルサイズを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxgetrdbssprocess" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxgetrdbssprocess)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS カーネルプロセスによって使用されるメインスレッドのプロセスへのポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンは、後で処理するために、バッファリング状態の変更要求 (oplock の中断を示すなど) を登録するために呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、後で処理するために、バッファリング状態の変更要求 (oplock の中断を示すなど) を登録するために呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxinferfiletype" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxinferfiletype)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体の<strong>Createoptions</strong> (<strong>オプション</strong>) フィールドからファイルの種類 (ディレクトリまたはディレクトリ以外) を推論しようとします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>このルーチンは、新しく割り当てられた RX_CONTEXT 構造体を初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxisthisacscagentopen" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxisthisacscagentopen)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、ファイルがユーザーモードのクライアント側キャッシュエージェントによって作成されたかどうかを判断します。</p>
<p>このルーチンは、Windows Server 2003 でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlockenumerator" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlockenumerator)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB のファイルロックを列挙するために、ネットワークミニリダイレクターから呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o エラーログにエラーを記録するために呼び出されます。 このルーチンを直接呼び出すのではなく、 <strong>RxLogEvent</strong>または<strong>RxLogFailure</strong>マクロを使用することをお勧めします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o エラーログ構造を割り当て、ログ構造を格納し、この構造を i/o エラーログに書き込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o エラーログにエラーを記録するために呼び出されます。 このルーチンは、行番号と状態を i/o エラーログ構造に格納されているデータバッファーにエンコードします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>このルーチンは、処理が完了したときに、最初に保留が返された場合に、ネットワークミニリダイレクタードライバーの低 i/o ルーチンによって呼び出される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体の<strong>Lowiocontext</strong>構造から、MDL に対応するバッファーを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxmakelatedeviceavailable" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxmakelatedeviceavailable)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>このルーチンは、デバイスオブジェクトを変更して "遅延デバイス" を使用できるようにします。 遅延デバイスとは、ドライバーの読み込みルーチンで作成されたものではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を MID_ATLAS データ構造内の関連付けられたコンテキストにマップし、その中間とコンテキストとの関連付けを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS データ構造内の関連付けられているコンテキストに MID をマップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o 要求パケット (IRP) からのシステムバッファーアドレスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、名前キャッシュエントリを受け取り、有効期限とネットワークミニリダイレクターコンテキストを更新します。 次に、アクティブなリストにエントリを配置します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリの有効性を確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された名前の文字列を使用して NAME_CACHE 構造体を割り当て、初期化します。 呼び出し元は、name cache コンテキストの追加のネットワークミニリダイレクター要素を初期化し、そのエントリを name cache active list に配置する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリをフリーリストに挿入します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された短いファイル名と一致する名前プレフィックスを持つすべての NAME_CACHE エントリの有効期限が切れます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリに対して指定された名前の文字列との一致を検索します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE_CONTROL 構造体に関連付けられているすべての NAME_CACHE エントリのストレージを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE エントリのストレージを解放し、NAME_CACHE_CONTROL 構造に関連付けられている NAME_CACHE キャッシュエントリの数を減らします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>このルーチンは、NAME_CACHE 構造体を初期化し、NAME_CACHE_CONTROL 構造体に関連付けます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/rxnewmapuserbuffer)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>このルーチンは、低 i/o に使用されたユーザーバッファーのアドレスを返します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前をカタログ化するために使用されるプレフィックステーブルに対して排他ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前のカタログ化に使用されるプレフィックステーブルに対して共有ロックを取得します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>このルーチンは参照カウントを逆参照し、FCB を終了します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferencenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferencenetfcb)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをデクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、ドライバーがワンショットタイマー要求を初期化するために使用されます。 タイマーの有効期限が切れると、このルーチンに渡されるワーカースレッドルーチンが1回呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、定期的なタイマー要求を初期化するために使用されます。 このルーチンに渡されるワーカースレッドルーチンは、このルーチンへの入力パラメーターに基づいて定期的なタイマーが起動されると、一定の間隔で呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>このルーチンは、ワーカースレッドのコンテキストでルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpreferencenetfcb" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpreferencenetfcb)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>このルーチンは、FCB の参照カウントをインクリメントします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前をカタログ化するために使用されるプレフィックステーブル内の名前を検索し、基になるポインターから含んでいる構造体に変換します。</p>
<p>このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>このルーチンは、SRV_CALL と NET_ROOT の名前をカタログ化するために使用されるプレフィックステーブルのロックを解放します。</p>
<p>このルーチンは、Windows XP および Windows 2000 でのみ使用できます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクタードライバーでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>このルーチンは、実行されたすべての操作固有の割り当てと取得をリセットすることによって、再利用できるように RX_CONTEXT 構造を準備します。 IRP から取得したパラメーターは変更されません。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>このルーチンは、再解析を容易にするためにファイルオブジェクト名を設定します。 このルーチンは、シンボリックリンクをスキャンするためにネットワークミニリダイレクターによって使用されます。 このルーチンは、RDBSS によって内部的に使用されるため、ネットワークミニリダイレクターでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference)"><strong>Rxp Track逆参照</strong></a></p></td>
<td align="left"><p>このルーチンは、チェックを行うビルドで、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB、SRV_OPEN の各構造を逆参照する要求を追跡するために使用されます。 これらの逆参照要求のログは、ログ記録システムおよび WMI からアクセスできます。</p>
<p>リテールビルドの場合、このルーチンは何も行いません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference)"><strong>Rxp Trackreference</strong></a></p></td>
<td align="left"><p>このルーチンは、チェックされたビルドで、SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB、および SRV_OPEN 構造体を参照する要求を追跡するために使用されます。 これらの参照要求のログは、ログ記録システムおよび WMI からアクセスできます。</p>
<p>リテールビルドの場合、このルーチンは何も行いません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS を使用してドライバーの登録を解除し、内部 RDBSS 登録テーブルから登録情報を削除するために、ネットワークミニリダイレクタードライバーによって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクターに関連付けられているすべての FOBX 構造を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造体に関連付けられているすべての FOBX 構造体を削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を別のコンテキストに再関連付けします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS によって使用されるいくつかの参照カウントデータ構造体のインスタンスの参照カウントをインクリメントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクタードライバーによって呼び出され、ドライバーを RDBSS に登録します。これにより、登録情報が内部登録テーブルに追加されます。 RDBSS は、ネットワークミニリダイレクター用のデバイスオブジェクトも構築します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンは、 <strong>RxAcquireExclusiveFcbResourceInMRx</strong>または<strong>RxAcquireSharedFcbResourceInMRx</strong>を使用して取得した FCB リソースを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>このルーチンは、RxAcquireSharedFcbResourceInMRxEx を使用して取得した FCB リソースを解放します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"></a></p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>このルーチンは、シリアル化されたブロッキング i/o キューで次の待機中のスレッド (存在する場合) をウェイクアップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のネットワークミニリダイレクターデバイスオブジェクトに関連付けられているすべての FOBX 構造を清掃します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された NET_ROOT 構造体に関連するすべての FOBX 構造体を清掃します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>このルーチンは、mailslots がドライバーでサポートされている場合に、メールスロットブロードキャストに使用されるドメインを設定するために、ネットワークミニリダイレクタードライバーによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>このルーチンは、RX_CONTEXT 構造体に対してネットワークミニリダイレクターのキャンセルルーチンを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxsetsrvcalldomainname" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxsetsrvcalldomainname)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のサーバー (SRV_CALL 構造) に関連付けられているドメイン名を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクターのディスパッチャーコンテキストを破棄します。</p>
<p>このルーチンは、Windows XP 以降でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、を呼び出して自身を登録するネットワークミニリダイレクターを起動します。 また、ドライバーが UNC 名をサポートしている場合は、RDBSS (MUP) と共 Multiple UNC Provider にネットワークミニリダイレクタードライバーが UNC (汎用名前付け規則) プロバイダーとして登録されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクタードライバーを停止します。 停止したドライバーは、新しいコマンドを受け付けなくなります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、 <em>rxstruc</em>で定義されたインライン関数で、RDBSS でドライバーの登録を解除し、内部 RDBSS 登録テーブルから登録情報を削除するために、ネットワークミニリダイレクタードライバーによって呼び出されます。 <strong>RxUnregisterMinirdr</strong> inline 関数は、内部的に<strong>RxpUnregisterMinirdr</strong>を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリの問題のインスタンスをキャッチするために使用できる、ブロックの先頭に4バイトのタグを持つプールからメモリを割り当てます。</p>
<p>このルーチンを直接呼び出すのではなく、 <strong>RxAllocatePoolWithTag</strong>マクロを使用することをお勧めします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリブロックに特別な RX_POOL_HEADER HEADER 署名があるかどうかをチェックします。 ネットワークミニリダイレクタードライバーは、ルーチンを使用するために割り当てられたメモリに、この特殊な署名ブロックを追加する必要があることに注意してください。</p>
<p>この特別なヘッダーブロックが実装されていないため、このルーチンは使用しないでください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリプールを解放します。</p>
<p>このルーチンを直接呼び出すのではなく、 <strong>RxFreePool</strong>マクロを使用することをお勧めします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>このルーチンは、書式指定文字列と可変数のパラメーターを受け取り、ログ記録が有効になっている場合に i/o エラーログエントリとして構造体を作成するための出力文字列を書式設定します。</p>
<p>このルーチンを直接呼び出すのではなく、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>RxLog</strong></a>マクロを使用することをお勧めします。</p>
<p>このルーチンは、Windows Server 2003、Windows XP、および Windows 2000 の RDBSS のチェックされたビルドでのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、通常のディスパッチ i/o ベクターと同一の高速 i/o ディスパッチベクターを入力し、渡されたデバイスオブジェクトに関連付けられているドライバーオブジェクトにインストールします。</p>
<p>このルーチンは、モノリシックでないドライバーに対してのみ実装され、モノリシックドライバーでは何も行いません。</p></td>
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

 

 

 





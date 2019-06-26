---
title: 接続エンジン管理
description: 接続エンジン管理
ms.assetid: 00ac74c5-2a69-493f-ad9b-6fa2f9082ac1
keywords:
- RDBSS WDK ファイル システム、エンジンの接続の管理
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、エンジンの接続の管理
- 接続エンジン WDK ネットワーク リダイレクター
- TDI ドライバー WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddee33c37803ed8e6996c698d34265fc71c5e731
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378964"
---
# <a name="connection-engine-management"></a>接続エンジン管理


## <span id="ddk_connection_engine_management_if"></span><span id="DDK_CONNECTION_ENGINE_MANAGEMENT_IF"></span>


RDBSS、接続のエンジンにマップし、可能な限り TDI 仕様をエミュレートする設計されています。 これは、完全にネットワークのミニ リダイレクターを使用するための基になる TDI 実装を悪用する効率的なメカニズムを提供します。

RDBSS 接続エンジンは、TDI を抽象化は、ネットワーク リダイレクターは無料 RDBSS 接続エンジン ルーチンを使用する代わりに TDI と直接通信するためにもします。 TDI のラッパーを提供する既存の RDBSS 接続エンジン ルーチンは、非常に Windows を中心とした、他のネットワークの責任者の適切なことができない可能性がありますので、Microsoft のネットワークをサポートするために開発されました。 また、RDBSS で接続エンジン ルーチンは、Windows Server 2003 以降後にリリースされた Windows オペレーティング システムから削除するがあります。 今後は、各ネットワーク リダイレクターが (TDI またはその他のいくつかのトランスポートの場合) に必要な接続エンジン ルーチンの開発を担当になります。 たとえば、WebDAV リダイレクターはでした TDI ではなく (標準 TCP/IP) の HTTP パケットを送信するいくつかのユーザー モード reflector プロセスに問い合わせてください。

RDBSS 接続エンジンのルーチンは、次のエンティティを処理します。

-   トランスポート

-   トランスポート アドレス

-   トランスポートの接続

-   接続で仮想回線

トランスポートは、任意のシステムでさまざまなトランスポートのサービス プロバイダーへのバインドです。 トランスポートのアドレスは、ローカル接続の終点をされます。 接続は、エンドポイント間のトランスポート接続です。 各接続は、さまざまな仮想回線 (通常は 1 つ) をカプセル化します。

次の重要なデータ構造が作成され、RDBSS に関連付けられているさまざまな接続エンジン ルーチンによって操作します。

-   RXCE\_トランスポート--すべてのトランスポートのパラメーターをカプセル化します

-   RXCE\_アドレス--すべてのトランスポート アドレスのパラメーターをカプセル化します

-   RXCE\_接続--すべてのトランスポート接続のパラメーターをカプセル化します

-   RXCE\_VC--すべてのトランスポート接続で仮想回線のパラメーターをカプセル化します

ネットワーク ミニ リダイレクター ドライバーは、これらのデータ構造を使用して、、ビルド エンジンを接続する特定の部分を破棄して、各種類に対して指定したルーチンを呼び出すことができます。 これらのルーチンでは割り当てできませんまたはこれらの構造に関連付けられているメモリを解放しないでください。 これは、これらの接続エンジン データ構造体のインスタンスを管理するミニ リダイレクター ドライバーの柔軟なメカニズムを提供します。

上記で説明した 4 つの接続エンジンの種類が特別な RXCE で各データ構造体の先頭にタグ付けされた\_検証 RDBSS で広範囲に使用される署名の署名。

RDBSS は、ネットワークのミニ リダイレクター ドライバーで使用できる次の接続エンジン ルーチンを提供します。

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
<td align="left"><p>このルーチンは、ローカル RDBSS 接続アドレスと、特定のリモート アドレスの間の接続を確立し、複数のトランスポートをサポートします。 一連のローカル アドレスは指定され、このルーチンはすべてのローカル アドレスに関連付けられたトランスポート経由でターゲット サーバーに接続しようとしています。 1 つの接続は、接続オプションによって優勝者として選択されます。 このルーチンは、システム ワーカー スレッドのコンテキストで呼び出される必要があります。</p></td>
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
<td align="left"><p>このルーチンは、接続に関連する情報を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequerytransportinformation" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcequerytransportinformation)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>このルーチンは、接続の数と特定のトランスポートのサービスの品質に関するトランスポート情報を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcesend" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxce/nf-rxce-rxcesend)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>このルーチンでは、仮想回線で指定された接続に沿ったの TSDU を送信します。</p></td>
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
</tbody>
</table>

 

**注**   Windows Vista の後に、TDI が Microsoft Windows のバージョンでサポートされません。 使用[Windows フィルタ リング プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)または[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)代わりにします。

 

 

 





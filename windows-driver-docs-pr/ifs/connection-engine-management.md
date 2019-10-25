---
title: 接続エンジン管理
description: 接続エンジン管理
ms.assetid: 00ac74c5-2a69-493f-ad9b-6fa2f9082ac1
keywords:
- RDBSS WDK ファイルシステム, 接続エンジン管理
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、接続エンジン管理
- 接続エンジンの WDK ネットワークリダイレクター
- TDI ドライバー WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274cd96bbefca0167b9b7f10aa91c600747ec629
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841458"
---
# <a name="connection-engine-management"></a>接続エンジン管理


## <span id="ddk_connection_engine_management_if"></span><span id="DDK_CONNECTION_ENGINE_MANAGEMENT_IF"></span>


RDBSS では、接続エンジンは、可能な限り TDI 仕様をマップおよびエミュレートするように設計されています。 これにより、ネットワークミニリダイレクターで使用するために、基になる TDI 実装を完全に悪用する効率的なメカニズムが提供されます。

RDBSS 接続エンジンは、TDI を抽象化しますが、ネットワークリダイレクターは、これらの RDBSS 接続エンジンルーチンを使用する代わりに、TDI と直接通信することもできます。 TDI のラッパーを提供する既存の RDBSS 接続エンジンルーチンは、Microsoft ネットワークをサポートするために開発されたものであるため、Windows 中心であり、他のネットワークディレクターには適していない可能性があります。 また、RDBSS の接続エンジンルーチンは、Windows Server 2003 以降にリリースされた Windows オペレーティングシステムから削除される予定です。 今後、各ネットワークリダイレクターは、必要な接続エンジンルーチン (TDI またはその他のトランスポート) の開発を担当します。 たとえば、WebDAV リダイレクターは、TDI ではなく HTTP パケット (標準 TCP/IP) を送信するために、一部のユーザーモードリフレクタープロセスと通信できます。

RDBSS 接続エンジンルーチンは、次のエンティティに対処します。

-   プロトコル

-   トランスポートアドレス

-   トランスポート接続

-   接続上の仮想回線

トランスポートは、システム上のさまざまなトランスポートサービスプロバイダーへのバインドです。 トランスポートアドレスは、ローカル接続エンドポイントです。 接続は、エンドポイント間のトランスポート接続です。 各接続は、多数の仮想回線 (通常は1つ) をカプセル化します。

次の重要なデータ構造は、RDBSS に関連付けられたさまざまな接続エンジンルーチンによって作成および操作されます。

-   RXCE\_TRANSPORT--トランスポートのすべてのパラメーターをカプセル化します。

-   RXCE\_ADDRESS--トランスポートアドレスのすべてのパラメーターをカプセル化します。

-   RXCE\_接続--トランスポート接続のすべてのパラメーターをカプセル化します。

-   RXCE\_VC--トランスポート接続上の仮想回線のすべてのパラメーターをカプセル化します。

ネットワークミニリダイレクタードライバーでは、これらのデータ構造を使用して、各型に対して提供されるルーチンを呼び出して、接続エンジンの部分を構築および破棄することができます。 これらのルーチンは、これらの構造体に関連付けられているメモリの割り当てや解放を行いません。 これにより、このような接続エンジンのデータ構造のインスタンスを管理するための柔軟な機能がミニリダイレクタードライバーに提供されます。

上記で説明した4種類の接続エンジンは、各データ構造体の先頭に、検証に RDBSS が広く使用する特殊な RXCE\_署名署名を使用してタグ付けされています。

RDBSS には、ネットワークミニリダイレクタードライバーで使用できる次の接続エンジンルーチンが用意されています。

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
<td align="left"><p>このルーチンは、ローカルの RDBSS 接続アドレスと指定されたリモートアドレスとの間の接続を確立し、複数のトランスポートをサポートします。 ローカルアドレスのセットが指定され、このルーチンは、ローカルアドレスに関連付けられているすべてのトランスポートを介して対象サーバーへの接続を試みます。 接続オプションに応じて、1つの接続が勝者として選択されます。 このルーチンは、システムワーカースレッドのコンテキストで呼び出す必要があります。</p></td>
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
<td align="left"><p>このルーチンは、接続に関連する情報を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>このルーチンは、指定されたトランスポートの接続数とサービスの品質に関するトランスポート情報を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>このルーチンは、仮想回線上の指定された接続に沿って TSDU を送信します。</p></td>
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
</tbody>
</table>

 

Windows Vista 以降では、Microsoft Windows のバージョンでは TDI はサポートされませ**ん  。** 代わりに、 [Windows フィルタリングプラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)または[Winsock カーネル](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を使用してください。

 

 

 





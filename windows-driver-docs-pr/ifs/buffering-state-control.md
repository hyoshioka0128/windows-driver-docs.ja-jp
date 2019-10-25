---
title: バッファー処理状態の制御
description: バッファー処理状態の制御
ms.assetid: 16590332-9d0d-4d8b-8304-a3fa9269c0e2
keywords:
- RDBSS WDK ファイルシステム、バッファリング状態
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、バッファリング状態
- 状態のバッファリング (WDK RDBSS)
- 分散キャッシュの一貫性に関する WDK RDBSS
- WDK RDBSS をキャッシュする
- SRV_OPEN 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b664f3966da3bde490d0310bcd1633540918de6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841478"
---
# <a name="buffering-state-control"></a>バッファー処理状態の制御


## <span id="ddk_buffering_state_control_if"></span><span id="DDK_BUFFERING_STATE_CONTROL_IF"></span>


RDBSS には、分散キャッシュの一貫性をさまざまなネットワークミニリダイレクターと組み合わせて提供するためのメカニズムであるバッファリングマネージャーが用意されています。 このサービスは、バッファリング状態の変更要求を処理する RDBSS のバッファリングマネージャーにカプセル化されています。 RDBSS のバッファリングマネージャーは、さまざまなネットワークミニリダイレクターおよび RDBSS によって生成されたすべての変更バッファリング状態要求に対するアクションを追跡し、開始します。

一般的なネットワークミニリダイレクターでのキャッシュの一貫性の実装には、いくつかの一般的なコンポーネントがあります。

-   ファイルルーチンを作成して開くための変更。

    このパスでは、バッファリング要求の種類が決定され、適切な要求がサーバーに対して行われます。 ネットワークミニリダイレクターおよび場合によっては、サーバーから戻ると、作成またはオープン呼び出しの結果に基づいて、FCB に関連付けられているバッファリング状態が更新されます。

-   サーバーからの変更バッファリング状態通知を処理するための指示コードを受け取るように変更します。

    このような要求が検出された場合は、バッファリング状態を調整するローカル機構をトリガーする必要があります。

-   RDBSS の一部として実装されるバッファリング状態を変更するための機構。 変更バッファリング状態要求では、要求が適用されるオープン構造の SRV\_を識別する必要があります。

SRV\_のオープン構造を識別するために必要な計算作業の量は、ネットワークミニリダイレクターのプロトコルと詳細によって異なります。 SMB プロトコルでは、便宜的ロック (oplock) によって、キャッシュの一貫性を確保するために必要なインフラストラクチャが提供されます。 Windows での SMB プロトコルの実装では、RDBSS によって提供される多重 ID Api が使用されます。 サーバーでは、サーバーで開かれたファイルを識別するために使用される多重 ID を選択します。 多重 Id は、それらが開かれている NET\_ROOT (共有) に関連しています。 したがって、すべての変更バッファリング状態要求は、NetRootKey と SrvOpenKey の2つのキーによって識別されます。このキーは、それぞれ適切な NET\_ROOT および SRV\_OPEN 構造体に変換する必要があります。 リソースの取得/解放メカニズムとの統合を強化し、さまざまなネットワークミニリダイレクターでのこの作業の重複を回避するために、RDBSS はこのサービスを提供します。

RDBSS で提供されるルーチンは2つあります。これは、SRV\_開いている構造体に対するバッファリング状態の変化を示すためのものです。

-   要求を登録するための[**RxIndicateChangeOfBufferingState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)

-   SRV\_OPEN 構造体をキーと関連付けるための[**RxIndicateChangeOfBufferingStateForSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)

キーの関連付けは元に戻すことができないため、関連付けられた SRV\_オープン構造の有効期間が終了します。

ネットワークミニリダイレクターは、多重 Id から SRV\_のオープン構造へのマッピングを確立するための補助機構を必要としますが、 [**RxIndicateChangeOfBufferingState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)を使用できますが、これは不要なネットワークミニリダイレクターです。[**RxIndicateChangeOfBufferingStateForSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)を使用することができます。

RDBSS のバッファリングマネージャーは、これらの要求をさまざまな段階で処理します。 さまざまな基盤となるネットワークミニリダイレクターから受信した要求を、複数のリストのいずれかに保持します。

-   ディスパッチャーの一覧には、SRV\_OPEN 構造体に対する適切なマッピングが確立されていないすべての要求が含まれます。

-   ハンドラーの一覧には、適切なマッピングが確立されているがまだ処理されていないすべての要求が含まれています。

-   LastChanceHandlerList には、初期処理が失敗したすべての要求が含まれています。 これは通常、変更バッファリング状態要求の受信時に FCB が共有モードで取得された場合に発生します。 このような場合、oplock 解除要求は遅延ワーカースレッドでのみ処理できます。

ネットワークミニリダイレクタードライバーでの変更バッファリング状態要求の処理は、FCB の取得と解放のプロトコルに関係ます。 これにより、ターンアラウンド時間が短縮されます。

RDBSS には、ネットワークミニリダイレクタードライバーで使用できるバッファリング状態を管理するための次のルーチンが用意されています。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンは、バッファリング状態の変更要求を処理するために呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンは、後で処理するために、バッファリング状態の変更要求 (oplock の中断を示すなど) を登録するために呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンは、後で処理するために、バッファリング状態の変更要求 (oplock の中断を示すなど) を登録するために呼び出されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: バッファー処理状態の制御
description: バッファー処理状態の制御
ms.assetid: 16590332-9d0d-4d8b-8304-a3fa9269c0e2
keywords:
- バッファリング状態、RDBSS WDK ファイル システム
- バッファリング状態、リダイレクトされたバッファリング サブシステム WDK のドライブのファイル システム
- バッファリング状態 WDK RDBSS
- 分散キャッシュ コヒレンシー WDK RDBSS
- キャッシュ WDK RDBSS
- SRV_OPEN 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3042dc6dd1a967db8b6fad3f7b4b6c050a687f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391498"
---
# <a name="buffering-state-control"></a>バッファー処理状態の制御


## <span id="ddk_buffering_state_control_if"></span><span id="DDK_BUFFERING_STATE_CONTROL_IF"></span>


RDBSS では、バッファーのマネージャー、さまざまなネットワーク ミニ-リダイレクターを組み合わせて、分散キャッシュの一貫性を提供するためのメカニズムを提供します。 このサービスは、バッファリングの状態を変更する要求を処理する RDBSS でバッファリング マネージャーでカプセル化されます。 RDBSS のバッファー マネージャーは、追跡し、RDBSS とさまざまなネットワークのミニ リダイレクターによって生成された状態の要求をバッファリングするすべての変更操作を開始します。

標準的なネットワークのミニ リダイレクターでキャッシュ コヒレンシーの実装には、いくつかの一般的なコンポーネントがあります。

-   作成して開くファイルのルーチンの変更。

    このパスでバッファリング要求の種類が決定され、サーバーに適切な要求が行われました。 ネットワーク ミニリダイレクターと可能性があるサーバーから戻ると、作成または開くための呼び出しの結果に基づいて、FCB に関連付けられているバッファー処理の状態が更新されました。

-   処理するために、ことを示すコードを受信する変更は、サーバーからバッファリング状態の通知を変更します。

    このような要求が検出されると、バッファーの状態を調整するローカルのメカニズムをトリガーする必要があります。

-   RDBSS の一部として実装されているバッファーの状態を変更するためのメカニズムです。 バッファリング状態の要求の変更は、SRV を識別する必要があります\_オープン構造体が、要求が適用されます。

SRV を識別するときに関係する計算作業量\_オープン構造体は、プロトコルとネットワークのミニ リダイレクターの詳細によって異なります。 SMB プロトコルでは、便宜的ロック (oplock) は、キャッシュの一貫性を必要なインフラストラクチャを提供します。 Windows での SMB プロトコルの実装によって RDBSS マルチプレクシング ID Api が提供されているが使用されます。 サーバーで開かれたファイルを識別するために使用する multiplex ID を取得するサーバーを取得します。 Id は、NET の基準とした、マルチプレクシング\_ルート (共有) が開かれます。 したがって、すべての変更状態要求をバッファリングが 2 つのキーによって識別: NetRootKey と適切な NET に変換する必要があると、SrvOpenKey\_ルートや SRV\_それぞれ構造を開きます。 リソースの取得/解放メカニズムにより優れた統合を提供して、さまざまなネットワークのミニ リダイレクターでこの作業の重複を回避するために、RDBSS はこのサービスを提供します。

SRV バッファリング状態変更を示す RDBSS で指定された 2 つのルーチンがある\_構造体の開く。

-   [**RxIndicateChangeOfBufferingState** ](https://msdn.microsoft.com/library/windows/hardware/ff554485)要求を登録します。

-   [**RxIndicateChangeOfBufferingStateForSrvOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff554490) 、SRV を関連付けるため\_キーを持つ構造体を開く

キーの関連付けが元に戻せる状態でないし、関連付けられている SRV の有効期間が最後に注意してください\_オープン構造体。

ミニ リダイレクター multiplex Id から、SRV へのマッピングを確立するための補助のメカニズムを必要があるネットワーク\_オープン構造が使用できる[ **RxIndicateChangeOfBufferingState**](https://msdn.microsoft.com/library/windows/hardware/ff554485)、このサポートを必要としないネットワークのミニ-リダイレクターを使用できます[ **RxIndicateChangeOfBufferingStateForSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff554490)します。

RDBSS のバッファー マネージャーは、さまざまな段階でこれらの要求を処理します。 さまざまな基になるネットワーク ミニ-リダイレクターでいくつかのリストのいずれかから受信した要求を保持します。

-   ディスパッチャーの一覧を含むすべての要求を適切なマッピングを SRV\_オープン構造が確立されていません。

-   ハンドラーの一覧には、すべての対象の適切なマッピングが、確立されましたが、まだ処理されていない要求が含まれています。

-   LastChanceHandlerList には、すべての初期の処理が成功したいない要求が含まれます。 これは通常、状態要求をバッファリングする変更を受け取った時点で、FCB が共有モードで取得されたときに発生します。 このような場合は、oplock 解除要求は、遅延のワーカー スレッドでしか処理できません。

変更バッファリング状態要求がネットワークのミニ リダイレクター ドライバーで処理は FCB の取得と解放のプロトコルと絡まり合っています。 これによりより短い時間がかかってことを確認します。

RDBSS には、ネットワークのミニ リダイレクター ドライバーで使用できるバッファーの状態を管理する次のルーチンが用意されています。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554335" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554335)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンは、バッファリング状態の変更要求の処理に呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554485" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554485)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>このルーチンはバッファリング状態変更要求 (oplock 中断を示す値、たとえば) 後で処理するための登録と呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554490" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554490)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>このルーチンはバッファリング状態変更要求 (oplock 中断を示す値、たとえば) 後で処理するための登録と呼ばれます。</p></td>
</tr>
</tbody>
</table>

 

 

 





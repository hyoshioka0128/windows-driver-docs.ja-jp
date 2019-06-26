---
title: 多重 ID 管理
description: 多重 ID 管理
ms.assetid: feffc421-bd51-4174-80a4-1f9a36355667
keywords:
- RDBSS WDK ファイル システム、ID を多重化します。
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、ID を多重化します。
- 多重化 ID WDK ネットワーク リダイレクター
- MID WDK ネットワーク リダイレクター
- MID のマッピング
- MID_ATLAS 構造体
- MID_MAP 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcad2321ab6254231361170c0dbc54c74bd92a84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383863"
---
# <a name="multiplex-id-management"></a>多重 ID 管理


## <span id="ddk_multiplex_id_management_if"></span><span id="DDK_MULTIPLEX_ID_MANAGEMENT_IF"></span>


RDBSS を多重化 ID (MID)、すべての接続で同時にアクティブな要求を区別する (ミニリダイレクター) のネットワーク クライアントとサーバーの両方で使用できる 16 ビットの値を定義します。 ネットワーク リダイレクターは、任意のコンテキストや内部データ構造に使用すると、MID を関連付けることができます。 完全にネットワーク リダイレクターのオプションの搭載を割り当てられ、使用するかどうか。

MID の一部は、MID、RDBSS で定義されている、\_ATLAS データ構造ではいくつかの条件を満たすために設計されています。 関連付けられた、MID\_ATLAS データ構造は、一連の 1 つまたは複数の MID\_搭載を関連付けられているコンテキストにマップするために使用するデータ構造をマップします。

MID\_ATLAS データ構造、MID\_マップの構造と搭載が異なるさまざまなリモート サーバーの機能の処理に適切にスケールする必要があります。 たとえば、Windows の標準的な LAN Manager サーバーは、任意の接続で 50 の未処理の要求を許可します。 いくつかの種類のサーバーは、この数は (未処理の接続の数千) の順序は非常に高くなることをゲートウェイ サーバー間、未処理の要求が 1 つとして、いくつかサポート可能性があります。

適切に処理する必要がある 2 つの主な操作は次のとおりです。

-   関連付けられているコンテキストに、MID をマッピングします。 このルーチンは、クライアントとサーバー (サーバーは、搭載の使用を想定) の両方で任意の接続上で受け取られるすべてのパケットの処理に呼び出されます。

-   サーバーに要求を送信するための新しい MID を生成しています。 このルーチンは、一意の id。 指定された各同時実行要求をタグ付けの場合と同様、最大接続数制限の適用のクライアントで使用されます。

MID は、65,536 値の組み合わせから、一意のタグ付けおよび搭載 (通常は 50) 数の id を効率的に管理できる必要があります。 場合によっては、小さな MID を作成する方が必要があります\_MID で使用されるカーネルのメモリを節約する ATLAS 構造\_構造をマップおよび MID のサイズを拡張\_ATLAS 構造の使用率が高くを効率的に処理するために必要な場合。 適切な時間領域のトレードオフを確実には、検索は、3 つのレベルの階層として編成されます。 MID を表すために使用される 16 ビットは、ビット フィールドの 3 つに分類されます。 (最下位) の最も右にあるフィールドの長さは初期 atlas で使用できる搭載の最大数によって決定されます。 この最大値にパラメーターを渡すは、 [ **RxCreateMidAtlas** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas)ルーチンと MID\_ATLAS データ構造が最初に作成します。 この最大値、MID の初期サイズを決定する\_ATLAS データ構造が作成されると数 MID\_マップ データ構造に対応することができます。 残りの長さは可能な下位 MID の最大サイズを決定する次の 2 つのフィールドの間で均等に分割されます\_ATLAS 構造を展開し、既存の MID を拡張するために定義できる\_ATLAS が 3 つのレベルMID の階層\_マップ データ構造体。 したがってには、各 MID\_ATLAS データ構造が MID の最大数を含めることができます\_マップ構造または 1 つの下位 MID へのポインター\_ATLAS と MID\_マップの構造体。

たとえば、最大 50 の搭載の作成時に割り当てられると場合、に、最初のフィールドの長さは 6 (64 (2 \* \* 6) が 50 より大きい)。 残りの長さに分割されて、2 番目と 3 つ目の階層のレベルの 5 ビットごとの 2 つのフィールドのためを既存の MID\_ATLAS データ構造を展開するには複数 MID を対応するために\_マップ エントリ。

RDBSS 作成と操作、MID、次のルーチンを提供する\_ATLAS データ構造体に関連付けられた MID\_マップ データ構造体、および Multiplex Id。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>このルーチンは、指定した不透明なコンテキストを MID_ATLAS 構造から使用可能な MID に関連付けます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンでは、MID_ATLAS データ構造体の新しいインスタンス、それを初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンは MID_ATLAS データ構造体の既存のインスタンスを破棄し、それに割り当てられたメモリを解放します。 副作用として呼び出して、渡された MID_ATLAS 構造内のすべての有効なコンテキストのコンテキストのデストラクターでします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を MID_ATLAS 構造に関連付けられているそのコンテキストにマップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS 構造では、関連付けられているコンテキストに、MID をマップし、コンテキストから MID の関連付けを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>このルーチンは、代替のコンテキストで、MID を再関連付けします。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: 多重 ID 管理
description: 多重 ID 管理
ms.assetid: feffc421-bd51-4174-80a4-1f9a36355667
keywords:
- RDBSS WDK ファイルシステム、多重 ID
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、多重 ID
- 多重 ID WDK ネットワークリダイレクター
- 中間 WDK ネットワークリダイレクター
- マッピング中
- MID_ATLAS 構造体
- MID_MAP 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc73f78a61b1058d87f65020ff4b3eb8195f46e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841060"
---
# <a name="multiplex-id-management"></a>多重 ID 管理


## <span id="ddk_multiplex_id_management_if"></span><span id="DDK_MULTIPLEX_ID_MANAGEMENT_IF"></span>


RDBSS は、16ビット値の多重化 ID を定義します。この ID は、ネットワーククライアント (ミニリダイレクター) とサーバーの両方で使用でき、任意の接続で同時にアクティブになっている要求を区別するために使用されます。 ネットワークリダイレクターは、MID を、それが使用する任意のコンテキストまたは内部データ構造に関連付けることができます。 MIDs が割り当てられて使用されているかどうかにかかわらず、ネットワークリダイレクターのオプションで完全に設定されています。

RDBSS によって定義されている MID は、いくつかの条件を満たすように設計された、1つの\_アトラスデータ構造の一部です。 \_アトラスデータ構造に関連付けられている1つ以上の MID\_マップデータ構造体は、関連付けられたコンテキストに MIDs をマップするために使用されます。

\_アトラスデータ構造体、MID\_マップ構造体、および MIDs は、さまざまなリモートサーバーのさまざまな機能を処理するために適切にスケーリングする必要があります。 たとえば、Windows の一般的な LAN Manager サーバーでは、任意の接続で50の未処理の要求を許可しています。 サーバーの種類によっては、未処理の要求が1つしかサポートされない場合がありますが、ゲートウェイサーバーではこの数が非常に高くなることが求められる場合があります (多数の未処理の接続の順序で)。

適切に処理する必要がある2つの主な操作は次のとおりです。

-   MID をそれに関連付けられているコンテキストにマップする。 このルーチンは、クライアントとサーバーの両方で、任意の接続で受信したすべてのパケットを処理するために呼び出されます (サーバーで MIDs が使用されていることを前提としています)。

-   サーバーに要求を送信するための新しい MID を生成しています。 このルーチンは、最大接続数の制限を適用するためだけでなく、それぞれの同時要求に一意の ID をタグ付けするために、クライアントで使用されます。

MID は、65536値の可能な組み合わせから、一意のタグ付けと多数の MIDs (通常は 50) の識別を効率的に管理できる必要があります。 場合によっては、小さな MID\_アトラス構造を作成して、MID\_マップ構造によって使用されるカーネルメモリを節約し、必要に応じて MID\_アトラス構造のサイズを拡大して、より多くの使用量を効率的に処理することが理にかなっています。 適切な時間領域のトレードオフを保証するために、参照は3レベルの階層として編成されます。 MID を表すために使用される16ビットは、3つのビットフィールドに分割されます。 右端のフィールドの長さ (最も重要ではない) は、最初のアトラスで許可されている MIDs の最大数によって決定されます。 この最大値は、\_アトラスデータ構造体の最初の作成時に[**RxCreateMidAtlas**](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)ルーチンに渡されるパラメーターです。 この最大値によって、作成される MID\_アトラスデータ構造の初期サイズと、対応可能な MID\_マップデータ構造の数が決まります。 残りの長さは、次の2つのフィールド間で均等に分割されます。これにより、既存のミッド\_を拡大して拡張するために定義できるアトラス構造\_アトラス構造の最大サイズが中間の3レベルの階層になります。\_マップのデータ構造体。 そのため、各 MID\_アトラスデータ構造体には、\_マップ構造体の最大数、または1つの下位中央\_アトラスと中間\_マップ構造体へのポインターを含めることができます。

たとえば、作成時に最大 50 MIDs が割り当てられている場合、最初のフィールドの長さは 6 (64 (2 \*\* 6) が50を超える) になります。 残りの長さは、2番目と3番目の階層レベルでそれぞれ5ビットの2つのフィールドに分割されます。そのため、既存の MID\_アトラスデータ構造を拡張して、より多くの MID\_マップエントリに対応することができます。

RDBSS は、\_アトラスデータ構造体、関連する\_マップデータ構造体、および多重 Id を作成して操作するための次のルーチンを提供します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>このルーチンは、指定された不透明なコンテキストを、MID_ATLAS 構造体の使用可能な中間に関連付けます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS データ構造体の新しいインスタンスを割り当て、それを初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>このルーチンは、MID_ATLAS データ構造体の既存のインスタンスを破棄し、割り当てられたメモリを解放します。 副作用として、MID_ATLAS 構造体のすべての有効なコンテキストで、渡されたコンテキストデストラクターを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を MID_ATLAS 構造体内の関連付けられたコンテキストにマップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を MID_ATLAS 構造体内の関連付けられたコンテキストにマップし、その中間とコンテキストとの関連付けを解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>このルーチンは、MID を別のコンテキストに再関連付けします。</p></td>
</tr>
</tbody>
</table>

 

 

 





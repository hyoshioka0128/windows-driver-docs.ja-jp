---
title: リンク コレクション
description: リンク コレクション
ms.assetid: 3f934661-c33c-4c08-82ac-ee2e0f519c8e
keywords:
- コレクションの WDK を非表示のリンクします。
- 入れ子になったコレクションを非表示に WDK
- WDK の HID リンク コレクションの配列
- WDK の HID エイリアス化されたコレクション
- WDK の HID コレクション ノードをリンクします。
- WDK の HID 配列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5072f4ce271352902cfd2695ae8e7a4706804204
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371968"
---
# <a name="link-collections"></a>リンク コレクション





A*リンク コレクション*内で入れ子になったサブコレクションとして、[最上位のコレクション](top-level-collections.md)します。 最上位のコレクションには、0 個以上のリンク コレクションを持つことができます。

[**HidP\_GetLinkCollectionNodes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)最上位のコレクションを返します[リンク コレクション配列](#ddk-link-collection-array-kg)最上位のコレクションのリンク コレクションに関する情報を格納します。

### <a href="" id="ddk-link-collection-array-kg"></a>リンク コレクションの配列

A*リンク コレクション配列*最上位のコレクションに含まれるすべてのリンク コレクションについて説明します。 各リンク コレクションがによって表される、 [ **HIDP\_リンク\_コレクション\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_link_collection_node)構造体。 配列のリンクのノードは、最上位のコレクション内のシーケンシャルで階層的な順序を識別する方法でリンクされています。 リンク コレクションの配列の最初の要素は最上位のコレクションを表し、残りのメンバーは、最上位のコレクションのリンクのコレクションを表します。

リンク接続配列内のノードをトレースでは、ユーザー モード アプリケーションまたはカーネル モード ドライバーは、組織と最上位のコレクション内のすべてのリンク コレクションの使用状況を判断できます。 さらに、アプリケーションまたはドライバーは、それぞれのリンクのコレクションでコントロールを編成できます。 これは可能ですので、最上位のコレクションの[ボタン配列の機能](button-capability-arrays.md)と[機能の配列の値](value-capability-arrays.md)を含む各リンクのコレクションを識別[HID の使用状況](hid-usages.md)機能の配列で記述されます。

次の図は、次の 4 つのリンク コレクションを格納する最上位のコレクションの例を示します。

![次の 4 つのリンク コレクションを格納する最上位のコレクションを示す図](images/linkcol.png)

前の図に示されるように、上から下にまとめてリンクと左から右の順序 (ABCD) が、リンクのコレクション。 次の表には、最上位のコレクションとそのリンクのコレクション間のリンクが例では、各リンクのコレクションを示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>リンク ノード</th>
<th>Parent</th>
<th>Children</th>
<th>最初の子</th>
<th>次の兄弟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A</p></td>
<td><p>最上位のコレクション</p></td>
<td><p>B、C</p></td>
<td><p>B</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>B</p></td>
<td><p>A</p></td>
<td><p>D</p></td>
<td><p>D</p></td>
<td><p>C</p></td>
</tr>
<tr class="odd">
<td><p>C</p></td>
<td><p>A</p></td>
<td><p>なし</p></td>
<td><p>なし</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>D</p></td>
<td><p>B</p></td>
<td><p>なし</p></td>
<td><p>なし</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

リンク コレクションの配列を次の定義が保持します。

<a href="" id="parent"></a>**親**  
リンク コレクションの*親*はコレクションの上から下の階層でそのすぐ上のコレクションです。 リンクのコレクションでは、1 つの親があります。 **親**リンク ノードのメンバーは、リンクのコレクションの配列でその親のインデックスを指定します。

<a href="" id="children"></a>**子**  
リンク コレクションが、*子*の親。 親は、0 個以上の子でことができます。 **コード**リンク ノードのメンバーが親が子の数を指定します。

<a href="" id="sibling"></a>**兄弟**  
親の子が*兄弟*します。

<a href="" id="next-sibling"></a>**次の兄弟**  
兄弟では、左から右に順序付けされます。 兄弟の*次の兄弟*は兄弟のセットに存在する場合に、すぐに、右側の兄弟です。 **NextSibling**リンク コレクション ノードのメンバーがリンク コレクションの配列内の次の兄弟にインデックスを指定します。 リンク コレクション ノードには次の兄弟がない場合**NextSibling** 0 に設定されます。

<a href="" id="first-child"></a>**最初の子**  
*最初の子*は兄弟のセット内の一番左の兄弟です。 **FirstChild**リンク コレクション ノードのメンバーがリンク コレクションの配列の最初の子にインデックスを指定します。 リンク コレクション ノードが子を持たない場合**FirstChild** 0 に設定されます。

アプリケーションまたはドライバーが親コレクションのすべての子まで最初の子の兄弟をシーケンス処理、親の最初の子から開始して判断できます、 **NextSibling**の兄弟ノードのメンバーは 0 になります。

次のコードでは、リンク コレクション ノードのインデックスを使用してリンク コレクション 7 の最初の子を検索する方法を示します。

```cpp
HIDP_LINK_COLLECTION_NODE Collection[10] ;
HIDP_LINK_COLLECTION_NODE Node1 ;
 
Node1 = Collection[Collection[7].FirstChild]] ;
```

### <a href="" id="aliased-collections"></a> エイリアス化されたコレクション

区切り記号アイテムは、レポート記述子でのセットを区切るために使用できます*別名コレクション*します。 各エイリアス化されたコレクションは、エイリアス化されたリンク コレクション ノードによって表されます。 完全かつ一意のセット*n*、 *n* &gt;= 2、次のようにエイリアス化されたノードが互いにリンクします。

-   エイリアス化されたノードはリンク コレクションの配列内の連続した順序で。

-   最初の*n*-1 ノードがその**IsAlias**メンバーに設定**TRUE**します。 *N 番目*直後にこのような一連のノードがその**IsAlias**メンバーに設定**FALSE**します。 このノードには、エイリアス化されたノードのシーケンスが終了します。 このノードに関連付けられた使用量は、推奨される使用方法です。

アプリケーション、ドライバーは、コレクションでは、別名が繰り返しこのようなシーケンスを検索するリンク コレクションの配列の配列インデックスをインクリメントして判断できます。

[配列の機能をボタン](button-capability-arrays.md)と[機能の配列の値](value-capability-arrays.md)識別、説明、各使用法の使用状況を含むリンクのコレクション。 リンク コレクションが別名の場合は、機能の配列は、推奨される使用方法を指定します。

 

 





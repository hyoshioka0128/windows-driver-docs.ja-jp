---
title: リンク コレクション
description: リンク コレクション
ms.assetid: 3f934661-c33c-4c08-82ac-ee2e0f519c8e
keywords:
- コレクションのリンク WDK HID
- 入れ子になったコレクション WDK HID
- コレクションコレクションアレイの WDK HID のリンク
- エイリアスコレクション WDK HID
- コレクションノードのリンク WDK HID
- アレイ WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdd8413a928b06c4e557db0826afdb093521e5de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841574"
---
# <a name="link-collections"></a>リンク コレクション





[最上位レベルのコレクション](top-level-collections.md)内の入れ子になったサブコレクションとしての*リンクコレクション*。 最上位レベルのコレクションには、0個以上のリンクコレクションを含めることができます。

[**Hidp\_GetLinkCollectionNodes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes)は、最上位のコレクションのリンクコレクションに関する情報を含む最上位レベルのコレクションの[リンクコレクション配列](#ddk-link-collection-array-kg)を返します。

### <a href="" id="ddk-link-collection-array-kg"></a>リンクコレクションの配列

*リンクコレクションの配列*では、最上位のコレクションに含まれるすべてのリンクコレクションが記述されます。 各リンクコレクションは、 [ **\_コレクション\_ノード構造の Hidp\_リンク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_link_collection_node)によって表されます。 配列のリンクノードは、最上位のコレクション内の順序と階層順を識別する方法でリンクされています。 リンクコレクション配列の最初の要素は最上位のコレクションを表し、残りのメンバーは最上位レベルのコレクションのリンクコレクションを表します。

リンク接続配列内のノードをトレースすることにより、ユーザーモードアプリケーションまたはカーネルモードドライバーは、最上位のコレクションにあるすべてのリンクコレクションの組織と使用状況を判断できます。 さらに、アプリケーションまたはドライバーは、リンクコレクションによってコントロールを整理できます。 これが可能なのは、最上位レベルのコレクションの[ボタン機能の配列](button-capability-arrays.md)と[値の機能](value-capability-arrays.md)配列が、機能配列で記述されている各[HID 使用法](hid-usages.md)を含むリンクコレクションを識別するためです。

次の図は、4つのリンクコレクションを含む最上位レベルのコレクションの例を示しています。

![4つのリンクコレクションを含む最上位レベルのコレクションを示す図](images/linkcol.png)

前の図に示されているように、リンクコレクションは、上から下および左から右の順 (ABCD) にリンクされています。 次の表は、この例の各リンクコレクションについて、最上位コレクションとそのリンクコレクションとの間のリンクを示しています。

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
<th>ノードのリンク</th>
<th>Parent</th>
<th>Children</th>
<th>最初の子</th>
<th>次の兄弟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>確認が完了していないエイリアスの横には、</p></td>
<td><p>最上位レベルのコレクション</p></td>
<td><p>B、C</p></td>
<td><p>B</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>B</p></td>
<td><p>確認が完了していないエイリアスの横には、</p></td>
<td><p>D</p></td>
<td><p>D</p></td>
<td><p>C</p></td>
</tr>
<tr class="odd">
<td><p>C</p></td>
<td><p>確認が完了していないエイリアスの横には、</p></td>
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

 

リンクコレクションの配列では、次の定義が保持されます。

<a href="" id="parent"></a>**所属**  
リンクコレクションの*親*は、コレクションの最上位階層のコレクションの直下にあるコレクションです。 リンクコレクションには1つの親があります。 リンクノードの**親**メンバーは、リンクコレクション配列内の親のインデックスを指定します。

<a href="" id="children"></a>**子供**  
リンクコレクションは、その親の*子*です。 親は、0個以上の子を持つことができます。 リンクノードの**numberofchildren**メンバーは、親が持つ子の数を指定します。

<a href="" id="sibling"></a>**同列**  
親の子は*兄弟*です。

<a href="" id="next-sibling"></a>**次の兄弟**  
兄弟は左から右に並べられます。 兄弟の*次の兄弟*は、兄弟のセット内の右側の兄弟 (存在する場合) です。 リンクコレクションノードの**nextsibling**メンバーは、リンクコレクション配列内の次の兄弟のインデックスを指定します。 リンクコレクションノードに次の兄弟がない場合、 **nextsibling**は0に設定されます。

<a href="" id="first-child"></a>**最初の子**  
*最初の子*は、兄弟のセット内の左端の兄弟です。 リンクコレクションノードの**firstchild**メンバーは、リンクコレクション配列内の最初の子のインデックスを指定します。 リンクコレクションノードに子がない場合は、 **Firstchild**が0に設定されます。

アプリケーションまたはドライバーでは、親コレクションの子をすべて特定できます。これは、親の最初の子から始まり、兄弟ノードの**nextsibling**メンバーがゼロになるまで、最初の子の兄弟を通じてシーケンス処理を行います。

次のコードは、リンクコレクションノードのインデックスを使用して、リンクコレクションの最初の子を検索する方法7を示しています。

```cpp
HIDP_LINK_COLLECTION_NODE Collection[10] ;
HIDP_LINK_COLLECTION_NODE Node1 ;
 
Node1 = Collection[Collection[7].FirstChild]] ;
```

### <a href="" id="aliased-collections"></a>エイリアスを持つコレクション

区切り記号の項目は、一連のエイリアスが設定された*コレクション*を区切るためにレポート記述子で使用できます。 エイリアス化された各コレクションは、エイリアスリンクコレクションノードによって表されます。 *N*、 *n* &gt;= 2 の完全で一意なセットは、次の方法でリンクされます。

-   エイリアスが付けられたノードは、リンクコレクションの配列の連続する順序になっています。

-   最初の*n*-1 ノードでは、 **isalias**メンバーが**TRUE**に設定されています。 このようなシーケンスの直後にある*n 番目*のノードでは、 **isalias**メンバーが**FALSE**に設定されています。 このノードは、エイリアス化されたノードのシーケンスを終了します。 このノードに関連付けられている使用法は、推奨される使用方法です。

アプリケーションまたはドライバーは、このようなシーケンスを検索するために、リンクコレクション配列の配列インデックスを繰り返しインクリメントすることで、どのコレクションがエイリアス化されているかを判断できます。

[ボタン機能配列](button-capability-arrays.md)と[値機能配列](value-capability-arrays.md)は、記述されている各使用法について、使用法を含むリンクコレクションを識別します。 リンクコレクションに別名が設定されている場合は、機能配列によって、優先される使用法が指定されます。

 

 





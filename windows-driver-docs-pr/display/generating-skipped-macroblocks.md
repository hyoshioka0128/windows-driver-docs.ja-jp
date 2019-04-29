---
title: スキップされたマクロブロックの生成
description: スキップされたマクロブロックの生成
ms.assetid: 98ea004b-347d-4299-a23c-da0a9d0e844f
keywords:
- マクロ ブロック WDK DirectX va なので、マクロ ブロックをスキップします。
- WDK DirectX VA マクロ ブロックをスキップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28852808309a5fbda66c7f7d546b710ebe033601
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391251"
---
# <a name="generating-skipped-macroblocks"></a>スキップされたマクロブロックの生成


## <span id="ddk_generating_skipped_macroblocks_gg"></span><span id="DDK_GENERATING_SKIPPED_MACROBLOCKS_GG"></span>


DirectX VA でスキップされたマクロ ブロックの生成とは若干異なっている mpeg-2 ビデオ セクション 7.6.6 します。 DirectX VA で上記 nonskipped マクロ ブロックの型から推論されるのではなく、別のマクロ ブロック コントロール コマンドでは、スキップされたマクロ ブロックが生成され、(たとえば、mpeg-2、スキップを生成するメソッドで画像の種類が表示されます。マクロ ブロックは、画像がかどうかによって異なります、 *P 画像*または*B 画像*)。

マクロ ブロックをスキップの生成と使用時に、次の条件が必要です。

- スキップされたマクロ ブロックには、残存の相違点はあるありません。

- スキップされたマクロ ブロックは、インクリメントしたマクロ ブロック制御コマンドの操作を繰り返すことによって生成できます**wMBaddress**します。 (の値のインクリメントを除く、各後続のスキップされたマクロ ブロックが、1 番目と同じ方法で生成された**wMBaddress**)。

- 画像のマクロ ブロックの新しい行に折り返しから制限されますマクロ ブロックをスキップしています。 (別のマクロ ブロック コントロールのコマンドはマクロ ブロックの行の最初のマクロ ブロックを生成する送信する必要があります)。

- 以外の値を持つマクロ ブロック コントロール コマンドのコンテンツ*MBskipsFollowing*と同じです (の値を除く*MBskipsFollowing*) 最初の明示的に指定のコンテンツを一連のスキップされたマクロ ブロックに対して使用します。 したがって、たびに*MBskipsFollowing*が 0、次の構造体のメンバーと、変数する必要がありますすべて 0 を指定します。*Motion4MV、IntraMacroblock、* **wPatternCode**<em>、および</em> **wPC\_Overflow**します。

最初の 3 つのため上記の条件、アクセラレータは動き補正を実装できます (ときに*Motion4MV*は 0 です) で次の式と等しくない幅の四角形に指定されたモーションのベクトルを適用することで、輝度コンポーネント、およびクロミナンス コンポーネントで同様に指定した四角形にします。 この四角形領域のモーション補正メソッドを使用してではなく、アクセラレータで実行できる*MBskipsFollowing*同じマクロ ブロック コントロールの操作の繰り返しを +1。

```cpp
(bMacroblockWidthMinus1+1) X (MBskipsFollowing+1)
```

**BMacroblockWidthMinus1**にメンバーが含まれている[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)します。 *MBskipsFollowing*変数は、 **wMBtype**各マクロ ブロック コントロールの構造体のメンバー。

### <a name="span-idskippedmacroblocksinh263annexfspanspan-idskippedmacroblocksinh263annexfspanspan-idskippedmacroblocksinh263annexfspanskipped-macroblocks-in-h263-annex-f"></a><span id="Skipped_Macroblocks_in_H.263__Annex_F_"></span><span id="skipped_macroblocks_in_h.263__annex_f_"></span><span id="SKIPPED_MACROBLOCKS_IN_H.263__ANNEX_F_"></span>H.263 (付録 F) でスキップされたマクロ ブロック

高度な予測のモードのアクティブな (Annex F) H.263 でスキップされたマクロ ブロックの生成は、DirectX VA マクロ ブロック コントロール コマンドで nonskipped マクロ ブロックとしていくつかスキップされたマクロ ブロックを表す必要があります。 生成するためにこれは、 *OBMC*これらのマクロ ブロックに影響します。

### <a name="span-idgeneratingskippedmacroblocksinmpeg-2examplespanspan-idgeneratingskippedmacroblocksinmpeg-2examplespanspan-idgeneratingskippedmacroblocksinmpeg-2examplespangenerating-skipped-macroblocks-in-mpeg-2-example"></a><span id="Generating_Skipped_Macroblocks_in_MPEG-2_Example"></span><span id="generating_skipped_macroblocks_in_mpeg-2_example"></span><span id="GENERATING_SKIPPED_MACROBLOCKS_IN_MPEG-2_EXAMPLE"></span>Mpeg-2 の例ではスキップされたマクロ ブロックを生成します。

次の例では、スキップされたマクロ ブロックが生成されたときにマクロ ブロック制御コマンドを使用する方法を示します。 デモンストレーションの目的で、mpeg-2 ビット ストリームで 7 つのマクロ ブロックは次のように使用を想定しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ ブロック数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>残存の違いをコード化されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>スキップされました</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>残存の違いをコード化されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>スキップされました</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>スキップされました</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>スキップされました</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>残存の違いをコード化されました。</p></td>
</tr>
</tbody>
</table>

 

これらの 7 つのマクロ ブロックには、世代が必要です (少なくとも) の次の表に示すように 5 つの DirectX VA マクロ ブロック コントロール コマンド。 *MBskipsFollowing*変数がスキップされたマクロ ブロックの数を示します。 **WMBaddress**メンバーは、マクロ ブロックのアドレスを示します。 *MBskipsFollowing*と**wMBaddress**に含まれる、 [ **DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563997)、および[ **DXVA\_MBctrl\_P\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563993)構造体。 (、 *MBskipsFollowing*で変数が定義されている、 **dwMB\_SNL**構造体のメンバーです)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ ブロックのコマンド</th>
<th align="left">メンバーの値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>First</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 0</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>第 2 週</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 1</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>サードパーティ</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 2</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4 番目</p></td>
<td align="left"><p><strong>wMBaddress</strong> 3 を =</p>
<p><em>MBskipsFollowing</em> = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5 番目</p></td>
<td align="left"><p><strong>wMBaddress</strong> 6 を =</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
</tbody>
</table>

 

 

 






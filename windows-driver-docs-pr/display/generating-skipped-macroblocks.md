---
title: スキップされたマクロブロックを生成しています
description: スキップされたマクロブロックを生成しています
ms.assetid: 98ea004b-347d-4299-a23c-da0a9d0e844f
keywords:
- マクロが WDK DirectX VA をブロックし、スキップされたマクロブロック
- スキップされたマクロブロック WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 277daf1a98a0c8c9dab8af5df59706634804b2dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839680"
---
# <a name="generating-skipped-macroblocks"></a>スキップされたマクロブロックを生成しています


## <span id="ddk_generating_skipped_macroblocks_gg"></span><span id="DDK_GENERATING_SKIPPED_MACROBLOCKS_GG"></span>


DirectX VA でスキップされたマクロブロックの生成は、MPEG 2 ビデオセクション7.6.6 の部分とは多少異なります。 DirectX VA では、スキップされたマクロブロックは、前のスキップされたマクロブロックの型から推論されるのではなく、別のマクロブロックコントロールコマンドで生成されます。たとえば、MPEG 2 では、スキップを生成する方法ですマクロブロックは、画像が*P 画像*と*B 画像*のどちらであるかによって異なります)。

スキップされたマクロブロックを生成して使用する場合は、次の条件が必要です。

- スキップされたマクロブロックには、残存点の違いはありません。

- スキップされたマクロブロックは、 **Wmbaddress**をインクリメントしたマクロブロックコントロールコマンドの操作を繰り返すことによって生成できます。 ( **Wmbaddress**の値をインクリメントする場合を除き、後続のスキップされたマクロブロックは1つ目と同じ方法で生成されます)。

- マクロブロックのスキップは、画像のマクロブロックの新しい行へのラップから制限されています。 (マクロブロックの各行の最初のマクロブロックを生成するには、別のマクロブロックコントロールコマンドを送信する必要があります)。

- *Mbskipsfollowing* 0 以外の値を持つマクロブロックコントロールコマンドの内容は、一連のスキップされたマクロブロックの最初の仕様の内容に相当します ( *Mbskipsfollowing*の値を除く)。 したがって、 *Mbskipsfollowing*の値が0ではない場合、次の構造体のメンバーと変数はすべてゼロに等しくなければなりません: *Motion4MV、IntraMacroblock、* **wpattern コード**<em>、</em> **wpc\_Overflow**。

最初の3つの条件のため、アクセラレータは、輝度コンポーネントの次の式と等しい幅の四角形に、指定されたモーションベクトルを適用することにより、モーション補正 ( *Motion4MV*がゼロの場合) を実装することがあります。クロミナンスコンポーネント内の同様に指定された四角形。 この四角形領域モーション補正メソッドは、同じマクロブロック制御操作の*Mbskipsfollowing*+ 1 回の繰り返しを使用するのではなく、アクセラレータによって実行できます。

```cpp
(bMacroblockWidthMinus1+1) X (MBskipsFollowing+1)
```

**BMacroblockWidthMinus1**メンバーは、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)に含まれています。 *Mbskipsfollowing*の変数は、各マクロブロック制御構造の**wmbtype**メンバーに含まれています。

### <a name="span-idskipped_macroblocks_in_h263__annex_f_spanspan-idskipped_macroblocks_in_h263__annex_f_spanspan-idskipped_macroblocks_in_h263__annex_f_spanskipped-macroblocks-in-h263-annex-f"></a><span id="Skipped_Macroblocks_in_H.263__Annex_F_"></span><span id="skipped_macroblocks_in_h.263__annex_f_"></span><span id="SKIPPED_MACROBLOCKS_IN_H.263__ANNEX_F_"></span>をスキップしました。263のマクロブロック (付属 F)

高度な予測モードがアクティブ (付属物 F) である、263内のスキップされたマクロブロックの生成では、一部のスキップされたマクロブロックを DirectX VA マクロブロック制御コマンドの非スキップマクロブロックとして表す必要があります。 これは、これらのマクロブロック内で*Obmc*効果を生成するために行われます。

### <a name="span-idgenerating_skipped_macroblocks_in_mpeg-2_examplespanspan-idgenerating_skipped_macroblocks_in_mpeg-2_examplespanspan-idgenerating_skipped_macroblocks_in_mpeg-2_examplespangenerating-skipped-macroblocks-in-mpeg-2-example"></a><span id="Generating_Skipped_Macroblocks_in_MPEG-2_Example"></span><span id="generating_skipped_macroblocks_in_mpeg-2_example"></span><span id="GENERATING_SKIPPED_MACROBLOCKS_IN_MPEG-2_EXAMPLE"></span>MPEG-2 の例でスキップされたマクロブロックを生成する

次の例は、スキップされたマクロブロックが生成されたときに、マクロブロックコントロールコマンドを使用する方法を示しています。 デモンストレーションを目的として、MPEG 2 ビットストリーム7マクロブロックで次のように使用するとします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロブロック番号</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>残余差でコード化</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>Skipped</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>残余差でコード化</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>Skipped</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>Skipped</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>Skipped</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>残余差でコード化</p></td>
</tr>
</tbody>
</table>

 

これら7つのマクロブロックには、次の表に示すように、5つの DirectX VA マクロブロックコントロールコマンドの生成 (少なくとも) が必要です。 *Mbskipsfollowing*の変数は、スキップされたマクロブロックの数を示します。 **Wmbaddress**メンバーは、マクロブロックのアドレスを示します。 *Mbskipsfollowing*と**Wmbaddress**は、 [**DXVA\_Mbctrl\_P\_offhostidct\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)、および[**DXVA\_Mbctrl\_p\_hostresiddiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)構造体に含まれています。 ( *Mbskipsfollowing*の変数は、 **DWMB\_SNL**構造体メンバーで定義されています)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロブロックコマンド</th>
<th align="left">メンバーの値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>最初の</p></td>
<td align="left"><p><strong>Wmbaddress</strong> = 0</p>
<p><em>Mbskipsfollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>秒</p></td>
<td align="left"><p><strong>Wmbaddress</strong> = 1</p>
<p><em>Mbskipsfollowing</em> = 0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>サード</p></td>
<td align="left"><p><strong>Wmbaddress</strong> = 2</p>
<p><em>Mbskipsfollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>つ</p></td>
<td align="left"><p><strong>Wmbaddress</strong> = 3</p>
<p><em>Mbskipsfollowing の</em>= 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>個</p></td>
<td align="left"><p><strong>Wmbaddress</strong> = 6</p>
<p><em>Mbskipsfollowing</em> = 0</p></td>
</tr>
</tbody>
</table>

 

 

 






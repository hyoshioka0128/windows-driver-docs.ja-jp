---
title: マクロブロック制御コマンド構造の最初の部分
description: マクロブロック制御コマンド構造の最初の部分
ms.assetid: b282adac-3bf3-4477-a817-371d37b174a5
keywords:
- マクロ ブロック WDK DirectX va なので、汎用的なコマンド構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410ac772bd3a765585fe5c4f592aa2e6b8b9896b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369863"
---
# <a name="first-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の最初の部分


## <span id="ddk_first_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FIRST_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


ジェネリックのマクロ ブロック コントロール コマンド構造体の最初の 4 つのメンバーは、常に同じです。 次の表では、この構造体の最初の部分のメンバーについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wMBaddress</strong></p></td>
<td align="left"><p>現在処理中のマクロ ブロックのマクロ ブロックのアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wMBtype</strong></p></td>
<td align="left"><p>処理中のマクロ ブロックの種類を指定します。 このメンバーには、マクロ ブロックの値を予測する動き補正を使用するかどうかと、どの種類の違いの残存データが送信されることを示すフラグが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwMB_SNL</strong></p></td>
<td align="left"><p>2 つのフィールドが含まれています<em>MBskipsFollowing</em> (で上限の 8 ビット) および<em>MBdataLocation</em> (下位 24 ビット) にします。</p>
<p><em>MBskipsFollowing</em>を現在のマクロ ブロックの後に生成するマクロ ブロックをスキップした数を指定します。</p>
<p><em>MBdataLocation</em> IDCT 残存違いブロック データ バッファーに、データは、現在のマクロ ブロックのブロックの残存の相違の位置を示すインデックスします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wPatternCode</strong></p></td>
<td align="left"><p>残存の違いのデータをマクロ ブロック内の各ブロックに送信するかどうかを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idwmbaddressspanspan-idwmbaddressspanspan-idwmbaddressspanwmbaddress"></a><span id="wMBaddress"></span><span id="wmbaddress"></span><span id="WMBADDRESS"></span>wMBaddress

**WMBaddress**構造体のメンバーは、ラスター スキャンの順序で現在のマクロ ブロックのマクロ ブロックのアドレスを指定します。 次の表では、マクロ ブロックのアドレスの例を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ ブロック</th>
<th align="left">Address</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左</p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p>右上</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>左下</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong>+1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>右下</p></td>
<td align="left"><p>(<strong>wPicHeightInMBminus1</strong>+1) x (<strong>wPicWidthInMBminus1</strong>+1) - 1</p></td>
</tr>
</tbody>
</table>

 

**WPicWidthInMBminus1**と**wPicHeightInMBminus1**アドレスのメンバーである、 [ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造体。

### <a name="span-idwmbtypespanspan-idwmbtypespanspan-idwmbtypespanwmbtype"></a><span id="wMBtype"></span><span id="wmbtype"></span><span id="WMBTYPE"></span>wMBtype

**WMBtype**構造体のメンバーが処理されているマクロ ブロックの種類を指定します。 このメンバーには一連の方法のマクロ ブロックを定義するビットと動きベクトルが処理されます。 **BPic4MVallowed**、 **bPicScanMethod**、 **bPicBackwardPrediction**、 **bPicStructure**、および**bPicScanFixed**アドレスのメンバーである、 [ **DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造体。 **BConfigHostInverseScan**アドレスのメンバーである、 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>15 ~ 12</p></td>
<td align="left"><p><em>MvertFieldSel_3</em> (15、最上位ビット) を通じて<em>MvertFieldSel</em>0 (12 ビット)</p>
<p>マクロ ブロック コントロール コマンドの次の表に示したように後で送信される対応する動きベクトルの垂直方向のフィールドの選択を指定します。 (たとえば、H.261 と H.263) のフレームの画像構造でのモーションをフレーム ベースのこれらのビットすべてゼロなければなりません。 内のビット<em>MvertFieldSel_0、MvertFieldSel_1、MvertFieldSel_2、</em>と<em>MvertFieldSel_3</em> motion_vertical_field_select [r] [s] セクション 6.3.17.2 mpeg-2 のビットに対応しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>予約済みのビット。 0 にする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p><em>HostResidDiff</em></p>
<p>デコードされたドメイン空間残存違いブロックが送信されるかどうか、または現在のマクロ ブロックのオフホスト IDCT の変換係数を送信するかどうかを指定します。 場合は 0 にする必要があります<strong>bConfigResidDiffHost</strong>は 0 です。 場合 1 をする必要があります<strong>bConfigResidDiffAccelerator</strong>は 0 です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9、8</p></td>
<td align="left"><p><em>MotionType</em></p>
<p>図では、アニメーションの種類を指定します。 たとえば、(H.261) のように、フレームの画像構造でのモーションをフレーム ベースのビット 9 は、1 と第 8 ビットはゼロである必要があります。</p>
<p>これらのビットの使用の使用に直接対応、 <em>frame_motion_type</em>または<em>field_motion_type</em>セクション 6.3.17.1 およびテーブルの 6-17 とこれらのビットが mpeg-2 ビデオ標準の 6-18 ビットmpeg-2 のビット ストリームに存在します。 この表の後、これらのビットを使用がさらに説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7 および 6</p></td>
<td align="left"><p><em>MBscanMethod</em></p>
<p>マクロ ブロックの scan メソッドを指定します。 これと同じである必要があります<strong>bPicScanMethod</strong>場合<strong>bPicScanFixed</strong>は 1 です。 場合<em>HostResidDiff</em> 1 で、この変数は意味を持たず、これらのビットを 0 に設定する必要があります。</p>
<p>場合<strong>bConfigHostInverseScan</strong>ゼロ、 <em>MBscanMethod</em>値は次のいずれかを指定する必要があります。</p>
<ul>
<li><p>6 ビットがゼロ、ビット 7 はジグザグ スキャン (mpeg-2 図 7-2) のゼロ</p></li>
<li><p>6 ビットが 1 と 7 ビットが 0 の代替垂直スキャン (mpeg-2 図 7-3)</p></li>
<li><p>6 ビットが 0 と 7 のビットが 1 のスキャンを代替水平 (H.263 図 I.2 の一部を)</p></li>
</ul>
<p>場合<strong>bConfigHostInverseScan</strong>は 1 です。 <em>MBscanMethod</em>次の値と等しくする必要があります。</p>
<ul>
<li><p>6 ビットが 1 で、ビット 7 は係数の絶対アドレスを使用して任意のスキャンの 1 です。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p><em>FieldResidual</em></p>
<p>残存の違いのブロックが mpeg-2 で指定されているフィールド IDCT 構造体を使用するかどうかを示します。</p>
<p>場合、このフラグは 1 をする必要があります<strong>bPicStructure</strong>が 1 または 2 です。 このフラグは mpeg-2 場合に使用する場合、0 である必要があります、 <em>frame_pred_frame_DCT</em> mpeg-2 構文のフラグは 1 です。 このフラグでなければなりません、 <em>dct_type</em> mpeg-2 場合に使用する場合は、mpeg-2 構文の要素<em>dct_type</em>マクロ ブロックに存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><em>H261LoopFilter</em></p>
<p>H.261 ループ フィルター (セクション 3.2.3 H.261 の) が現在のマクロ ブロック予測アクティブかどうかを指定します。 H.261 ループのフィルターとは分離 ¼, ½, ¼ フィルターに適用される両方水平および垂直に H.261 マクロ ブロックでは、内のすべての 6 つのブロックを除く、タップのいずれかのどこブロックの外側に当てはまるブロックにします。 係数 0、1、0 に、フィルターを変更する、このような場合。 完全な算術演算の精度は、2 D のフィルター処理 (整数値の半分以上の値が切り上げ中) の出力の 8 ビット整数に丸めを適用した保持されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><em>Motion4MV</em></p>
<p>H.263 別冊 F および j. で使用されるよう、前進が、マクロ ブロックの 4 つの明るさブロックごとに個別の動きベクトルを使用することを示します<em>Motion4MV</em>場合は 0 にする必要があります<em>MotionForward</em>ゼロ場合<strong>bPic4MVallowed</strong>は 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><em>MotionBackward</em></p>
<p>この変数の使用に対して、対応する指定された<em>macroblock_motion_backward</em> mpeg-2 内のパラメーター。 場合、 <strong>bPicBackwardPrediction</strong> DXVA_PictureParameters 構造体のメンバーは 0、 <em>MotionBackward</em> 0 にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><em>MotionForward</em></p>
<p>この変数の使用に対して、対応する指定された<em>macroblock_motion_forward</em> mpeg-2 でします。 このビットの使用はさらに次の表に続くテキストでについて説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p><em>IntraMacroblock</em></p>
<p>内に、マクロ ブロックがコード化されたことと、現在のマクロ ブロックの動きベクトルが使用されていないことを示します。</p>
<p>この変数に対応して、 <em>macroblock_intra</em> mpeg-2 変数。 このビットの使用はさらに次の表に続くテキストでについて説明します。</p></td>
</tr>
</tbody>
</table>

 

マクロ ブロックは、コード化された、ときに動きベクトルの値に関連付けられています。 フィールドのコード化されたまたはフレームのコード化された画像のマクロ ブロックを使用するかどうかに基づいて、値が生成されます。 適切に考慮されます (特に、フィールドの構造化の画像またはデュアル素数モーション) の使用率が低いマクロ ブロックの種類ごとに任意の実装用に重要です。

このセクションでは次の 2 つのテーブルの有効な組み合わせを示す*IntraMacroblock*、 *MotionForward*、 *MotionBackward*、 *MotionType*、 *MvertFieldSel*、および**MVector**フレーム-コード化されたおよびフィールド-コード化された画像。 **MVector**動きベクトルの水平および垂直方向のコンポーネントが含まれます。 残りの変数とフラグは、動きベクトルへの操作を指定します。 これは、マクロ ブロックの処理の種類とフレームのコード化されたまたはフィールド-コード化された画像のマクロ ブロックを使用されているかどうかに従って決定されます。

(このセクションでは、次の表に示した値は、次の条件が発生します。

-   *H261LoopFilter*、 *Motion4MV*、および**bPicOBMC**は 0。

-   *PicCurrentField*フラグはしない限り、0 **bPicStructure** 2 (下部にあるフィールド) です。 この場合、 *PicCurrentField*は 1 です。

**MVector**のメンバーである、 [ **DXVA\_MBctrl\_P\_HostResidDiff\_1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)と[ **DXVA\_MBctrl\_P\_OffHostIDCT\_1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)構造体。 *IntraMacroblock*、 *MotionForward*、 *MotionBackward*、 *MotionType*、 *MvertFieldSel*、 *H261LoopFilter*、および*Motion4MV*フラグと変数は、ビット フィールドに含まれている、 **wMBtype**メンバーは、DXVA の\_MBctrl\_P\_HostResidDiff\_1 と DXVA\_MBctrl\_P\_OffHostIDCT\_1 構造体。 **bPicOBMC**のメンバーである、 [ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造体。 *PicCurrentField*フラグがから派生した、 **bPicStructure**の DXVA メンバー\_PictureParameters します。

このセクションでは、次の表を確認する際に、次の考慮事項が適用されます。

-   さまざまな場所、mpeg-2 変数名で*PMV*動きベクトルの値を示すために使用します。 この表記が識別するために使用、 *PMV*フレームの座標、および可能性がある場合 (つまり、半分垂直方向の解像度) でフィールドの座標で動きベクトルである mpeg-2 で定義されている変数。 すべてのケースで*PMV*の値を指す*後 PMV* (で指定されている mpeg-2 ビデオ セクション 7.6.3.1) として現在の動きベクトルの値で更新されています。

-   ベクターの定義 '\[2\]\[0\]とベクター'\[3\]\[0\] mpeg-2 セクション内にある 7.6.3.6 します。 左 **-** 表示シフト演算は、フレームの座標を垂直方向のコンポーネントが変更されることを示します。

-   両方の「場合、モーション」(0,0,0) の場合、マクロ ブロック パラメーターは、モーションの値が 0 のベクターで前方予測マクロ ブロック (0,1,0) をエミュレートします。 (Mpeg-2 セクション 7.6.3.5 も参照してください)。

-   用に表示される値*MotionType*は単一引用符で囲まれたバイナリ表現です (最初の数値がビット 9、および、2 つ目は 8 ビット)。

-   最初の表の左シフト演算子は、2 番目の値にのみ適用されます。

### <a name="span-idframe-structuredpicturesspanspan-idframe-structuredpicturesspanspan-idframe-structuredpicturesspanframe-structured-pictures"></a><span id="Frame-Structured_Pictures"></span><span id="frame-structured_pictures"></span><span id="FRAME-STRUCTURED_PICTURES"></span>画像をフレーム構造

次の表に、有効な画像をフレーム構造の要素の設定の組み合わせ (ときに、 **bPicStructure**のメンバー、 [ **DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造が 3 に等しい)。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IntraMacroblock、MotionForward、MotionBackward</th>
<th align="left">MotionType (意味は、画像の種類によって異なります)</th>
<th align="left">[0] MVector MvertFieldSel_0 (1 日、dir1)</th>
<th align="left">[1] MVector MvertFieldSel_1 (1 日、ディレクトリ 2)</th>
<th align="left">[2] の MVector MvertFieldSel_2 (2 番目、dir1)</th>
<th align="left">[3] の MVector MvertFieldSel_3 (2 つ目は、ディレクトリ 2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1,0,0 (内)</p></td>
<td align="left"><p>' 00' (内)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,0 (モーションなし)</p></td>
<td align="left"><p>' 10' (モーションなし)</p></td>
<td align="left"><p>0</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>' 10' (フレーム MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>' 10' (フレーム MC)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>' 10' (フレーム MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>' 01' (フィールド MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>[1] [0] の選択</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>' 01' (フィールド MC)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>' 01' (フィールド MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>[1] [0] の選択</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>' 11' (デュアル素数)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<div>
 
</div>
<p>0 (上)</p></td>
<td align="left"><p>ベクター ' [2] [0] [0]</p>
<div>
 
</div>
ベクター ' [2] [0] [1]&lt;&lt;1
<p>1 (下)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<div>
 
</div>
<p>1</p></td>
<td align="left"><p>ベクター ' [3] [0] [0]</p>
<div>
 
</div>
ベクター ' [3] [0] [1]&lt;&lt;1
<p>0</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfield-structuredpicturesspanspan-idfield-structuredpicturesspanspan-idfield-structuredpicturesspanfield-structured-pictures"></a><span id="Field-Structured_Pictures"></span><span id="field-structured_pictures"></span><span id="FIELD-STRUCTURED_PICTURES"></span>フィールドの構造化の画像

次の表に、有効なフィールド構造の図の要素の設定の組み合わせ (ときに、 **bPicStructure**のメンバー、 [ **DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)構造体が 1 または 2 と等しい)。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IntraMacroblock、MotionForward、MotionBackward</th>
<th align="left">MotionType (意味は、画像の種類によって異なります)</th>
<th align="left">[0] MVector MvertFieldSel_0 (1 日、dir1)</th>
<th align="left">[1] MVector MvertFieldSel_1 (1 日、ディレクトリ 2)</th>
<th align="left">[2] の MVector MvertFieldSel_2 (2 番目、dir1)</th>
<th align="left">[3] の MVector MvertFieldSel_3 (2 つ目は、ディレクトリ 2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1,0,0 (内)</p></td>
<td align="left"><p>' 00' (内)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,0 (モーションなし)</p></td>
<td align="left"><p>' 01' (モーションなし)</p></td>
<td align="left"><p>0</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>' 01' (フィールド MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>' 01' (フィールド MC)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>' 01' (フィールド MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>' 10' (16 x 8 MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>[1] [0] の選択</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>' 10' (16 x 8 MC)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>' 10' (16 x 8 MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>[1] [0] の選択</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>' 11' (デュアル素数)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>ベクター ' [2] [0]</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalvalidelementsettingsforfieldandframepicturesspanspan-idadditionalvalidelementsettingsforfieldandframepicturesspanspan-idadditionalvalidelementsettingsforfieldandframepicturesspanadditional-valid-element-settings-for-field-and-frame-pictures"></a><span id="Additional_Valid_Element_Settings_for_Field_and_Frame_Pictures"></span><span id="additional_valid_element_settings_for_field_and_frame_pictures"></span><span id="ADDITIONAL_VALID_ELEMENT_SETTINGS_FOR_FIELD_AND_FRAME_PICTURES"></span>フィールドおよびフレームの画像の追加の要素が有効な設定

フレーム構造およびフィールド構造の画像の許可されている残りのケースは、次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>H261LoopFilter</em> = 1</p>
<p><strong>bPicOBMC</strong> = 0</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>その 1 つの前方動きベクトル送信されることを示します<strong>MVector</strong>[0] H.261 ループのフィルターがアクティブで、マクロ ブロックで前方の予測であるとします。</p>
<p><em>MotionForward</em> 1 をここである必要がありますと<em>IntraMacroblock</em>と<em>MotionBackward</em>どちらもゼロがある必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong> = 0</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>4 つの前方動きベクトル送信されることを示します<strong>MVector</strong>[0] から<strong>MVector</strong>[3]。 <em>MotionForward</em> 1 をここである必要がありますと<em>IntraMacroblock</em> 0 にする必要があります。</p>
<p>場合<em>MotionBackward</em> 1、5 番目は、旧バージョンとの予測に動きベクトルが送信される<strong>MVector</strong>[4]。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>bPicOBMC</em></strong>  = 1</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>10 前方動きベクトル送信されることを示します<strong>MVector</strong>[0] から<strong>MVector</strong>[9] OBMC の仕様、モーション センサーとの最初の 4 はこのような値がベクトルをモーションがすべて等しい。</p>
<p>場合<em>MotionBackward</em> 1 に設定されて、11 番目の旧バージョンと予測の動きベクトルが送信される<strong>MVector</strong>[10]。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong> = 1</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>10 の前方動きベクトル送信されることを示します<strong>MVector</strong>[0] から<strong>MVector</strong>[9] OBMC の仕様の動き、および最初の 4 はこのような値がベクトルをモーションがからそれぞれ異なる場合がありますその他。</p>
<p>場合<em>MotionBackward</em> 1 に設定されて、11 番目の旧バージョンと予測の動きベクトルが送信される<strong>MVector</strong>[10]。</p></td>
</tr>
</tbody>
</table>

 

**注**   average 演算子は数学的に同じです ((s1 s2、+ 1)&gt;&gt;1)、mpeg-1 mpeg-2 半分サンプルの予測をフィルター処理、双方向平均、およびデュアル素数同じ逆パリティの結合. H.263 双方向の平均化演算子は、右シフトする前に +1 のオフセットを追加できません。 **BBidirectionalAveragingMode**のメンバー [ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)使用がどちらの方法を決定します。

 

 

 






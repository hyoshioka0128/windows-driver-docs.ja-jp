---
title: マクロブロック制御コマンド構造の最初の部分
description: マクロブロック制御コマンド構造の最初の部分
ms.assetid: b282adac-3bf3-4477-a817-371d37b174a5
keywords:
- マクロは WDK DirectX VA、汎用コマンド構造をブロックします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa77e27bb9078f8ead49294ee1177f854522b3e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839693"
---
# <a name="first-part-of-macroblock-control-command-structure"></a>マクロブロック制御コマンド構造の最初の部分


## <span id="ddk_first_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FIRST_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


汎用マクロブロックコントロールコマンド構造の最初の4つのメンバーは常に同じです。 次の表では、この構造体の最初の部分のメンバーについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wMBaddress</strong></p></td>
<td align="left"><p>現在処理されているマクロブロックのマクロブロックアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wMBtype</strong></p></td>
<td align="left"><p>処理するマクロブロックの種類を指定します。 このメンバーには、マクロブロックの値を予測するためにモーション補正を使用するかどうか、およびどのような種類の残存差データが送信されるかを示すフラグが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwMB_SNL</strong></p></td>
<td align="left"><p><em>Mbskipsfollowing</em> (上位8ビット) と<em>MBdataLocation</em> (下位24ビット) の2つのフィールドが含まれています。</p>
<p><em>Mbskipsfollowing</em>は、現在のマクロブロックの後に生成されるスキップされるマクロブロックの数を指定します。</p>
<p><em>MBdataLocation</em>は、idct 残差ブロックデータバッファーへのインデックスであり、現在のマクロブロックの残存差データの場所を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Wpattern コード</strong></p></td>
<td align="left"><p>マクロブロックの各ブロックに残差のデータが送信されるかどうかを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idwmbaddressspanspan-idwmbaddressspanspan-idwmbaddressspanwmbaddress"></a><span id="wMBaddress"></span><span id="wmbaddress"></span><span id="WMBADDRESS"></span>wMBaddress

**Wmbaddress**構造体のメンバーは、ラスタースキャンの順序で現在のマクロブロックのマクロブロックアドレスを指定します。 次の表は、マクロブロックアドレスの例を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロブロック</th>
<th align="left">Address</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左上</p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p>右上</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>左下</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong>+ 1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>右下</p></td>
<td align="left"><p>(<strong>wPicHeightInMBminus1</strong>+ 1) x (<strong>wPicWidthInMBminus1</strong>+ 1)-1</p></td>
</tr>
</tbody>
</table>

 

**WPicWidthInMBminus1**と**wPicHeightInMBminus1**のアドレスは、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体のメンバーです。

### <a name="span-idwmbtypespanspan-idwmbtypespanspan-idwmbtypespanwmbtype"></a><span id="wMBtype"></span><span id="wmbtype"></span><span id="WMBTYPE"></span>wMBtype

**Wmbtype**構造体のメンバーは、処理されるマクロブロックの種類を指定します。 このメンバーには、マクロブロックとモーションベクターの処理方法を定義する一連のビットが含まれています。 **BPic4MVallowed**、 **b scanmethod**、 **bPicBackwardPrediction**、 **b Structure**、 **BDXVA Scanの各固定**アドレスは、 [ **\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体のメンバーです。 **BConfigHostInverseScan**アドレスは、 [**DXVA\_configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体のメンバーです。

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
<td align="left"><p><em>Mvertfieldsel</em>0 (ビット 12) を使用して<em>MvertFieldSel_3</em> (ビット15、最上位)</p>
<p>次の表で指定されているように、後でマクロブロックコントロールコマンドで送信される対応するモーションベクターの垂直方向のフィールド選択を指定します。 フレームの画像構造を使用したフレームベースのモーションの場合 (たとえば、たとえば、たとえば、-261 と-263)、これらのビットはすべてゼロである必要があります。 <em>MvertFieldSel_0、MvertFieldSel_1、MvertFieldSel_2、</em>および<em>MvertFieldSel_3</em>のビットは、6.3.17.2 のセクションの [r] [s] ビット motion_vertical_field_select に対応しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>予約済みビット。 0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p><em>HostResidDiff</em></p>
<p>空間ドメインの残りの、デコードされたブロックが送信されるかどうか、または現在のマクロブロックのオフホスト IDCT に対して変換係数を送信するかどうかを指定します。 <strong>BConfigResidDiffHost</strong>が0の場合は0にする必要があります。 <strong>BConfigResidDiffAccelerator</strong>が0の場合、は1である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9と8</p></td>
<td align="left"><p><em>MotionType</em></p>
<p>画像のモーションの種類を指定します。 たとえば、フレーム画像構造を使用したフレームベースのモーションの場合 (例: のように)、ビット9は1、ビット8は0にする必要があります。</p>
<p>これらのビットは、MPEG-2 ビットストリームにこれらのビットが含まれている場合に、セクション6.3.17.1 と、MPEG-2 ビデオ標準の表6-17 および6-18 での<em>frame_motion_type</em>または<em>field_motion_type</em>の使用に直接対応します。 これらのビットの使用方法については、次の表で詳しく説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7および6</p></td>
<td align="left"><p><em>MBscanMethod</em></p>
<p>マクロブロックスキャンメソッドを指定します。 <strong>Bbfile Scanfixed</strong>が1の場合、この<strong>メソッドは b絵文字 scanmethod</strong>と同じである必要があります。 <em>Hostresiddiff</em>が1の場合、この変数は意味を持たず、これらのビットは0に設定する必要があります。</p>
<p><strong>BConfigHostInverseScan</strong>が0の場合、 <em>mbscanmethod</em>は次のいずれかの値である必要があります。</p>
<ul>
<li><p>ビット6がゼロで、ジグザグスキャンのビット7が0である (MPEG-2 図 7-2)</p></li>
<li><p>ビット6は1で、代替垂直スキャンの場合はビット7が0です (MPEG-2 図 7-3)</p></li>
<li><p>ビット6はゼロで、ビット7は代替水平スキャンの場合は1です (263 図 i. 2 部)</p></li>
</ul>
<p><strong>BConfigHostInverseScan</strong>が1の場合、 <em>mbscanmethod</em>は次の値と同じである必要があります。</p>
<ul>
<li><p>ビット6は1で、ビット7は、絶対係数アドレスを使用した任意のスキャンの場合は1です。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p><em>FieldResidual</em></p>
<p>残存差ブロックが MPEG-2 で指定されたフィールド IDCT 構造体を使用するかどうかを示します。</p>
<p><strong>B絵文字構造</strong>が1または2の場合、このフラグは1にする必要があります。 Mpeg-2 構文の<em>frame_pred_frame_DCT</em>フラグが1の場合、mpeg-2 に対してこのフラグが0に設定されている必要があります。 マクロブロックに<em>dct_type</em>が存在する場合、このフラグは mpeg-2 構文の<em>dct_type</em>要素と同じである必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><em>H261LoopFilter</em></p>
<p>現在のマクロブロック予測に対して、3.2.3 ループフィルター (セクションの .H) がアクティブかどうかを指定します。 -261 ループフィルターは、分離可能な1/4、1/2、1/4 フィルターであり、水平方向と垂直方向の両方に適用されます。ただし、ブロックエッジでは、タップの1つがブロックの外側にあります。 このような場合は、係数が0、1、0になるようにフィルターが変更されます。 完全な算術精度は、2-d フィルター処理の出力時に8ビットの整数に丸められて保持されます (半整数またはそれより大きい値が切り上げられます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><em>Motion4MV</em></p>
<p>前方モーションが、BPic4MVallowed で使用される、マクロブロック内の4つの輝度ブロックのそれぞれに対して個別のモーションベクターを使用することを示します。 <em>Motion4MV</em>は、 <em>motionforward</em>が0の場合、またはが0の場合は0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><em>MotionBackward</em></p>
<p>この変数は、MPEG-2 の対応する<em>macroblock_motion_backward</em>パラメーターに指定されているとおりに使用されます。 DXVA_PictureParameters 構造体の<strong>bPicBackwardPrediction</strong>メンバーがゼロの場合、 <em>motionbackward</em>を0にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><em>MotionForward</em></p>
<p>この変数は、MPEG-2 の対応する<em>macroblock_motion_forward</em>に対して指定されたとおりに使用されます。 このビットの使用方法については、この表の後のテキストで詳しく説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p><em>IntraMacroblock</em></p>
<p>マクロブロックが内部としてコード化され、現在のマクロブロックにモーションベクターが使用されないことを示します。</p>
<p>この変数は、MPEG-2 の<em>macroblock_intra</em>変数に対応します。 このビットの使用方法については、この表の後のテキストで詳しく説明します。</p></td>
</tr>
</tbody>
</table>

 

マクロブロックが predictively によってコード化されている場合は、モーションベクター値が関連付けられています。 値は、フィールドコードまたはフレームによってコード化された画像にマクロブロックが使用されているかどうかに基づいて生成されます。 すべての実装で、使用されているすべてのマクロブロック型 (特に、フィールド構造化画像またはデュアルプライムモーション) を適切に考慮することが重要です。

このセクションの次の2つの表は、 *IntraMacroblock*、 *motionforward*、 *motionforward*、 *motionforward*、 *mvertfieldsel*、および**mvector** (フレームコードおよびフィールドでコード化された画像) の有効な組み合わせを示しています。 **Mvector**には、モーションベクターの水平方向と垂直方向のコンポーネントが含まれています。 残りの変数とフラグは、モーションベクター演算を指定します。 これは、処理されたマクロブロックの種類と、フレームコードまたはフィールドでコード化された画像にマクロブロックが使用されているかどうかによって決まります。

次の表に示す値 (このセクションの) は、次の条件で発生します。

-   *H261LoopFilter*、 *Motion4MV*、 **b絵文字 obmc**はゼロです。

-   、 **B絵文字構造**が 2 (下のフィールド) でない限り、*ピクチャ*は0になります。 この例では、 *"ピクチャ" フィールド*は1です。

**Mvector**は、 [**DXVA\_mbctrl\_P\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)および[**DXVA\_Mbctrl\_P\_offhostidct\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)構造体のメンバーです。 *IntraMacroblock*、 *motionforward*、 *motionforward*、 *motionforward*、 *mvertfieldsel*、、および*Motion4MV*の各フラグと変数は、DXVA\_MBctrl\_P\_Hostresiddiff\_1 および DXVA\_mbctrl\_P\_offhostidct\_1 構造体に含ま**れてい**ます。 **BDXVA Obmc**は、 [ **\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体のメンバーです。 DXVA\_ピクチャパラメーターの**B絵文字構造体**から派生した、画像形式の*フィールド*です。

このセクションの次の表を確認する場合は、次の点に注意してください。

-   さまざまな場所で、MPEG 2 変数名*Pmv*を使用して、モーションベクターの値を示します。 この表記は、フレーム座標にある MPEG-2 で定義されている*Pmv*変数と、フィールド座標にある (つまり、半垂直解像度の) モーションベクターを区別するために使用されます。 どのような場合でも、 *Pmv*は、現在のモーションベクター値によって更新され*た後の pmv*の値を参照します (MPEG 2 video Section 7.6.3.1 で指定)。

-   Vector '\[2\]\[0\] および vector '\[3\]\[0\] の定義は、MPEG-2 セクション7.6.3.6 にあります。 左 **-** シフト操作は、垂直コンポーネントがフレーム座標に変更されたことを示します。

-   "モーションなし" の場合 (0, 0, 0)、マクロブロックパラメーターは、ゼロ値モーションベクターを使用して前方予測マクロブロック (0, 1, 0) をエミュレートします。 (「MPEG-2 セクション7.6.3.5」も参照してください)。

-   *Motiontype*を単一引用符で示す値は、バイナリ表現です (最初の数値はビット9用、2番目はビット8用)。

-   最初のテーブルの左シフト演算子は、表示されている2番目の値にのみ適用されます。

### <a name="span-idframe-structured_picturesspanspan-idframe-structured_picturesspanspan-idframe-structured_picturesspanframe-structured-pictures"></a><span id="Frame-Structured_Pictures"></span><span id="frame-structured_pictures"></span><span id="FRAME-STRUCTURED_PICTURES"></span>フレーム構造化画像

次の表は、フレーム構造化画像の要素設定の有効な組み合わせを示しています ( [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**b絵文字構造**体のメンバーが 3)。

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
<th align="left">IntraMacroblock、MotionForward、Motionforward</th>
<th align="left">MotionType (画像の種類によって異なります)</th>
<th align="left">MVector [0] MvertFieldSel_0 (1 番目、dir1)</th>
<th align="left">MVector [1] MvertFieldSel_1 (1、dir2)</th>
<th align="left">MVector [2] MvertFieldSel_2 (2 番目、dir1)</th>
<th align="left">MVector [3] MvertFieldSel_3 (2 番目、dir2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1、0、0 (内部)</p></td>
<td align="left"><p>' 00 ' (内部)</p></td>
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
<td align="left"><p>0、0、0 (動作なし)</p></td>
<td align="left"><p>' 10 ' (モーションなし)</p></td>
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
<td align="left"><p>0、1、0</p></td>
<td align="left"><p>' 10 ' (フレーム MC)</p></td>
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
<td align="left"><p>0、0、1</p></td>
<td align="left"><p>' 10 ' (フレーム MC)</p></td>
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
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>' 10 ' (フレーム MC)</p></td>
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
<td align="left"><p>0、1、0</p></td>
<td align="left"><p>' 01 ' (フィールド MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、0、1</p></td>
<td align="left"><p>' 01 ' (フィールド MC)</p></td>
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
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>' 01 ' (フィールド MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、1、0</p></td>
<td align="left"><p>' 11 ' (デュアルプライム)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<div>
 
</div>
<p>0 (上)</p></td>
<td align="left"><p>ベクター ' [2] [0] [0]、</p>
<div>
 
</div>
ベクター ' [2] [0] [1]&lt;&lt;1
<p>1 (下)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<div>
 
</div>
<p>1</p></td>
<td align="left"><p>ベクター ' [3] [0] [0]、</p>
<div>
 
</div>
ベクター ' [3] [0] [1]&lt;&lt;1
<p>0</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfield-structured_picturesspanspan-idfield-structured_picturesspanspan-idfield-structured_picturesspanfield-structured-pictures"></a><span id="Field-Structured_Pictures"></span><span id="field-structured_pictures"></span><span id="FIELD-STRUCTURED_PICTURES"></span>フィールド構造化画像

次の表は、フィールド構造化画像の要素設定の有効な組み合わせを示しています ( [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)構造体の**b 構造**体メンバーが1または2に等しい場合)。

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
<th align="left">IntraMacroblock、MotionForward、Motionforward</th>
<th align="left">MotionType (画像の種類によって異なります)</th>
<th align="left">MVector [0] MvertFieldSel_0 (1 番目、dir1)</th>
<th align="left">MVector [1] MvertFieldSel_1 (1、dir2)</th>
<th align="left">MVector [2] MvertFieldSel_2 (2 番目、dir1)</th>
<th align="left">MVector [3] MvertFieldSel_3 (2 番目、dir2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1、0、0 (内部)</p></td>
<td align="left"><p>' 00 ' (内部)</p></td>
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
<td align="left"><p>0、0、0 (動作なし)</p></td>
<td align="left"><p>' 01 ' (モーションなし)</p></td>
<td align="left"><p>0</p>
<p><em>ピクチャフィールド</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、1、0</p></td>
<td align="left"><p>' 01 ' (フィールド MC)</p></td>
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
<td align="left"><p>0、0、1</p></td>
<td align="left"><p>' 01 ' (フィールド MC)</p></td>
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
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>' 01 ' (フィールド MC)</p></td>
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
<td align="left"><p>0、1、0</p></td>
<td align="left"><p>' 10 ' (16x8 MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、0、1</p></td>
<td align="left"><p>' 10 ' (16x8 MC)</p></td>
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
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>' 10 ' (16x8 MC)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、1、0</p></td>
<td align="left"><p>' 11 ' (デュアルプライム)</p></td>
<td align="left"><p>PMV [0] [0]</p>
<p><em>ピクチャフィールド</em></p></td>
<td align="left"><p>ベクター ' [2] [0]</p>
<p><em>ピクチャフィールド</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_valid_element_settings_for_field_and_frame_picturesspanspan-idadditional_valid_element_settings_for_field_and_frame_picturesspanspan-idadditional_valid_element_settings_for_field_and_frame_picturesspanadditional-valid-element-settings-for-field-and-frame-pictures"></a><span id="Additional_Valid_Element_Settings_for_Field_and_Frame_Pictures"></span><span id="additional_valid_element_settings_for_field_and_frame_pictures"></span><span id="ADDITIONAL_VALID_ELEMENT_SETTINGS_FOR_FIELD_AND_FRAME_PICTURES"></span>フィールドおよびフレームの画像に対する追加の有効な要素の設定

フレーム構造およびフィールド構造化画像で許可される残りのケースは次のとおりです。

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
<p><strong>B絵文字 Obmc</strong> = 0</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>1つの前方モーションベクターが<strong>Mvector</strong>[0] で送信され、マクロブロック内の前方予測に対して、[-261 loop] フィルターがアクティブになっていることを示します。</p>
<p>この場合、 <em>Motionforward</em>は1である必要があります。また、 <em>IntraMacroblock</em>と<em>motionforward</em>の両方を0にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B絵文字 Obmc</strong> = 0</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>4つの前方モーションベクトルが<strong>mvector</strong>[0] から<strong>mvector</strong>[3] に送信されることを示します。 この場合、 <em>Motionforward</em>は1である必要があり、 <em>IntraMacroblock</em>はゼロである必要があります。</p>
<p><em>Motionbackward</em>が1の場合、 <strong>mvector</strong>[4] の後方予測用に5番目のモーションベクトルが送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>B絵文字 Obmc</em></strong> = 1</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>10個の前方モーションベクトルが、OBMC モーションの指定のために<strong>Mvector</strong>[0] から<strong>mvector</strong>[9] に送信され、最初の4つのモーションベクターの値がすべて等しいことを示します。</p>
<p><em>Motionbackward</em>が1の場合、11番目のモーションベクターが<strong>mvector</strong>[10] の後方予測用に送信されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B絵文字 Obmc</strong> = 1</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>10個の前方モーションベクトルが、OBMC モーションの指定のために<strong>Mvector</strong>[0] から<strong>mvector</strong>[9] の順に送信され、最初の4つのモーションベクターの値が相互に異なる場合があることを示します。</p>
<p><em>Motionbackward</em>が1の場合、11番目のモーションベクターが<strong>mvector</strong>[10] の後方予測用に送信されます。</p></td>
</tr>
</tbody>
</table>

 

**注**   average 演算子は、(s1 + s2 + 1)&gt;&gt;1)、mpeg-2、mpeg-2 ハーフサンプリングの予測フィルター、双方向平均、および2つの主要な同等のパリティの組み合わせに対しては数学的に同一です。 -263 双方向平均演算子は、右シフトの前に + 1 のオフセットを追加しません。 これらのメソッドのうち、どれを使用するかは、 [**DXVA\_ピクチャパラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)の**bBidirectionalAveragingMode**メンバーによって決まります。

 

 

 






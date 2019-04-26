---
title: 画質の制御
description: 画質の制御
ms.assetid: b6d25178-6726-4ce0-ab34-efeedc618044
keywords:
- Unidrv、画像の品質
- イメージ品質の WDK Unidrv オプションします。
- ドラフト イメージ品質 WDK Unidrv
- 画質 WDK Unidrv
- 最適な画質 WDK Unidrv
- 品質設定エントリ WDK Unidrv
- 印刷ジョブ WDK、画像の品質
- WDK のイメージ品質を書式設定します。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f993d6dc41c93c245993e2b1c841a00480dd9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358653"
---
# <a name="controlling-image-quality"></a>画質の制御





Unidrv のユーザー インターフェイスでは、印刷ジョブに対して「より優れた」または「最高の」イメージ品質をユーザーが「下書き」を選択できるようにする 3 つのラジオ ボタンのセットを提供します。 最適な品質では、その逆ドラフト品質は画像の解像度、経由でプリンターの速度を強調しています。

これらのラジオ ボタンの目的を明示的に必要なオプションを個別に選択しなくても、目的の品質を取得するために必要な機能オプションを簡単に選択できるようにします。

Unidrv はラジオ ボタンが押された場合に選択するオプションは、プリンターの GPD ファイルで指定されます。 GPD 言語では、次の 3 つのエントリを定義します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em><strong>DraftQualitySettings</strong></p></td>
</tr>
<tr class="even">
<td><p></em><strong>BetterQualitySettings</strong></p></td>
</tr>
<tr class="odd">
<td><p>*<strong>BestQualitySettings</strong></p></td>
</tr>
</tbody>
</table>

 

各エントリは、ラジオ ボタンのいずれかに関連付けられ、各エントリは、オプションの一覧を受け入れます。 ユーザーは、対応するボタンを選択する Unidrv はのリストし、指定したオプションを設定します。

各品質設定エントリの形式は次のとおりです。

\**XXXX*QualitySettings:一覧 (*FeatureName*.*OptionName*、 *FeatureName*.*OptionName*、 *FeatureName*.*OptionName*,...)

各*FeatureName*名前に関連付けられている、 \**機能*エントリ、および*OptionName*機能ののいずれかに関連付けられている名前は、\**オプション*エントリ。 空のリストは、灰色表示に関連付けられているラジオ ボタンをによりします。

追加、必要なエントリでは、既定のイメージ品質を指定します。 形式は次のとおりです。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>DefaultQuality:</strong><em>DefaultQuality</em></p></td>
</tr>
</tbody>
</table>

 

場所*DefaultQuality*の 1 つ`DRAFTQUALITY`、 `BETTERQUALITY`、または`BESTQUALITY`します。

これらの GPD ファイル エントリのどのオプションと関連付けることができます、`ColorMode`と`MediaType`機能します。 通常でそれらの[条件付きステートメント](conditional-statements.md)次の例に示すように、します。

```cpp
*switch: ColorMode {
    *case: Mono {
        *BestQualitySettings: LIST(ColorMode.Mono,
                                   Resolution.Option1,
                                   TextQuality.Option3)
        *BetterQualitySettings: LIST(ColorMode.Mono,
                                     Resolution.Option1,
                                     TextQuality.Option1)
        *DraftQualitySettings: LIST(ColorMode.Mono,
                                    Resolution.Option2,
                                    TextQuality.Option2)
        *DefaultQuality: BETTERQUALITY }
    *default: {
        *BestQualitySettings: LIST(ColorMode.24bpp,
                                   Resolution.Option2,
                                   TextQuality.Option3)
        *BetterQualitySettings: LIST(ColorMode.Color,
                                     Resolution.Option2,
                                     TextQuality.Option1)
        *DraftQualitySettings: LIST(ColorMode.Color,
                                    Resolution.Option2,
                                    TextQuality.Option2)
        *DefaultQuality: BETTERQUALITY }}
```

1 つ指定する適切な戦略は、例のように、 \***ケース**エントリを 1 つの色のモードを使用し、 \***既定**多色モードのすべてのエントリ。 これは、ため Unidrv の**ページ セットアップ**プロパティ シート ページがユーザー--カラーかモノクロ印刷の 2 つの選択肢を提供しています。 例では、形式を使用する場合、ユーザーがカラー印刷オプションを選択すると Unidrv 品質ボタン表示されます。

イメージ品質を両方の色のモードにするより複雑な例を次に、メディアの種類します。

```cpp
*switch: Colormode {
    *case: Mono {
    *switch: MediaType {
        *case: CLAYCOATED {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BESTQUALITY }
        *case: GLOSSY {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BETTERQUALITY 
        *default: 
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  DRAFTQUALITY }}}
    *default: {
    *switch: MediaType {
        *case: CLAYCOATED {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BESTQUALITY }
        *case: GLOSSY {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BETTERQUALITY }
        *default: {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  DRAFTQUALITY }}}
}
```

品質設定 GPD のエントリを使用する場合、次の規則を確認する必要があります。

-   常に 4 つすべてのエントリを使用する必要があります。 空のオプションのリストを指定することが許可され、灰色表示に関連付けられているラジオ ボタンします。

-   返さとメディアの種類のすべての組み合わせの 4 つすべてのエントリを指定する必要があります。 例を使用して、 \***既定**これを実現するために各条件付きステートメント内のエントリ。

-   品質設定エントリ内のオプション リストする必要がありますいずれかに違反しない[制約オプション](option-constraints.md)を指定します。

-   オプション リストに含まれるオプションでは、選択したメディアの種類は変更しないでください。 ですが、許容可能なたとえば、24 ビット/ピクセルの最適な品質を高画質の 8 ビット/ピクセル カラー モードと 4 を設定するビット/ピクセルのドラフトは 1 ビット/ピクセル (1 つの色) に変更していない許容できます。

パーサーが設定、機能の品質設定を指定する条件付きステートメントで、機能が含まれる場合\*UpdateQualityMacro でしょうか。 属性を**TRUE**します。 (を参照してください[属性機能](feature-attributes.md))。

 

 





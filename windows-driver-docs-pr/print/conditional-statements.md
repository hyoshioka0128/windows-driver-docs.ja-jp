---
title: 条件文
description: 条件文
ms.assetid: eea2f9c1-a73b-46ed-a778-ece6bed615ac
keywords:
- Unidrv、条件付きステートメント
- GPD ファイル WDK Unidrv、条件付きステートメント
- 条件付きステートメント WDK Unidrv
- 複数の依存関係 WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f2476cf2a96ea99b5a07a41c72a5eb16379b0c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330315"
---
# <a name="conditional-statements"></a>条件文





GPD 言語は、プリンターのプロパティをいくつかの場合は、プリンターの構成に依存を記述するための C のような条件付きステートメントを提供します。 たとえば、余白およびページのカーソルの配信元は、ページの向きに依存可能性があります。 **\*スイッチ**と **\*ケース**ステートメントを使用すると、このような依存関係を表現できます。 これらのステートメントの形式は次のとおりです。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p>
* スイッチ<em>FeatureName</em> {* ケース<em>Option1_Name</em> {} * ケース<em>Option2_Name</em> {}<em>など</em>* ケース<em>OptionN_Name</em>{} * {}} を既定値</td>
</tr>
</tbody>
</table>

 

*FeatureName* GPD ファイル内で指定されている機能の名前を指定する必要があります、 **\*機能**エントリ。 使用されるオプションの名前は、指定した機能に関連付けられているオプションである必要があります。

ページ余白とカーソルの配信元は、ページの向きに依存するケースを表現するには、次のエントリを使用できます。

```cpp
*Feature: Orientation
{
    *DefaultOption: Portrait
    *Option: Portrait
    {
        *Name: "Portrait"
        *rcIconID: =RC_ICON_PORTRAIT
    }
    *Option: LANDSCAPE_CC90
    {
        *Name: "Landscape"
        *rcIconID: =RC_ICON_LANDSCAPE
    }
}
*Feature: PaperSize
{
    *DefaultOption: Letter
    *Option: Letter
    {
        *Name: "Letter 8.5 x 11 inch"
        *switch: Orientation
        {
            *case: Portrait
            {
                *PrintableArea: PAIR(4800, 6324)
                *PrintableOrigin: PAIR(150, 150)
                *CursorOrigin: PAIR(150,100)
            }
            *case: LANDSCAPE_CC90
            {
                *PrintableArea: PAIR(4860, 6360)
                *PrintableOrigin: PAIR(120, 120)
                *CursorOrigin: PAIR(100,6480)
            }
        }
    }
}
```

この例では、プリンターのオプション**PaperSize**機能は、プリンターの選択したオプションに依存している**向き**機能します。

かどうかを指定していないすべての機能のオプションとして **\*ケース**ステートメントの引数を含めることができます、 **\*既定**ステートメントでは、C 言語と同じようにします。 すべてのオプションを含めないし、含めない場合、 **\*既定**ステートメントでは、関連する属性を評価する必要があります (例では、  **\*PrintableArea**、 \* **PrintableOrigin**、および **\*CursorOrigin**) GPD ファイルでは、上記の他の場所で、 \***スイッチ**ステートメント。

### <a href="" id="ddk-specifying-multiple-dependencies-gg"></a>複数の依存関係を指定します。

含めることができます **\*スイッチ**内のステートメント **\*ケース**と **\*既定**ステートメント。 次のように複数の依存関係を指定できます。

```cpp
*Feature: feature1 {*Option: optionA {...} *Option: optionB {...}}
*Feature: feature2 {*Option: optionC {...} *Option: optionD {...}}
*Feature: feature3 
    {*Option: optionE 
        {*Switch: feature1 
            {*Case: optionA
                 {*Switch: feature2
                     {*Case: optionD
                         {AttributeX: ValueX}
                      *Default
                         {AttributeX: ValueY}
                     }
                 }
             *Default
                  {AttributeX: ValueZ}
             }
         }
    *Option: optionF {...} 
    }
```

この例では、feature3 の optionE に属する AttributeX は feature1 と feature2 の両方に依存します。

Feature1 のオプション、feature2 の optionD optionE feature3 用に、ユーザーが選択した場合、attributeX は、値 x に設定されます。

Feature1 のオプション、feature2 の optionC optionE feature3 用に、ユーザーが選択した場合、attributeX は、ValueY に設定されます。

Feature1 の optionB と optionE feature3 用にユーザーが選択した場合、attributeX は、値 z に設定されます。 Feature2 の設定は関係ありません。

複数の依存関係を指定するときに、次の規則が適用されます。

-   1 つのスコープ内で複数の依存関係を指定する必要があります **\*スイッチ**エントリ。 例を使用して、たとえば、使うことはできません、 **\*スイッチ**その feature3 が feature1 にし、それ以降に依存していることを示すエントリに入れ子にされた **\*スイッチ**ステートメントでは、その feature3 が feature2 に依存します。

-   内で入れ子になった、同じ機能を複数回指定できない\***スイッチ**エントリ。

### <a href="" id="ddk-where-to-place-a-switch-statement-gg"></a>配置する場所、 \*Switch ステートメント

配置することができます、 **\*スイッチ**GPD ファイル内で、次の場所内のステートメント。

-   内で、\*ステートメントのオプション

-   内で、\*ステートメントの機能

-   内で、 **\*ケース**ステートメント

-   内で、 **\*既定**ステートメント

-   ファイルの最上位レベルで (つまり、かっこ内ではなく)

### <a href="" id="ddk-what-to-place-inside-switch-case-and-default-statements-gg"></a>内にどのような\*スイッチ、\*ケース、および\*ステートメントの既定

内で、 **\*スイッチ**エントリを配置できますのみ **\*ケース**と **\*既定**エントリ。

GPD ファイルのエントリの内側に配置できる **\*ケース**または **\*既定**エントリを再配置可能なエントリと呼びます。 GPD エントリの次の種類は、再配置することがあります。

-   ほとんど[プリンター属性](printer-attributes.md)、除く[属性のルート レベルのみ](root-level-only-attributes.md)します。 ([一般的な属性](general-attributes.md)EXTERN を付ける必要があります\_グローバルしない限り、 \***スイッチ**エントリは、ルート レベルで中かっこ内にありません)。

-   入れ子になった\***スイッチ**エントリで、複数の依存関係を指定できます。

-   \*コマンドのエントリ。

-   \*TTFSEnabled?、フォントの置き換えをことができます。

GPD エントリの次の種類は、再配置することはできません。

-   属性のルート レベルのみです。

-   \*TTFS エントリを指定するためには、フォントが置き換えられます。

-   \*制約、 \*InvalidCombination、 \*InvalidInstallableCombination、 \*」の説明に従って、オプションの無効な組み合わせを定義する NotInstalledConstraints エントリ[オプション制約](option-constraints.md).

-   \*機能と\*エントリのオプション (が[機能の属性](feature-attributes.md)と[オプション属性](option-attributes.md)再配置することが)。

1 つのメソッドのエントリが内部に正しく配置されている場合を決定する\***ケース**ステートメントがすべて削除するには、 \***スイッチ**と\***ケース**ステートメント。 場合内のエントリ、 \***ケース**ステートメントが正しいこと、それらが正しい後、 \***スイッチ**と\***ケース**ステートメントが削除されます。

### <a name="ordering-of-switch-statements-in-a-v4-print-driver-derived-from-a-class-driver"></a>ドライバーの印刷クラス ドライバーから派生した V4 の switch ステートメントの順序付け

派生の v4 プリンター ドライバーの GPD ファイルは、基底クラスのドライバーと同じ順序に従う必要があります。

次のシナリオを検討してください。 設定して v4 クラス ドライバーから派生した v4 プリンター ドライバーがある**RequiredClass**クラス ドライバーに、 \*-manifest.ini ファイル。

クラス ドライバーの GPD ファイルには、次のスイッチのツリーがあります。

```cpp
* Option: A4
    1. Switch: Resolution
* Option: Letter
    1. Switch: Resolution
    2. Switch: InputBin
```

派生の v4 プリンター ドライバーを追加する場合、 **MarginSetting**切り替えるには、その GPD ファイルに次のスイッチのツリーがあります。

```cpp
* Option: A4
    1. Switch: Resolution
    2. Switch: InputBin
    3. Switch: MarginSetting
* Option: Letter
    1. Switch: Resolution
    2. Switch: InputBin
    3. Switch: MarginSetting
```

なお**解決**前に設定されます**InputBin**派生 GPD でと**MarginSetting**両方の後に設定されます。 派生の v4 プリンター ドライバーの GPD ファイル、基底クラス ドライバーのと同じ順序に依存して、追加**MarginSetting**後。

など、正しく派生 GPD ファイルは、次のようになります可能性があります。

```cpp
* Option: A4
    1. Switch: MarginSetting
    2. Switch: InputBin
    3. Switch: Resolution
* Option: Letter
    1. Switch: MarginSetting
    2. Switch: InputBin
    3. Switch: Resolution
```

 

 





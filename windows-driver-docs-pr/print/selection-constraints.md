---
title: 選択制約
description: 選択制約
ms.assetid: 9537e4c7-2cee-494d-b1ec-95d8c91a90e6
keywords:
- 選択範囲の制約 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77b8d32a741abb4770b9dc935a1d6775210ba9fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572638"
---
# <a name="selection-constraints"></a>選択制約





多くの場合、同時にさまざまなプリンターの機能の特定のオプションを選択することはできません。 たとえば、封筒フィーダーが選択されている場合、レター サイズまたは A4 サイズの用紙などの nonenvelope 用紙サイズ選択できません。

同時に選択することはできませんプリンター オプションの組み合わせを指定するには、使用\*InvalidCombination または\*制約エントリ。 ユーザーが無効であると指定したオプションの組み合わせを選択しようとすると、Unidrv は選択範囲を拒否します。

\*InvalidCombination エントリに、次の形式があります。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* InvalidCombination:一覧 ( <em>FeatureName</em>します。 <em>OptionName</em> 、 <em>FeatureName</em>します。 <em>OptionName</em> ,...)</p></td>
</tr>
</tbody>
</table>

 

場所*FeatureName*機能の名前を指定し、 *OptionName*機能に関連付けられているオプションの名前を指定します。

1 つのオプションが一覧表示\*InvalidCombination エントリは、一連の組み合わせで使用できないオプションを示します。 たとえば、次のエントリを指定する*CMYK*普通紙と 720 DPI でカラー モードは使用できません。

```cpp
*InvalidCombination: LIST(Resolution.720dpi, MediaType.Plain, ColorMode.CMYK)
```

すべて\*InvalidCombination エントリは、GPD ファイルのルート レベルである必要があります (つまり、中かっこ内にありません)。 エントリに含まれるオプションの数は制限されています。

使用することができますを 2 つのオプションを無効な組み合わせでリレーションシップを示すためにのみ必要がある場合、\*制約のエントリ。 その形式です。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* の制約:<em>FeatureName</em>します。 <em>OptionName</em></p></td>
</tr>
</tbody>
</table>

 

場所*FeatureName*機能の名前を指定し、 *OptionName*機能に関連付けられているオプションの名前を指定します。 A\*制約のエントリは、内に配置する必要があります、\*エントリのオプションします。 たとえば、封筒フィーダーとレター サイズ、および A4 サイズの用紙を使用できないことを示す、次のエントリを使用できます。

```cpp
*Feature: InputBin
{
    *Option: ENVFEED
    {
        *Constraints: PaperSize.Letter
        *Constraints: PaperSize.A4
    }
}
```

または同等にします。

```cpp
*Feature: InputBin
{
    *Option: ENVFEED
    {
        *Constraints: LIST(PaperSize.Letter, PaperSize.A4)
    }
}
```

これらの例では、ユーザーは、封筒フィーダーとレター サイズの用紙または封筒フィーダーおよび A4 サイズの用紙を選択すると、Unidrv が選択範囲を拒否することを指定します。

 

 





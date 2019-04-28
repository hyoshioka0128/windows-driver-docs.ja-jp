---
title: 機能エントリ形式
description: 機能エントリ形式
ms.assetid: f4e91611-aa68-4426-82ef-9ad3f09d62f2
keywords:
- プリンター機能 WDK Unidrv、エントリの形式
- WDK のプリンターの機能を書式設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31cefd326154fe90d4a11d9e027d947f28af26db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361985"
---
# <a name="feature-entry-format"></a>機能エントリ形式





GPD ファイルで、プリンターの機能のエントリを指定するには、次の形式を使用します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* 機能:<em>FeatureName</em> {<em>FeatureAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

場所*FeatureName* 、定義済みのいずれかの名前を指定します[標準機能](standard-features.md)またはカスタマイズされた機能名と*FeatureAttributes*のセットは、 [機能の属性](feature-attributes.md)します。

たとえば、GPD ファイルには、標準の InputBin 機能の仕様が含まれます。

```cpp
*Feature: InputBin
{
    *Name: "Paper Bin"
    *DefaultOption: Upper
    *Option: Upper
    {
        *Name: "Upper Tray"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.10
            *Cmd: "<1B>&l1H"
        }
        *Constraints: PaperSize.Env10
    }
    *Option: Manual
    {
        *Name: "Manual Feed"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.10
            *Cmd: "<1B>&l2H"
        }
        *Installable?: TRUE
    }
}
```

繰り返し実行する機能仕様では、たとえば、2 つ以上の InputBin 機能のエントリを含む場合は、次の規則が適用されます。

-   属性とが重複しないオプションは、Unidrv のデータベースに追加されます。

-   属性と重複しているオプションは上書きされ、Unidrv には、最後の指定のみが保持されます。

機能がユーザーに表示される順序を制御できます。 参照してください[表示順序を指定する機能とオプション](specifying-feature-and-option-display-order.md)します。

 

 





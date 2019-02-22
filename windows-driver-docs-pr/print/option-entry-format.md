---
title: オプションのエントリの形式
description: オプションのエントリの形式
ms.assetid: defc035a-d571-4bf1-abeb-c7528ba23b81
keywords:
- プリンターは、WDK Unidrv、エントリの形式をオプションします。
- WDK プリンター オプションの形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 687d7ccbd26df18f635f99a42ff1e40e0c804507
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556496"
---
# <a name="option-entry-format"></a>オプションのエントリの形式





GPD ファイルでプリンター オプションのエントリを指定するには、次の形式を使用します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>オプション</strong>:<em>OptionName</em> { <em>OptionAttributes</em> }</p></td>
</tr>
</tbody>
</table>

 

場所*OptionName* 、定義済みのいずれかの名前は、[標準オプション](standard-options.md)またはカスタマイズされたオプション名と*OptionAttributes*は一連の[属性のオプション](option-attributes.md)します。

例では、一連の\***オプション**機能に関連付けられているエントリを参照してください[機能エントリの形式](feature-entry-format.md)します。

2 つ以上を指定することで、オプションの指定をたとえば反復する場合\***オプション**のエントリ、 **PaperSize**機能の文字のオプション、内の各オプションの重複する属性、\***オプション**エントリは、前の上書きし、GPD パーサーでは、発生した最後の 1 つだけ保持されます。 その一方で、GPD パーサーは、2 つまたは複数が発生した場合に\*機能のエントリ、 **PaperSize** (またはその他) 機能、 \***オプション**エントリが指定されていません。パーサーのデータベースに追加します。

ユーザーにオプションが表示される順序を制御できます。 参照してください[表示順序を指定する機能とオプション](specifying-feature-and-option-display-order.md)します。

 

 





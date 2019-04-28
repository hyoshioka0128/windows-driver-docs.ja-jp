---
title: forceIfDriverIsNotBetter XML 要素
description: forceIfDriverIsNotBetter XML 要素
ms.assetid: ba83c8fd-cc8e-44fd-96ed-855bb42c2493
keywords:
- forceIfDriverIsNotBetter XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- forceIfDriverIsNotBetter XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 14f19564df66e4d83d8880d69571f490e8f86e79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377081"
---
# <a name="forceifdriverisnotbetter-xml-element"></a>forceIfDriverIsNotBetter XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**ForceIfDriverIsNotBetter** XML 要素が空の要素を設定する、 **forceIfDriverIsNotBetter**フラグには、ドライバーがいる場合でも、デバイス ドライバーをインストールする DPInst を構成します。デバイスに現在インストールされているとは、新しいドライバーよりも優れた一致です。

### <a name="element-tag"></a>要素タグ

```cpp
<forceIfDriverIsNotBetter>
```

### <a name="xml-attributes"></a>XML 属性

なし

### <a name="element-information"></a>要素情報

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>親要素</strong></p></td>
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データの内容</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子要素が重複しています</strong></p></td>
<td align="left"><p>許可なし</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="comments"></a>「解説」

既定で、 **forceIfDriverIsNotBetter**フラグが OFF に設定します。 設定することができます、 **forceIfDriverIsNotBetter**を ON にフラグを含めることによって、 **forceIfDriverIsNotBetter**要素の子要素として、 [ **dpinst XML 要素**](dpinst-xml-element.md) DPinst 記述子ファイル、またはを使用して、 **/f**コマンド ライン スイッチ。

次のコード例に示します、 **forceIfDriverIsNotBetter**要素。

```cpp
<dpinst>
  ...
  <forceIfDriverIsNotBetter/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







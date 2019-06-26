---
title: scanHardware XML 要素
description: scanHardware XML 要素
ms.assetid: c1af7238-97e9-4c5f-95ea-fbc9f3cc8279
keywords:
- scanHardware XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- scanHardware XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5375092c38ca70da652fd98d53e45fa8fafb91f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374210"
---
# <a name="scanhardware-xml-element"></a>scanHardware XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)します。\]

**ScanHardware** XML 要素が空の要素を設定する、 **scanHardware**フラグをオンにします。 DPInst をインストールするを構成してこのフラグをオンに設定、[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)ドライバー パッケージに一致するコンピューターで構成されているデバイスとドライバー パッケージが適している場合にのみ、プラグ アンド プレイ (PnP) 関数ドライバー、デバイスに現在インストールされているドライバー パッケージとデバイスです。

### <a name="element-tag"></a>要素タグ

```cpp
<scanHardware>
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

既定で、 **scanHardware**フラグが OFF に設定します。 設定することができます、 **scanHardware**を ON にフラグを含めることによって、 **scanHardware** XML 要素の子要素として、 **dpinst** DPInst 記述子ファイル、またはを使用して XML 要素、 **/sh** コマンド ライン スイッチ。

次のコード例に示します、 **scanHardware**要素。

```cpp
<dpinst>
  ...
  <scanHardware/>
  ...
</dpinst>
```

 

 






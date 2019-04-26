---
title: suppressAddRemovePrograms XML 要素
description: suppressAddRemovePrograms XML 要素
ms.assetid: ab3bac90-dffa-400b-916a-a7deecbc42d7
keywords:
- suppressAddRemovePrograms XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- suppressAddRemovePrograms XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26ac21a7d8b1b9db9aef1c8c957a8f6f1c43387e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339640"
---
# <a name="suppressaddremoveprograms-xml-element"></a>suppressAddRemovePrograms XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**SuppressAddRemovePrograms** XML 要素が空の要素を設定する、 **suppressAddRemovePrograms**フラグには、構成エントリの追加を抑制する DPInst **プログラムと機能**コントロール パネルの します。 これらのエントリを表す、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)と DPInst をインストールするドライバー パッケージのグループ。

**注**  DPInst がするドライバー パッケージのエントリを追加する Windows Vista より前のバージョンの Windows で**プログラム追加と削除**コントロール パネルの します。

 

### <a name="element-tag"></a>要素タグ

```cpp
<suppressAddRemovePrograms>
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
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong> </a>または<a href="group-xml-element.md" data-raw-source="[&lt;strong&gt;group&lt;/strong&gt;](group-xml-element.md)"><strong>グループ</strong></a></p></td>
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

既定で、 **suppressAddRemovePrograms**フラグが OFF に設定します。 設定する、 **suppressAddRemovePrograms**を ON にすべてのドライバーのドライバーのすべての DPInst がインストールされるフラグ[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)グループが含まれて、 **suppressAddRemovePrograms**要素の子要素として、 **dpinst** DPInst の記述子ファイルか使用して XML 要素、 **/sa** コマンド ライン スイッチ。 設定する、 **suppressAddRemoverPrograms**の特定のドライバー パッケージのグループにのみフラグは、含める、 **suppressAddRemovePrograms**要素に対応する子要素として**グループ** DPInst の記述子ファイルの XML 要素。

次のコード例に示します、 **suppressAddRemovePrograms**要素の子要素である、 **dpinst**要素。

```cpp
<dpinst>
  ...
   <suppressAddRemovePrograms/>
  ...
</dpinst>
```

次のコード例に示します、 **suppressAddRemovePrograms**要素の子要素である、**グループ**要素。

```cpp
<dpinst>
  ...
  <group>
    <package path="DirAbc\Abc.inf" /> 
    <package path="DirDef\Def.inf" /> 
    <suppressAddRemovePrograms/>
  <group/>
  ...
</dpinst>
```

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

[**グループ**](group-xml-element.md)

 

 







---
title: deleteBinaries XML 要素
description: DeleteBinaries XML 要素は、ドライバー パッケージのインストール時に、システムにコピーされたシステムからバイナリ ファイルを削除する DPInst を構成するには、deleteBinaries フラグを設定する空要素です。要素タグ deleteBinaries XML AttributesNoneElement 情報親 elementsdpinstChild elementsNoneData contentsNone permittedDuplicate 子 elementsNone 解説既定では許可されている、deleteBinaries フラグは OFF に設定されます。 DeleteBinaries フラグを ON に設定するには、dpinst 要素の子要素として deleteBinaries 要素を含めるか、/d DPInst のコマンド ライン スイッチを使用します。 次のコード例では、deleteBinaries 要素を示します。 dpinst.deleteBinaries/.../注以降、Windows 7 オペレーティング システムで dpinst ON の deleteBinaries XML 要素の設定は無視されます。 ドライバー パッケージがインストールされている、DPInst を使用して削除できなくできるときに、システムにコピーされたバイナリ ファイル。
ms.assetid: 2711b2c2-b1ec-41cb-aeb2-1d9078740075
keywords:
- deleteBinaries XML 要素のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- deleteBinaries XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bcee0636cb5c3141c812735c8c8cb4089044732e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341491"
---
# <a name="deletebinaries-xml-element"></a>deleteBinaries XML 要素


\[DIFx は非推奨、詳細については、「 [DIFx ガイドライン](https://msdn.microsoft.com/windows/hardware/drivers/install/difx-guidelines)します。\]

**DeleteBinaries** XML 要素が空の要素を設定する、 **deleteBinaries** DPInst、ときに、システムにコピーされたシステムからバイナリファイルを削除するを構成するには、フラグ[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)がインストールされています。

**要素タグ**

```cpp
<deleteBinaries>
```

**XML 属性**

なし

**要素情報**

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
<td align="left"><p>なし</p></td>
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

 

**注釈**

既定で、 **deleteBinaries**フラグが OFF に設定します。 設定する、 **deleteBinaries** on フラグは、含める、 **deleteBinaries**要素の子要素として、 **dpinst**要素または使用して、 **/d** DPInst のコマンド ライン スイッチ。

次のコード例に示します、 **deleteBinaries**要素。

```cpp
<dpinst>
  ...
   <deleteBinaries/>
  ...
</dpinst>
```

**注**   Windows 7 以降のオペレーティング システムは ON に設定は無視されます、 **deleteBinaries** XML 要素。 バイナリのファイルは、システムにコピーされたときに、[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)がインストールされている、不要になった DPInst を使用して削除できます。

 

## <a name="see-also"></a>関連項目


[**dpinst**](dpinst-xml-element.md)

 

 







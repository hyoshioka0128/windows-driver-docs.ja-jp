---
title: 選択とインストールの間の制約
description: 選択とインストールの間の制約
ms.assetid: abb6004f-daae-4f28-b36c-102d0b8c9f55
keywords:
- インストール制約 WDK Unidrv
- 選択範囲の制約 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e09254f2efed71de895b90b2393deeece3761e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537224"
---
# <a name="constraints-between-selections-and-installations"></a>選択とインストールの間の制約





場合によっては他のいくつかのオプションがインストールされている場合に、特定のオプションを選択することはできません、またはその他のオプションがインストールされていない場合に、特定のオプションを選択できないことを指定する必要です。 たとえば、ユーザーは必要があります tabloid 用紙をプリンターの大きなサイズの用紙トレイがインストールされていない場合に選択することできません。

その他のオプションのインストール状態を持つ特定のオプションの選択間のリレーションシップを指定するには、使用\* **InstalledConstraints**と\* **NotInstalledConstraints**エントリ。 その形式です。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>InstalledConstraints:<em>FeatureName</em>します。 <em>OptionName</em></p></td>
</tr>
<tr class="even">
<td><p></em>NotInstalledConstraints:<em>FeatureName</em>します。 <em>OptionName</em></p></td>
</tr>
</tbody>
</table>

 

場所*FeatureName*機能の名前を指定し、 *OptionName*機能に関連付けられているオプションの名前を指定します。 引数が、機能の場合、期間と*OptionName*は含まれません。

\* **InstalledConstraints**または\* **NotInstalledConstraints**エントリ内に配置する必要があります、\*機能または\*エントリのオプションします。 などをユーザーがされないこと、プリンターの大きなサイズの用紙トレイがインストールされていない場合は、tabloid 用紙を選択することを示すに、次のエントリを使用することができます。

```cpp
*Feature: InputBin
{
    *Option: LARGEFMT
    {
        Installable?: TRUE
        NotInstalledConstraints: PaperSize.TABLOID
    }
}
```

機能またはオプションが含まれている場合、 \* **InstalledConstraints**または\* **NotInstalledConstraints**エントリ、機能またはオプションの\*インストール可能ですか? 属性設定する必要があります**TRUE**します。

 

 





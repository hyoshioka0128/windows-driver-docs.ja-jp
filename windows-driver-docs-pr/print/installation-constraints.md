---
title: インストール制約
description: インストール制約
ms.assetid: 0adf5a6a-e9de-4bb0-bf1c-fe7eef565840
keywords:
- インストール制約 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f31b8c5a1022a5ed0498f65b9f277068e59ea4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362769"
---
# <a name="installation-constraints"></a>インストール制約





場合によっては、特定のプリンターのインストール可能なオプションを同時にインストールすることはできません。 たとえば、封筒フィーダー と 両面印刷ユニットの両方をインストールできないこと可能性があります。

同時にインストールすることはできませんプリンター オプションの組み合わせを指定するには、使用\*InvalidInstallableCombination エントリ。

\*InvalidInstallableCombination エントリに、次の形式があります。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* InvalidInstallableCombination:一覧 (</strong><em>FeatureName</em> <strong>します。</strong> <em>OptionName</em><strong>、</strong> <em>FeatureName</em> <strong>します。</strong> <em>OptionName</em><strong>、</strong> .<strong>)</strong></p></td>
</tr>
</tbody>
</table>

 

場所*FeatureName*機能の名前を指定し、 *OptionName*機能に関連付けられているオプションの名前を指定します。 この一覧含めることができます機能とオプション、この場合、期間と*OptionName*は含まれません。

1 つの機能とオプションが一覧表示\*InvalidInstallableCombination エントリが一連の機能と組み合わせて使用できないオプションを示します。 たとえば、次のエントリでは、封筒フィーダー、両面印刷ユニットことはできませんが同時にインストールされていることを指定します。

```cpp
*InvalidInstallableCombination: LIST(InputBin.ENVFEED, Duplex)
```

すべて\*InvalidInstallationCombination エントリは、GPD ファイルのルート レベルである必要があります (つまり、中かっこ内にありません)。 機能と、エントリに含まれるオプションの数が制限されています。

機能またはオプションが含まれている場合、 \*InvalidInstallationCombination エントリ、機能またはオプションの\*インストール可能でしょうか。 属性を設定する必要があります**TRUE**します。

 

 





---
title: pciir
description: Pciir 拡張機能には、コント ローラーの入力を中断するコンポーネントの周辺機器相互接続 (PCI) デバイスのハードウェアのルーティングの内容が表示されます。
ms.assetid: 83d1b716-adfe-4712-bdbb-25960c38fff0
keywords:
- PCI IRQ ルーティング テーブル
- 周辺機器のコンポーネントの相互接続 (PCI)
- Windows デバッグ pciir
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pciir
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3fc18822b946a2d64f755ab14888ecb35ccca71d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572528"
---
# <a name="pciir"></a>!pciir


**! Pciir**拡張機能は、コント ローラーの入力を中断するコンポーネントの周辺機器相互接続 (PCI) デバイスのハードウェアのルーティングの内容を表示します。

```dbgcmd
!pciir
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Vista 以降</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

この拡張機能のコマンドは、Advanced Configuration and Power Interface (ACPI) 有効になっていない x86 ベースの移行先コンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

すべての ACPI-有効になっているコンピューターで、同様の情報を使用して、 [ **! acpiirqarb** ](-acpiirqarb.md)拡張機能。

PCI バスについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

 

 






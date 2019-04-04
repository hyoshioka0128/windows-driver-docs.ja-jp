---
title: PcRegisterAdapterPower ルール (オーディオ)
description: PcRegisterAdapterPower ルールでは、ミニポート ドライバーがしないで PortCls、介在することがなく、2 回呼び出す PcRegisterAdapterPowerManagement を呼び出すことがなく PcUnregisterAdapterPowerManagement.Call PcUnregisterAdapterPowerManagement を指定しますまず、PcRegisterAdapterPowerManagement を呼び出すことです。
ms.assetid: 8F6E6B1D-F19C-469A-BC5A-061996BEA532
ms.date: 05/21/2018
keywords:
- PcRegisterAdapterPower ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcRegisterAdapterPower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bd4980b5b890db28179dab1b6009db07ca24d2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579623"
---
# <a name="pcregisteradapterpower-rule-audio"></a>PcRegisterAdapterPower ルール (オーディオ)


PortCls ミニポート ドライバーがしないで PcRegisterAdapterPower ルールを指定します。

-   呼び出す[ **PcRegisterAdapterPowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff537724)を呼び出さなくても 2 回[ **PcUnregisterAdapterPowerManagement**](https://msdn.microsoft.com/library/windows/hardware/ff537735)します。
-   呼び出す[ **PcUnregisterAdapterPowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff537735)呼び出さず[ **PcRegisterAdapterPowerManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff537724)最初。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071006) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain オーディオ</strong>します。</p>
<p>以下に例を示します。</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 






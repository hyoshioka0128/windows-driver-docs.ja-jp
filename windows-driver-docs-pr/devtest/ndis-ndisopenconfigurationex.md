---
title: NdisOpenConfigurationEx ルール (ndis)
description: このルールは、NdisOpenConfigurationEx と NdisCloseConfiguration が異なる順序でと呼ばれることを確認します。 最終的な目標では、MiniportHaltEx の終了時に、構成のハンドルが閉じられているかどうかを確認します。
ms.assetid: 3E23D8AE-5EBC-4C2F-9EE3-42718D86B97C
ms.date: 05/21/2018
keywords:
- NdisOpenConfigurationEx ルール (ndis)
topic_type:
- apiref
api_name:
- NdisOpenConfigurationEx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d61c15cc3fe3d00c79a70fcf13d45ecab0f4c3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572626"
---
# <a name="ndisopenconfigurationex-rule-ndis"></a>NdisOpenConfigurationEx ルール (ndis)


このルールは、ことを確認[ **NdisOpenConfigurationEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563717)と[ **NdisCloseConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff561642)代替の順序で呼び出されます。 最終的な目標は、構成のハンドルが閉じられている場合にかどうかを確認する[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が終了します。

ルールは、3 つの異なる状態を使用します。 構成を開くまたは閉じるときの状態の変更。 構成のハンドルが開いている場合でもときに、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)終了すると、欠陥が報告されます。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisOpenConfigurationEx</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**NdisCloseConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff561642)
[**NdisOpenConfigurationEx**](https://msdn.microsoft.com/library/windows/hardware/ff563717)
 

 






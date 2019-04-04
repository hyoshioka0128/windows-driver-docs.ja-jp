---
title: DDI 使用量ルール セット (Storport)
description: これらの規則を使用すると、ドライバー、正しく使用する Storport Ddi 正しくを確認します。
ms.assetid: 858BBD97-4E3D-464A-B85F-358809431347
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19011dc2606e6ed79b526a20e3bd06963410c8a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531919"
---
# <a name="ddi-usage-rule-set-storport"></a>DDI 使用量ルール セット (Storport)


これらの規則を使用すると、ドライバー、正しく使用する Storport Ddi 正しくを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-hwstorportprohibitedddis.md" data-raw-source="[&lt;strong&gt;HwStorPortProhibitedDDIs&lt;/strong&gt;](storport-hwstorportprohibitedddis.md)"><strong>HwStorPortProhibitedDDIs</strong></a></p></td>
<td align="left"><p>このルールには、物理 StorPort ミニポート ドライバーで呼び出すことはできませんを WDM Ddi (インタロックされた関数を除く) の一覧が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullchecks.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullchecks.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck ルールは、ドライバーの後で、ドライバーのコード内の NULL 値が逆参照しないことを確認します。 このルールは、これらの条件のいずれかが true の場合、欠陥を報告します。</p>
<ul>
<li>以降は逆参照が NULL の代入です。</li>
<li>ドライバーでは、後で逆参照が NULL の可能性があるプロシージャにグローバル/パラメーターがあるし、ポインターの初期値は NULL である可能性がありますの候補を示す、ドライバーでの明示的なチェックがあります。</li>
</ul>
<p>NullCheck ルール違反では、最も関連のコード ステートメントは、トレースのツリー ペインで強調表示されます。 レポートの出力の使用方法の詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff552834" data-raw-source="[Static Driver Verifier Report](https://msdn.microsoft.com/library/windows/hardware/ff552834)">静的ドライバー検証ツールのレポート</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff554020" data-raw-source="[Understanding the Trace Viewer](https://msdn.microsoft.com/library/windows/hardware/ff554020)">トレース ビューアーを理解する</a>を参照してください。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportddisportonly.md" data-raw-source="[&lt;strong&gt;StorPortDDIsPortOnly&lt;/strong&gt;](storport-storportddisportonly.md)"><strong>StorPortDDIsPortOnly</strong></a></p></td>
<td align="left"><p>このルールには、StorPort のポート専用 Ddi (インタロックされた関数を除く) StorPort miniports で呼び出すことはできませんの一覧が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportdeprecated.md" data-raw-source="[&lt;strong&gt;StorPortDeprecated&lt;/strong&gt;](storport-storportdeprecated.md)"><strong>StorPortDeprecated</strong></a></p></td>
<td align="left"><p>このルールは、ドライバーは呼び出さないことこれらの非推奨のルーチンのいずれかを確認します。<strong>StorPortValidateRange</strong>または<strong>StorPortLogError</strong>します。</p></td>
</tr>
</tbody>
</table>

 

**DDI 使用量のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **DDIUsage**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **DDIUsage.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 






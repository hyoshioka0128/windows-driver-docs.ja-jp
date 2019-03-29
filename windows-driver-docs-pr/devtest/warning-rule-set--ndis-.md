---
title: 警告の規則セット (NDIS)
description: これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。
ms.assetid: 454FB042-76FA-4A46-9549-4DE8BF52A2D3
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d59bffca23d1e7cf6d4819a73ca848a843914227
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581233"
---
# <a name="warning-rule-set-ndis"></a>警告の規則セット (NDIS)


これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。

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
<td align="left"><p><a href="ndis-ndisstallexecution-delay.md" data-raw-source="[&lt;strong&gt;NdisStallExecution_Delay&lt;/strong&gt;](ndis-ndisstallexecution-delay.md)"><strong>NdisStallExecution_Delay</strong></a></p></td>
<td align="left"><p>NdisStallExecution_Delay ルールを指定する<strong>NdisStallExecution</strong>の値を使用して呼び出す必要がありますしない<em>MicrosecondsToStall</em> 50 マイクロ秒よりも大きい。</p></td>
</tr>
</tbody>
</table>

 

**警告ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**警告**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Warning.sdv**で、 **/check**オプション。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 






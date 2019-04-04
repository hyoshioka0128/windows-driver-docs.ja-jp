---
title: 警告ルール (Storport) を設定します。
description: これらの規則を使用すると、さまざまなコンテキストでは、ドライバーが Irp を正しく処理を次のように Microsoft が推奨されるベスト プラクティスを確認します。
ms.assetid: 6557A741-C49F-456B-B285-DE6D171DDCEE
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 90c6e93119e5230ac4cabbb3a1e8255c8e990ed1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527642"
---
# <a name="warning-rule-set-storport"></a>警告ルール (Storport) を設定します。


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
<td align="left"><p><a href="storport-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](storport-pagedcode.md)"><strong>PagedCode</strong></a></p></td>
<td align="left"><p>このルールの検証時に、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff558773" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558773)"> <strong>PAGED_CODE</strong> </a>マクロが呼び出されると、ドライバーが、 <strong>IRQL &lt; DISPATCH_LEVEL</strong>します。 任意のコード実行<strong>IRQL &gt;= DISPATCH_LEVEL</strong>ページ フォールトを回避するために、非ページ メモリである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportstatuspending.md" data-raw-source="[&lt;strong&gt;StorPortStatusPending&lt;/strong&gt;](storport-storportstatuspending.md)"><strong>StorPortStatusPending</strong></a></p></td>
<td align="left"><p>このルールは、状態、SRB が完了していないことを確認します。 <strong>SRB_STATUS_PENDING</strong>します。</p></td>
</tr>
</tbody>
</table>

 

**警告ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**警告**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Warning.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 






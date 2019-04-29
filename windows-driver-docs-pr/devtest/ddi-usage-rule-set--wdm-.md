---
title: DDI 使用の規則セット (WDM)
description: これらの規則を使用すると、ドライバー、正しく使用する WDM Ddi 正しくを確認します。
ms.assetid: B958191C-8E14-4D4D-9D0F-AD5D29599E53
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: bcd9d30290931adf48098bd49489f092e7fe1e12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327116"
---
# <a name="ddi-usage-rule-set-wdm"></a>DDI 使用の規則セット (WDM)


これらの規則を使用すると、ドライバー、正しく使用する WDM Ddi 正しくを確認します。

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
<td align="left"><p><a href="wdm-debugbreakusage.md" data-raw-source="[&lt;strong&gt;DebugBreakUsage&lt;/strong&gt;](wdm-debugbreakusage.md)"><strong>DebugBreakUsage</strong></a></p></td>
<td align="left"><p><a href="wdm-debugbreakusage.md" data-raw-source="[&lt;strong&gt;DebugBreakUsage&lt;/strong&gt;](wdm-debugbreakusage.md)"> <strong>DebugBreakUsage</strong> </a>ルールでは、ドライバーを呼び出してはならないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff543626" data-raw-source="[&lt;strong&gt;DbgBreakPoint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543626)"> <strong>DbgBreakPoint</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff543629" data-raw-source="[&lt;strong&gt;DbgBreakPointWithStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543629)"> <strong>DbgBreakPointWithStatus</strong></a>します。 このルールは、非デバッグ バージョンのドライバーをビルドする場合にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheckw.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckw.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck ルールは、ドライバーの後で、ドライバーのコード内の NULL 値が逆参照しないことを確認します。 このルールは、これらの条件のいずれかが true の場合、欠陥を報告します。</p>
<ul>
<li>以降は逆参照が NULL の代入です。</li>
<li>ドライバーでは、後で逆参照が NULL の可能性があるプロシージャにグローバル/パラメーターがあるし、ポインターの初期値は NULL である可能性がありますの候補を示す、ドライバーでの明示的なチェックがあります。</li>
</ul>
<p>NullCheck ルール違反では、最も関連のコード ステートメントは、トレースのツリー ペインで強調表示されます。 レポートの出力の使用方法の詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff552834" data-raw-source="[Static Driver Verifier Report](https://msdn.microsoft.com/library/windows/hardware/ff552834)">静的ドライバー検証ツールのレポート</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff554020" data-raw-source="[Understanding the Trace Viewer](https://msdn.microsoft.com/library/windows/hardware/ff554020)">トレース ビューアーを理解する</a>します。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"><strong>SafeStrings</strong></a></p></td>
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"> <strong>SafeStrings</strong> </a>ルールでは、ドライバーがシステムを誤ってまたは悪意のある侵入から保護する文字列操作関数のみを呼び出すことを指定します。 これらのドライバーの安全な文字列関数は、Ntstrsafe.h で定義されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"><strong>ObsoleteDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"> <strong>ObsoleteDDIs</strong> </a>ルールでは、ドライバーを呼び出さないことを指定します<a href="https://msdn.microsoft.com/library/windows/hardware/ff547164" data-raw-source="[&lt;strong&gt;FsRtlPrivateLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547164)"> <strong>FsRtlPrivateLock</strong></a>します。 この機能は廃止されています。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545940" data-raw-source="[&lt;strong&gt;FsRtlFastLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545940)"> <strong>FsRtlFastLock</strong> </a>代わりにします。</p></td>
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

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 






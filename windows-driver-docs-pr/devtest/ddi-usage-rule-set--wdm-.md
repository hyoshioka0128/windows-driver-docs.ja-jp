---
title: DDI 使用の規則セット (WDM)
description: これらのルールを使用して、ドライバーが WDM DDIs を正しく使用していることを確認します。
ms.assetid: B958191C-8E14-4D4D-9D0F-AD5D29599E53
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6c1a79861b0a81680d593a33a3030a49a88eab76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840290"
---
# <a name="ddi-usage-rule-set-wdm"></a>DDI 使用の規則セット (WDM)


これらのルールを使用して、ドライバーが WDM DDIs を正しく使用していることを確認します。

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
<td align="left"><p><a href="wdm-debugbreakusage.md" data-raw-source="[&lt;strong&gt;DebugBreakUsage&lt;/strong&gt;](wdm-debugbreakusage.md)"><strong>Debugbreakusage</strong></a>ルールでは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint" data-raw-source="[&lt;strong&gt;DbgBreakPoint&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)"><strong>dbgbreakpoint ポイント</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus" data-raw-source="[&lt;strong&gt;DbgBreakPointWithStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)"><strong>dbgbreakpointwithstatus</strong></a>を呼び出すことができないことを指定します。 この規則は、ドライバーの非デバッグバージョンをビルドする場合にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheckw.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckw.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 規則は、ドライバーコード内の NULL 値がドライバーの後で逆参照されないことを検証します。 このルールは、次のいずれかの条件が満たされた場合に、欠陥を報告します。</p>
<ul>
<li>後で逆参照される NULL の割り当てがあります。</li>
<li>ドライバー内のプロシージャには、後で逆参照される可能性のあるグローバル/パラメーターがあります。また、ドライバーに明示的なチェックがあり、ポインターの初期値が NULL である可能性があることが示されています。</li>
</ul>
<p>NullCheck 規則違反では、最も関連性の高いコードステートメントが [トレースツリー] ウィンドウで強調表示されます。 レポート出力の操作の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)">静的ドライバーの検証ツールレポート</a>」と「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)">トレースビューアーに</a>ついて」を参照してください。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"><strong>SafeStrings</strong></a></p></td>
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"><strong>Safestrings</strong></a>規則は、意図しない、または悪意のある侵入からシステムを保護する文字列操作関数だけがドライバーによって呼び出されるように指定します。 これらのドライバーの安全な文字列関数は、、Ntstrsafe.h で定義されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"><strong>ObsoleteDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"><strong>ObsoleteDDIs</strong></a>ルールは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprivatelock" data-raw-source="[&lt;strong&gt;FsRtlPrivateLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprivatelock)"><strong>Fsrtlprivatelock</strong></a>を呼び出すことができないことを指定します。 この関数は互換性のために残されています。 代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfastlock" data-raw-source="[&lt;strong&gt;FsRtlFastLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfastlock)"><strong>Fsrtlfastlock</strong></a>を使用してください。</p></td>
</tr>
</tbody>
</table>

 

**DDI 使用規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[規則セット]** で **[ddiusage]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**ddiusage. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 






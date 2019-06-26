---
title: 保護レベルへの優先順位の割り当て
description: 保護レベルへの優先順位の割り当て
ms.assetid: 87a63d30-4aa2-4835-87bc-1acb062bde26
keywords:
- 保護レベルの優先順位を割り当て、WDK の表示
- 保護レベルの WDK 表示、ACP の優先順位
- 保護レベルの WDK 表示、CGMS A の優先順位
- 保護レベルの WDK 表示、HDCP の優先順位
- 保護レベルの WDK 表示、DPCP の優先順位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9abfda0b6561561a53d7eed0920f145677f778f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384633"
---
# <a name="assigning-precedence-to-protection-levels"></a>保護レベルへの優先順位の割り当て


優先順位の値は、各保護の種類の場合は、各保護レベルに割り当てられます。 これにより、物理出力は、2 つ以上の保護されている出力が物理的な出力に関連付けられ、保護された各出力が別の保護レベルがある場合に使用する保護レベルを決定できます。

Microsoft DirectX グラフィックスのカーネル サブシステム (*Dxgkrnl.sys*) 表示ミニポート ドライバーの 1 つ以上の呼び出しを行うことができます[ **DxgkDdiOPMCreateProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)特定の物理出力の 1 つ以上の保護された出力を作成する関数。 さらに、これらの保護された出力の各同じ出力保護の種類の別の保護レベルを持つことができます。

たとえば、グラフィックス アダプターが CGMS A 保護の型を持つ 1 つの複合出力をその複合の出力に関連付けられている保護された出力 A と B の両方があるとします。 たとえば、次に、A の出力を保護する[ **CGMS する保護レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa) DXGKMDT に設定されている\_OPM\_CGMSA\_コピー\_いいえ\_より保護されている出力 B の中に DXGKMDT に CGMS する保護レベルが設定されている\_OPM\_CGMSA\_コピー\_1 つ\_生成します。 このような状況で物理的な出力が両方の保護レベルを使用できません。 したがって、この物理の出力は、一度に CGMS する保護レベルを 1 つだけを出力することができます、ため、物理出力は優先順位の高い CGMS する保護レベルを使用する必要があります。

どの保護レベルが異なる場合 (最高優先順位の低い) から物理的な出力を使用する必要がありますには、出力が保護されている次のセクションでは表示では、さまざまな保護レベルを使用する物理出力よう指示します。 これらのテーブル COPP または OPM セマンティクスを持つ保護された出力に適用されることに注意してください。

### <a name="span-idacpprotectionlevelprecedencespanspan-idacpprotectionlevelprecedencespanacp-protection-level-precedence"></a><span id="acp_protection_level_precedence"></span><span id="ACP_PROTECTION_LEVEL_PRECEDENCE"></span>ACP の保護レベルの優先順位

別の保護された出力では、さまざまな ACP 保護レベルを使用する物理出力を指示と、物理の出力より高い優先順位が次の表に示すように、保護レベルを使用してください。 このテーブルが COPP セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ACP の保護レベル値</th>
<th align="left">優先度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_ACP_OFF (0)</p></td>
<td align="left"><p>最低の優先順位 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_ONE (1)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_THREE (3)</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_ACP_LEVEL_TWO (2)</p></td>
<td align="left"><p>最高の優先順位 (3)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcgmsaprotectionlevelprecedencespanspan-idcgmsaprotectionlevelprecedencespancgms-a-protection-level-precedence"></a><span id="cgms_a_protection_level_precedence"></span><span id="CGMS_A_PROTECTION_LEVEL_PRECEDENCE"></span>CGMS する保護レベルの優先順位

別の保護された出力では、さまざまな CGMS する保護レベルを使用する物理出力を指示と、物理の出力より高い優先順位が次の表に示すように、保護レベルを使用してください。 このテーブルが COPP セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CGMS する保護レベル値</th>
<th align="left">優先度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_OFF (0)</p></td>
<td align="left"><p>最低の優先順位 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_FREELY (1)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_ONE_GENERATION (3)</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_NO_MORE (2)</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_COPY_NEVER (4)</p></td>
<td align="left"><p>最高の優先順位 (4)</p></td>
</tr>
</tbody>
</table>

 

**注**  再配布の制御フラグ (DXGKMDT\_OPM\_再配布\_コントロール\_REQUIRED) CGMS A の優先順位の値には影響しません。 たとえば、(DXGKMDT\_OPM\_CGMSA\_コピー\_1 つ\_生成 |DXGKMDT\_OPM\_再配布\_コントロール\_REQUIRED) DXGKMDT と同じ優先順位値を持つ\_OPM\_CGMSA\_コピー\_いずれか\_生成します。

 

### <a name="span-idhdcpprotectionlevelprecedencespanspan-idhdcpprotectionlevelprecedencespanhdcp-protection-level-precedence"></a><span id="hdcp_protection_level_precedence"></span><span id="HDCP_PROTECTION_LEVEL_PRECEDENCE"></span>HDCP 保護レベルの優先順位

別の保護された出力では、さまざまな HDCP 保護レベルを使用する物理出力を指示と、物理の出力より高い優先順位が次の表に示すように、保護レベルを使用してください。 このテーブルが COPP または OPM セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HDCP 保護レベル値</th>
<th align="left">優先度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_HDCP_OFF (0)</p></td>
<td align="left"><p>最低の優先順位 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_HDCP_ON (1)</p></td>
<td align="left"><p>最高の優先順位 (1)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddpcpprotectionlevelprecedencespanspan-iddpcpprotectionlevelprecedencespandpcp-protection-level-precedence"></a><span id="dpcp_protection_level_precedence"></span><span id="DPCP_PROTECTION_LEVEL_PRECEDENCE"></span>DPCP 保護レベルの優先順位

別の保護された出力では、さまざまな DPCP 保護レベルを使用する物理出力を指示と、物理の出力より高い優先順位が次の表に示すように、保護レベルを使用してください。 このテーブルが OPM セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DPCP 保護レベル値</th>
<th align="left">優先度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_DPCP_OFF (0)</p></td>
<td align="left"><p>最低の優先順位 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_DPCP_ON (1)</p></td>
<td align="left"><p>最高の優先順位 (1)</p></td>
</tr>
</tbody>
</table>

 

 

 






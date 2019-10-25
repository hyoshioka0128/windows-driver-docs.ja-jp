---
title: 保護レベルに優先順位を割り当てる
description: 保護レベルに優先順位を割り当てる
ms.assetid: 87a63d30-4aa2-4835-87bc-1acb062bde26
keywords:
- 保護レベル WDK 表示、優先順位の割り当て
- 保護レベル WDK 表示、ACP 優先順位
- 保護レベル WDK display、CGMS-優先順位
- 保護レベル WDK 表示、HDCP 優先順位
- 保護レベル WDK 表示、[CP の優先順位]
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcdfb06305c196c9eb4abdc834a0b414f2331652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839827"
---
# <a name="assigning-precedence-to-protection-levels"></a>保護レベルに優先順位を割り当てる


それぞれの保護の種類について、各保護レベルに優先順位値が割り当てられます。 これにより、2つ以上の保護された出力が物理出力に関連付けられていて、保護された各出力の保護レベルが異なる場合に、物理出力でどの保護レベルを使用するかを決定できます。

Microsoft DirectX graphics カーネルサブシステム (*Dxgkrnl*) は、ディスプレイミニポートドライバーの[**DxgkDdiOPMCreateProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)関数を複数回呼び出して、特定の物理出力に対して複数の保護された出力を作成することができます。 さらに、これらの保護された各出力は、同じ出力保護の種類に対して異なる保護レベルを持つことができます。

たとえば、1つのグラフィックスアダプターに CGMS 保護型を持つ複合出力が1つあり、保護された出力が A で、B がその複合出力に関連付けられているとします。 次に、保護された出力 A の[**CGMS 保護レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgkmdt_opm_cgmsa)が dxgkmdt\_OPM に設定されているとします。\_CGMSA\_コピー\_保護されていない出力 B の CGMS-保護レベルは dxgkmdt\_OPM\_CGMSA に設定されています。\_コピー\_1 つの\_生成を行います。\_ このような状況では、物理出力で両方の保護レベルを使用することはできません。 したがって、物理出力は一度に1つの CGMS 保護レベルのみを出力するため、物理出力では、優先順位の高い CGMS 保護レベルを使用する必要があります。

次のセクションでは、保護された出力ごとに異なる保護レベルを使用するように物理出力に指示する場合に、物理出力で使用する必要がある保護レベル (優先順位の高いもの) を示します。 これらのテーブルは、COPP または OPM セマンティクスを使用した保護された出力に適用されることに注意してください。

### <a name="span-idacp_protection_level_precedencespanspan-idacp_protection_level_precedencespanacp-protection-level-precedence"></a><span id="acp_protection_level_precedence"></span><span id="ACP_PROTECTION_LEVEL_PRECEDENCE"></span>ACP の保護レベルの優先順位

さまざまな保護された出力で異なる ACP 保護レベルを使用するように物理出力に指示する場合、物理出力では、次の表に示すように、優先順位の高い保護レベルを使用する必要があります。 このテーブルは、COPP セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ACP の保護レベルの値</th>
<th align="left">優先順位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_ACP_OFF (0)</p></td>
<td align="left"><p>最低優先順位 (0)</p></td>
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

 

### <a name="span-idcgms_a_protection_level_precedencespanspan-idcgms_a_protection_level_precedencespancgms-a-protection-level-precedence"></a><span id="cgms_a_protection_level_precedence"></span><span id="CGMS_A_PROTECTION_LEVEL_PRECEDENCE"></span>CGMS-保護レベルの優先順位

異なる CGMS 保護レベルを使用するように、保護されている出力が異なる場合、物理出力では、次の表に示すように、優先順位の高い保護レベルを使用する必要があります。 このテーブルは、COPP セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CGMS-保護レベルの値</th>
<th align="left">優先順位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_CGMSA_OFF (0)</p></td>
<td align="left"><p>最低優先順位 (0)</p></td>
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

 

再配布制御フラグ (DXGKMDT\_OPM\_再配布\_コントロール\_必要) は、CGMS の優先順位の値には影響しません **。  ** たとえば、(DXGKMDT\_OPM\_CGMSA\_コピー\_1 つ\_生成 |DXGKMDT\_OPM\_再配布\_コントロール\_必須) は、DXGKMDT\_OPM\_CGMSA\_COPY\_1\_生成と同じ優先順位の値を持ちます。

 

### <a name="span-idhdcp_protection_level_precedencespanspan-idhdcp_protection_level_precedencespanhdcp-protection-level-precedence"></a><span id="hdcp_protection_level_precedence"></span><span id="HDCP_PROTECTION_LEVEL_PRECEDENCE"></span>HDCP 保護レベルの優先順位

異なる保護された出力で、物理的な出力で異なる HDCP 保護レベルを使用するように指示されている場合、物理出力では、次の表に示すように、優先順位の高い保護レベルを使用する必要があります。 このテーブルは、COPP または OPM セマンティクスを使用した保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">HDCP の保護レベルの値</th>
<th align="left">優先順位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_HDCP_OFF (0)</p></td>
<td align="left"><p>最低優先順位 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_HDCP_ON (1)</p></td>
<td align="left"><p>優先順位が高い (1)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddpcp_protection_level_precedencespanspan-iddpcp_protection_level_precedencespandpcp-protection-level-precedence"></a><span id="dpcp_protection_level_precedence"></span><span id="DPCP_PROTECTION_LEVEL_PRECEDENCE"></span>% CP 保護レベルの優先順位

異なる保護された出力によって、異なる状態の保護レベルを使用するように物理出力が指示された場合、物理出力では、次の表に示すように、優先順位の高い保護レベルを使用する必要があります。 このテーブルは、OPM セマンティクスを持つ保護された出力に適用されることに注意してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">% CP 保護レベルの値</th>
<th align="left">優先順位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXGKMDT_OPM_DPCP_OFF (0)</p></td>
<td align="left"><p>最低優先順位 (0)</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXGKMDT_OPM_DPCP_ON (1)</p></td>
<td align="left"><p>優先順位が高い (1)</p></td>
</tr>
</tbody>
</table>

 

 

 






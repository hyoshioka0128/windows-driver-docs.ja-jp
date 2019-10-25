---
title: MPEG2_A
description: MPEG2_A
ms.assetid: 4f9e2aad-4072-4a49-87df-dfc6b4bf5f56
keywords:
- MPEG2_A restricted profile WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 421e88d375641edf2540ecd8f322d740ad223b70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840544"
---
# <a name="mpeg2_a"></a>MPEG2\_A


## <span id="ddk_mpeg2_a_gg"></span><span id="DDK_MPEG2_A_GG"></span>


MPEG2\_制限付きプロファイルには、MPEG-2 ビデオメインプロファイルのサポートに必要な一連の機能が含まれています。 このプロファイルのサポートは、ハードウェアのビデオアクセラレータ機能を提供するビデオアクセラレータドライバーに必要です。

プロファイル\_の MPEG2 は、次の制限のセットによって定義されます。

### <a name="span-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanrestrictions-on-dxva_connectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA\_ConnectMode に関する制限事項

[**DXVA\_Configピクチャデコード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)構造体の**dwfunction**メンバーで定義されている*bDXVA\_Func*変数が1と等しい場合は、 [**DXVA\_connectmode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)構造体に対する次の制限が適用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_A</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_pictureparametersspanspan-idrestrictions_on_dxva_pictureparametersspanspan-idrestrictions_on_dxva_pictureparametersspanrestrictions-on-dxva_pictureparameters"></a><span id="Restrictions_on_DXVA_PictureParameters"></span><span id="restrictions_on_dxva_pictureparameters"></span><span id="RESTRICTIONS_ON_DXVA_PICTUREPARAMETERS"></span>DXVA\_ピクチャパラメーターに関する制限事項

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>BPP</em>変数 (1 に bBPPminus1 を追加することで定義<strong>)</strong></p></td>
<td align="left"><p>8</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MacroblockWidthMinus1</strong></p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MacroblockHeightMinus1</strong></p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bBlockWidthMinus1</strong></p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bBlockHeightMinus1</strong></p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bChromaFormat</strong> (4:2:0)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bRcontrol</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>ゼロ (MPEG-2 双方向平均)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>ゼロ (MPEG 2 ハーフサンプルモーション)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>B絵文字の外挿</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B絵文字 Deブロック</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPic4MVallowed</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B絵文字 Obmc</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bMV_RPS</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>固有の Idct</strong></p></td>
<td align="left"><p>回</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>B絵文字 Scanfixed</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanspan-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanspan-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanrestrictions-on-dxva_mbctrl_i_hostresiddiff_1-dxva_mbctrl_i_offhostidct_1-dxva_mbctrl_p_hostresiddiff_1-and-dxva_mbctrl_p_offhostidct_1"></a><span id="Restrictions_on_DXVA_MBctrl_I_HostResidDiff_1__DXVA_MBctrl_I_OffHostIDCT_1__DXVA_MBctrl_P_HostResidDiff_1__and_DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="restrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1"></span><span id="RESTRICTIONS_ON_DXVA_MBCTRL_I_HOSTRESIDDIFF_1__DXVA_MBCTRL_I_OFFHOSTIDCT_1__DXVA_MBCTRL_P_HOSTRESIDDIFF_1__AND_DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_I\_HostResidDiff\_1、DXVA\_MBctrl\_I\_OffHostIDCT\_1、DXVA\_MBctrl\_P\_HostResidDiff\_1、および DXVA\_MBctrl\_P\_OffHostIDCT\_1

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wMBtype ビット</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>MBscanMethod</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode" data-raw-source="[&lt;strong&gt;DXVA_ConfigPictureDecode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)"><strong>DXVA_ConfigPictureDecode</strong></a>の<strong>ConfigHostInverseScan</strong>メンバーが0の場合は、0 (ジグザグ) または 1 (代替の垂直) の値を指定できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>H261LoopFilter</p></td>
<td align="left"><p>回</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_bitstream_buffersspanspan-idrestrictions_on_bitstream_buffersspanspan-idrestrictions_on_bitstream_buffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>ビットストリームバッファーに関する制限事項

ビットストリームバッファーの内容には、MPEG-2 メインプロファイルビデオ形式のデータが含まれている必要があります。

逆量子化行列が使用されている場合、 [**DXVA\_QmatrixData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_qmatrixdata)の**Bnewqmatrix**メンバーは0になり、i = 2 および3になります。

 

 






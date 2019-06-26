---
title: MPEG2_A
description: MPEG2_A
ms.assetid: 4f9e2aad-4072-4a49-87df-dfc6b4bf5f56
keywords:
- MPEG2_A プロファイル WDK DirectX VA を制限します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4af2561413249315ed6e225c570448af736090ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372863"
---
# <a name="mpeg2a"></a>MPEG2\_A


## <span id="ddk_mpeg2_a_gg"></span><span id="DDK_MPEG2_A_GG"></span>


MPEG2\_制限プロファイルには、mpeg-2 ビデオのメイン プロファイルをサポートするために必要な機能のセットが含まれています。 このプロファイルのサポートは、ビデオ アクセラレータ ドライバー ハードウェア ビデオ アクセラレータ機能を提供する必要があります。

MPEG2\_プロファイルは、次の制限のセットによって定義されます。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA に関する制限事項\_ConnectMode

に対して次の制限、 [ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)構造体に適用されるときに、 *bDXVA\_Func* で定義された変数**dwFunction**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)構造体が 1 にします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
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

 

### <a name="span-idrestrictionsondxvapictureparametersspanspan-idrestrictionsondxvapictureparametersspanspan-idrestrictionsondxvapictureparametersspanrestrictions-on-dxvapictureparameters"></a><span id="Restrictions_on_DXVA_PictureParameters"></span><span id="restrictions_on_dxva_pictureparameters"></span><span id="RESTRICTIONS_ON_DXVA_PICTUREPARAMETERS"></span>DXVA に関する制限事項\_PictureParameters

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>BPP</em>変数 (1 を追加することで定義されている<strong>bBPPminus1)</strong></p></td>
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
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>0 (mpeg-2 双方向の平均を計算)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>0 (mpeg-2 半分サンプル モーション)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicExtrapolation</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicDeblocked</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPic4MVallowed</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bMV_RPS</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SpecificIDCT</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicScanFixed</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvambctrlihostresiddiff1dxvambctrlioffhostidct1dxvambctrlphostresiddiff1anddxvambctrlpoffhostidct1spanspan-idrestrictionsondxvambctrlihostresiddiff1dxvambctrlioffhostidct1dxvambctrlphostresiddiff1anddxvambctrlpoffhostidct1spanspan-idrestrictionsondxvambctrlihostresiddiff1dxvambctrlioffhostidct1dxvambctrlphostresiddiff1anddxvambctrlpoffhostidct1spanrestrictions-on-dxvambctrlihostresiddiff1-dxvambctrlioffhostidct1-dxvambctrlphostresiddiff1-and-dxvambctrlpoffhostidct1"></a><span id="Restrictions_on_DXVA_MBctrl_I_HostResidDiff_1__DXVA_MBctrl_I_OffHostIDCT_1__DXVA_MBctrl_P_HostResidDiff_1__and_DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="restrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1"></span><span id="RESTRICTIONS_ON_DXVA_MBCTRL_I_HOSTRESIDDIFF_1__DXVA_MBCTRL_I_OFFHOSTIDCT_1__DXVA_MBCTRL_P_HOSTRESIDDIFF_1__AND_DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA に関する制限事項\_MBctrl\_は\_HostResidDiff\_1、DXVA\_MBctrl\_は\_OffHostIDCT\_1、DXVA\_MBctrl\_P\_HostResidDiff\_1、および DXVA\_MBctrl\_P\_OffHostIDCT\_1

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
<td align="left"><p>場合、0 (ジグザグ) の値または値 1 (代替垂直) することがあります、 <strong>ConfigHostInverseScan</strong>のメンバー <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode" data-raw-source="[&lt;strong&gt;DXVA_ConfigPictureDecode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)"> <strong>DXVA_ConfigPictureDecode</strong> </a>が 0 に等しい。</p></td>
</tr>
<tr class="even">
<td align="left"><p>H261LoopFilter</p></td>
<td align="left"><p>Zero</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>ビット ストリーム バッファーに関する制限事項

ビット ストリーム バッファーの内容は、mpeg-2 メイン プロファイルのビデオ形式でデータを含める必要があります。

**BNewQmatrix**のメンバー [ **DXVA\_QmatrixData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_qmatrixdata)を 0 に等しいは行列の逆行列量子化を使用する場合は、2 および 3 を = です。

 

 






---
title: MPEG1_A
description: MPEG1_A
ms.assetid: 2c4d79b7-3331-49f9-a561-6e5b609543df
keywords:
- MPEG1_A プロファイル WDK DirectX VA を制限します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f230f191c6b5383192f4366dab6940670ef9babd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345641"
---
# <a name="mpeg1a"></a>MPEG1\_A


## <span id="ddk_mpeg1_a_gg"></span><span id="DDK_MPEG1_A_GG"></span>


「MPEG1\_制限プロファイルには、mpeg-1 ビデオをサポートするために必要な機能のセットにはが含まれています。 このプロファイルのサポートは、ビデオ アクセラレータ ドライバー ハードウェア ビデオ アクセラレータ機能を提供する必要があります。 この機能のセットは、次の制限のセットによって定義されます。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA に関する制限事項\_ConnectMode

に対して次の制限、 [ **DXVA\_ConnectMode** ](https://msdn.microsoft.com/library/windows/hardware/ff563138)構造体に適用されるときに、 *bDXVA\_Func* で定義された変数**dwFunction**のメンバー、 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)構造体が 1 にします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体のメンバー</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG1_A</p></td>
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
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>BPP</em>変数 (1 を追加することで定義されている<strong>bBPPminus1)</strong></p></td>
<td align="left"><p>等しい場合 8</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bSecondField</strong></p></td>
<td align="left"><p>0 します。</p></td>
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
<td align="left"><p><strong>bPicStructure</strong></p></td>
<td align="left"><p>3 (構造化されたフレーム)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bRcontrol</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>0 (mpeg-2 双方向の平均を計算)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>0 (mpeg-2 半分サンプル モーション)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicExtrapolation</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicDeblocked</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPic4MVallowed</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicOBMC</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMV_RPS</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SpecificIDCT</strong></p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicScanFixed</strong></p></td>
<td align="left"><p>Zero</p></td>
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
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>MotionType</em></p></td>
<td align="left"><p>2 (フレーム アニメーション)</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>MBscanMethod</em></p></td>
<td align="left"><p>(ジグザグ) の場合は 0 <strong>bConfigHostInverseScan</strong>が 0 に等しい</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>FieldResidual</em></p></td>
<td align="left"><p>0 (フレーム残存)</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>H261LoopFilter</em></p></td>
<td align="left"><p>0 (H.261 ループ フィルターなし)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>ビット ストリーム バッファーに関する制限事項

ビット ストリーム バッファーの内容は、mpeg-1 メイン プロファイルのビデオ形式でデータを含める必要があります。

 

 






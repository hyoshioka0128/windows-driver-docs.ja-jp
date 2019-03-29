---
title: MPEG2_B
description: MPEG2_B
ms.assetid: 7d67f0ef-a5eb-40db-9f00-6f652d28e530
keywords:
- MPEG2_B プロファイル WDK DirectX VA を制限します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95df63ab479eb2da8abd59ec991ba6ca8e0269b8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349819"
---
# <a name="mpeg2b"></a>MPEG2\_B


## <span id="ddk_mpeg2_b_gg"></span><span id="DDK_MPEG2_B_GG"></span>


MPEG2\_B の制限プロファイルには、mpeg-2 ビデオのメイン プロファイルとフロント エンドのバッファーのサブピクチャ ブレンドを使用して、関連付けられている DVD サブピクチャをサポートするために必要な機能のセットが含まれています。 アルファ ブレンドのソースと宛先表面がそれぞれの少なくとも 720 と 576 の幅と高さでサポートされます。 このプロファイルのサポートは現在推奨しますが、必要ありません。

[MPEG2\_A](mpeg2-a.md) 、MPEG2 のアクセラレータの要件を緩和したトークンによって制限されているプロファイルが定義されている\_B プロファイル、MPEG2 をサポートするすべてのアクセラレータ\_B のプロファイルをサポートする必要がありますMPEG2\_プロファイル。

MPEG2 に対する制限\_B が MPEG2 用に示された制限によって定義されている\_A は、以下の制限を除く。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA に関する制限事項\_ConnectMode

これらの値の*bDXVA\_Func*変数をサポートする必要があります。(図のデコード) 1、2 (アルファ ブレンドのデータの読み込み)、または 3 (アルファ ブレンドの組み合わせ)。

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
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_B</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigalphaloadanddxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphaloadanddxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphaloadanddxvaconfigalphacombinespanrestrictions-on-dxvaconfigalphaload-and-dxvaconfigalphacombine"></a><span id="Restrictions_on_DXVA_ConfigAlphaLoad_and_DXVA_ConfigAlphaCombine"></span><span id="restrictions_on_dxva_configalphaload_and_dxva_configalphacombine"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHALOAD_AND_DXVA_CONFIGALPHACOMBINE"></span>DXVA に関する制限事項\_ConfigAlphaLoad と DXVA\_ConfigAlphaCombine

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
<td align="left"><p><strong>bConfigBlendType</strong> (DXVA_ConfigAlphaCombine)</p></td>
<td align="left"><p>0 (フロント エンド バッファー間ブレンド)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigDataType</strong> (DXVA_ConfigAlphaLoad)</p></td>
<td align="left"><p>0、1、または 3 (アクセラレータの裁量)</p></td>
</tr>
</tbody>
</table>

 

 

 






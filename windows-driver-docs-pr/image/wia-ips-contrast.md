---
title: WIA\_IP\_コントラスト
description: WIA\_IP\_コントラスト プロパティには、デバイスの現在のハードウェア コントラスト設定が含まれています。
ms.assetid: 7fecfd43-212c-40e6-8520-ef1819448895
keywords:
- WIA_IPS_CONTRAST イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_CONTRAST
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 806f6358df3fb4927f980b4cf6d33e7f9bba0b9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370615"
---
# <a name="wiaipscontrast"></a>WIA\_IP\_コントラスト


WIA\_IP\_コントラスト プロパティには、デバイスの現在のハードウェア コントラスト設定が含まれています。

## <span id="ddk_wia_ips_contrast_si"></span><span id="DDK_WIA_IPS_CONTRAST_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定、WIA\_IP\_コントラストのプロパティをハードウェアのコントラストの値にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。

Wia 値\_IP\_コントラストを −1000 1000、−1000 が最低限のコントラストに対応して、0 は、通常のコントラストに対応およびコントラストが最大に対応する 1000 の範囲にマップする必要があります。

WIA\_IP\_のすべてのイメージの取得項目は、コントラストが必要です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 






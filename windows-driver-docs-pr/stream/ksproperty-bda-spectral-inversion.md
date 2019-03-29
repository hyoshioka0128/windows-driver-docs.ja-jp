---
title: KSPROPERTY\_BDA\_スペクトル\_逆転
description: クライアントを使用して、KSPROPERTY\_BDA\_スペクトル\_逆転復調器ノードのスペクトルの反転の設定を制御します。
ms.assetid: a51dee0b-4a45-4159-978b-27ff6e2333e2
keywords:
- KSPROPERTY_BDA_SPECTRAL_INVERSION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SPECTRAL_INVERSION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: edb2e4962397c8cca15f1f571e9b6805361fb4af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570627"
---
# <a name="kspropertybdaspectralinversion"></a>KSPROPERTY\_BDA\_スペクトル\_逆転


クライアントを使用して、KSPROPERTY\_BDA\_スペクトル\_逆転復調器ノードのスペクトルの反転の設定を制御します。

## <span id="ddk_ksproperty_bda_spectral_inversion_ks"></span><span id="DDK_KSPROPERTY_BDA_SPECTRAL_INVERSION_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>SpectralInversion</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

SpectralInversion 列挙型から返される値は、スペクトルの逆転の設定を指定します。

**NodeId** KSP のメンバー\_ノード復調器ノードの識別子を指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

[**SpectralInversion**](https://msdn.microsoft.com/library/windows/hardware/ff568154)

 

 







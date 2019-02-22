---
title: KSPROPERTY\_BDA\_LNB\_LOF\_高\_バンド
description: クライアントを使用して、KSPROPERTY\_BDA\_LNB\_LOF\_高\_バンド RF チューナーのノードを移行する低ノイズ ブロック (LNB) デバイスで使用されるローカル オシレーター頻度 (LOF) に通知するために、高帯域 RF 信号の受信の頻度です。
ms.assetid: 77ee5ad8-330e-47a6-8fdb-6a4f9b3eef1d
keywords:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_LOF_HIGH_BAND
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24728d55e8e00f36c353f9209b6a4ed4b2c0aa71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551774"
---
# <a name="kspropertybdalnblofhighband"></a>KSPROPERTY\_BDA\_LNB\_LOF\_高\_バンド


クライアントを使用して、KSPROPERTY\_BDA\_LNB\_LOF\_高\_バンド RF チューナーのノードを移行する低ノイズ ブロック (LNB) デバイスで使用されるローカル オシレーター頻度 (LOF) に通知するために、高帯域 RF 信号の受信の頻度です。

## <span id="ddk_ksproperty_bda_lnb_lof_high_band_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_LOF_HIGH_BAND_KS"></span>


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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**NodeId** KSP のメンバー\_ノードは、RF チューナーのノードの識別子を指定します。

プロパティの値には、高帯域信号、LNB によって使用される LOF を指定します。

LNB RF 信号を衛星アンテナがリフレクションを収集するには、高帯域 LOF amount では、下、RF 信号の頻度にシフトおよび RF チューナーを結果として得られる信号を送信します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 







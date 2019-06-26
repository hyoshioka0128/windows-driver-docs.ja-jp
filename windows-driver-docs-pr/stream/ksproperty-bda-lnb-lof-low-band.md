---
title: KSPROPERTY\_BDA\_LNB\_LOF\_低\_バンド
description: クライアントを使用して、KSPROPERTY\_BDA\_LNB\_LOF\_低\_バンド RF チューナーのノードを移行する低ノイズ ブロック (LNB) デバイスで使用されるローカル オシレーター頻度 (LOF) に通知するために、低帯域 RF 信号の受信の頻度です。
ms.assetid: 96880a70-5c3f-4391-a613-a6a90d1605b4
keywords:
- KSPROPERTY_BDA_LNB_LOF_LOW_BAND ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_LOF_LOW_BAND
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 239f5a6fb425162270d2903455e594afff466d72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364852"
---
# <a name="kspropertybdalnbloflowband"></a>KSPROPERTY\_BDA\_LNB\_LOF\_低\_バンド


クライアントを使用して、KSPROPERTY\_BDA\_LNB\_LOF\_低\_バンド RF チューナーのノードを移行する低ノイズ ブロック (LNB) デバイスで使用されるローカル オシレーター頻度 (LOF) に通知するために、低帯域 RF 信号の受信の頻度です。

## <span id="ddk_ksproperty_bda_lnb_lof_low_band_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_LOF_LOW_BAND_KS"></span>


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

プロパティの値には、低帯域信号、LNB によって使用される LOF を指定します。

LNB RF 信号を衛星アンテナがリフレクションを収集するには、RF 信号の頻度を低帯域 LOF amount では、下にシフトおよび RF チューナーを結果として得られる信号を送信します。

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


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 







---
title: KSPROPERTY\_BDA\_LNB\_スイッチ\_頻度
description: クライアントを使用して、KSPROPERTY\_BDA\_LNB\_切り替える\_チューナー位置から切り替えるには、低ノイズ ブロック (LNB) デバイスに通知する必要があります RF 信号の受信の頻度、RF チューナー ノードに通知する頻度高帯域 LOF を使用するまたはその逆の場合、LNB RF 信号の頻度にシフトすると、低帯域ローカル オシレーター頻度 (LOF) を使用します。
ms.assetid: a448bad1-40dc-4596-bc18-9522144e33a7
keywords:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93fbc8e83491bae5d94a14d1d4ef61adb0150ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376666"
---
# <a name="kspropertybdalnbswitchfrequency"></a>KSPROPERTY\_BDA\_LNB\_スイッチ\_頻度


クライアントを使用して、KSPROPERTY\_BDA\_LNB\_切り替える\_チューナー位置から切り替えるには、低ノイズ ブロック (LNB) デバイスに通知する必要があります RF 信号の受信の頻度、RF チューナー ノードに通知する頻度高帯域 LOF を使用するまたはその逆の場合、LNB RF 信号の頻度にシフトすると、低帯域ローカル オシレーター頻度 (LOF) を使用します。

## <span id="ddk_ksproperty_bda_lnb_switch_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY_KS"></span>


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

プロパティの値には、高帯域 LOF を使用する低帯域 LOF を使用して切り替える必要があります、LNB を RF 信号の受信の頻度を指定します。

クライアントが送信、KSPROPERTY 場合\_BDA\_RF\_チューナー\_RF チューナーは、特定の頻度と、この頻度を調整する頻度の要求が KSPROPERTY を使用して指定されたスイッチ頻度以上\_BDA\_LNB\_切り替える\_し、頻度、RF チューナーは、高帯域 LOF に切り替える LNB にコマンドを送信する必要があります。 RF チューナーが LNB デバイスが KSPROPERTY を使用して指定されている高帯域 LOF 量によって RF 信号を受信の頻度を移動することを期待する必要がありますし、\_BDA\_LNB\_LOF\_高\_バンド。

同様に、クライアントが送信、KSPROPERTY 場合\_BDA\_RF\_チューナー\_RF チューナーは、特定の頻度と、この頻度を調整する頻度の要求は、切り替えの頻度よりも小さい、RF チューナーを送信する必要があります、低帯域 LOF に切り替える、LNB するコマンドです。 RF チューナーが LNB デバイスが KSPROPERTY を使用して指定された、低帯域 LOF 金額によって RF 信号を受信の頻度を移動することを期待する必要がありますし、\_BDA\_LNB\_LOF\_低\_バンド。

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


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_LNB\_LOF\_高\_バンド**](ksproperty-bda-lnb-lof-high-band.md)

[**KSPROPERTY\_BDA\_LNB\_LOF\_低\_バンド**](ksproperty-bda-lnb-lof-low-band.md)

[**KSPROPERTY\_BDA\_RF\_チューナー\_頻度**](ksproperty-bda-rf-tuner-frequency.md)

 

 







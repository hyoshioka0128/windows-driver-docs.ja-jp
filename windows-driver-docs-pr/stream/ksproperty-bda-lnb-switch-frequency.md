---
title: KSK プロパティ\_BDA\_LNB\_スイッチ\_頻度
description: クライアントは、KSK プロパティ\_BDA\_LNB\_スイッチ\_頻度を使用して、チューナーが低騒音ブロック (LNB) デバイスに対して低帯域ローカルの使用から切り替えるように通知する着信 RF 信号の周波数について、RF チューナーノードに通知します。オシレーターが RF 信号の周波数をシフトするときに高帯域の LOF またはその逆を使用するためのオシレーター周波数 (LOF)。
ms.assetid: a448bad1-40dc-4596-bc18-9522144e33a7
keywords:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY ストリーミングメディアデバイス
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
ms.openlocfilehash: b4b409e9248bf0bb63b62bf3adceeb2d34d5eadf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845145"
---
# <a name="ksproperty_bda_lnb_switch_frequency"></a>KSK プロパティ\_BDA\_LNB\_スイッチ\_頻度


クライアントは、KSK プロパティ\_BDA\_LNB\_スイッチ\_頻度を使用して、チューナーが低騒音ブロック (LNB) デバイスに対して低帯域ローカルの使用から切り替えるように通知する着信 RF 信号の周波数について、RF チューナーノードに通知します。オシレーターが RF 信号の周波数をシフトするときに高帯域の LOF またはその逆を使用するためのオシレーター周波数 (LOF)。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP の**NodeId**メンバー\_node は、RF チューナーノードの識別子を指定します。

プロパティ値は、着信 RF シグナルの頻度を指定します。これは、LNB がローバンドの lof を使用して、高帯域の LOF を使用するように切り替える必要があります。

クライアントが KSK プロパティ\_BDA\_送信した場合、rf チューナーを特定の周波数にチューニングするための周波数\_チューナー\_頻度の要求が発生します。この頻度は、KSK プロパティ\_BDA を使用して指定されたスイッチの頻度以上になり\_LNB\_スイッチ\_周波数に切り替えると、RF チューナーは、高帯域の LOF に切り替えるコマンドを LNB に送信する必要があります。 次に、RF チューナーは、LNB デバイスが受信 RF 信号の周波数を高さが大きくなることを期待する必要があります。これは、KSK プロパティ\_BDA\_LNB\_LOF\_高\_を使用して指定されています。

同様に、クライアントが KSK プロパティ\_BDA\_RF\_チューナー\_頻度を指定して RF チューナーを特定の周波数に調整するように要求していて、この頻度がスイッチの頻度より小さい場合、RF チューナーは LNB にコマンドを送信してスイッチを切り替えます。低帯域の LOF に。 次に、RF チューナーは、LNB デバイスが帯域幅の増加によって受信 RF 信号の周波数をシフトすることを想定します。この量は、KSPROPERTY\_BDA\_LNB\_LOF\_低\_帯域を使用して指定されています。

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
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ノード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)

[**KSK プロパティ\_BDA\_LNB\_LOF\_高\_帯域**](ksproperty-bda-lnb-lof-high-band.md)

[**KSK プロパティ\_BDA\_LNB\_LOF\_低\_帯域**](ksproperty-bda-lnb-lof-low-band.md)

[**KSK プロパティ\_BDA\_RF\_チューナー\_頻度**](ksproperty-bda-rf-tuner-frequency.md)

 

 







---
title: KSPROPERTY\_ジャック\_CONTAINERID
description: KSPROPERTY\_ジャック\_CONTAINERID プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。
ms.assetid: 01A157B0-41EE-4713-B5D3-B9BF9C2B80CE
keywords:
- KSPROPERTY_JACK_CONTAINERID オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_CONTAINERID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b741cc917ea2c737c27aa1f9163b012a2a067175
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358772"
---
# <a name="kspropertyjackcontainerid"></a>KSPROPERTY\_ジャック\_CONTAINERID


KSPROPERTY\_ジャック\_CONTAINERID プロパティは、フィルターのハンドルを使用してアクセスされる pin-wise プロパティとして実装されます。

このプロパティは、1 つまたは複数の物理ジャック、またはその他のワイヤード (有線) またはワイヤレス接続に関連付けられているブリッジ暗証番号 (pin) をサポートできます。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>(フィルターのハンドル) を使用してファクトリをピン留めします。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><strong>GUID</strong></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (インスタンス データ) は、GUID です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_ジャック\_CONTAINERID プロパティ要求が物理ジャック、またはその他のワイヤード (有線) またはワイヤレス接続に関連付けられているデバイスのコンテナーの ID を持つ GUID を返します。

<a name="remarks"></a>注釈
-------

オーディオ ドライバーは、次の条件に当てはまる場合にのみ、このプロパティをサポートする必要があります。

-   関連付けられているオーディオ デバイスのコンテナー ID は、オーディオ ドライバーが読み込まれる対象のデバイス ノードのコンテナーの ID と異なるです。

-   ドライバーは、他の手段で適切なコンテナー ID を取得できます。

KSPROPERTY\_ジャック\_CONTAINERID プロパティは、オーディオのエンドポイントがプラスチックのオーディオのアダプターからのさまざまな部分にある場合に設定されることにのみ必要があります。 既定では、オーディオのエンドポイントは、親のコンテナーの ID を継承します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**BTHHFP\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)

[**IOCTL\_BTHHFP\_DEVICE\_GET\_CONTAINERID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

 

 







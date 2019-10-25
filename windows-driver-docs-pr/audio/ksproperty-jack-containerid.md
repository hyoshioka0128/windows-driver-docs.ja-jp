---
title: KSK プロパティ\_ジャック\_CONTAINERID
description: KSK プロパティ\_JACK\_CONTAINERID プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。
ms.assetid: 01A157B0-41EE-4713-B5D3-B9BF9C2B80CE
keywords:
- KSPROPERTY_JACK_CONTAINERID オーディオデバイス
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
ms.openlocfilehash: 74037d3400203ef5e32178311a15fd33efdba61e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832747"
---
# <a name="ksproperty_jack_containerid"></a>KSK プロパティ\_ジャック\_CONTAINERID


KSK プロパティ\_JACK\_CONTAINERID プロパティは、フィルターハンドルを使用してアクセスされるピン方向のプロパティとして実装されます。

このプロパティは、1つまたは複数の物理ジャック、または他のワイヤード (有線) またはワイヤレス接続に関連付けられている任意のブリッジピンでサポートできます。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>Pin ファクトリ (フィルターハンドル経由)</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><strong>GUID</strong></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (インスタンスデータ) は GUID です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_JACK\_CONTAINERID プロパティ要求は、物理ジャック、またはその他のワイヤード (有線) またはワイヤレス接続に関連付けられているデバイスのコンテナー ID を持つ GUID を返します。

<a name="remarks"></a>注釈
-------

オーディオドライバーは、次の条件に該当する場合にのみ、このプロパティをサポートする必要があります。

-   関連付けられたオーディオデバイスのコンテナー ID が、オーディオドライバーが読み込まれるデバイスノードのコンテナー ID と異なります。

-   ドライバーは、他の方法で正しいコンテナー ID を取得できます。

オーディオエンドポイントがオーディオアダプターの別のプラスチック部分にある場合にのみ、KSK プロパティ\_ジャック\_CONTAINERID プロパティに値を設定する必要があります。 既定では、オーディオエンドポイントは親のコンテナー ID を継承します。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**BTHHFP\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)

[**IOCTL\_BTHHFP\_デバイス\_\_の CONTAINERID を取得する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

 

 







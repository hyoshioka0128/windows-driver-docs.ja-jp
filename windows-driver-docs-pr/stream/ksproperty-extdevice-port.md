---
title: KSK プロパティ\_EXTDEVICE\_ポート
description: KSK プロパティ\_EXTDEVICE\_PORT プロパティは、外部デバイスのポートの種類を取得します。
ms.assetid: 7513c37f-0c93-4078-ba85-cbc98304880f
keywords:
- KSPROPERTY_EXTDEVICE_PORT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_PORT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d04b1a9781ab39ae60d36c2b1accc68261217b48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827028"
---
# <a name="ksproperty_extdevice_port"></a>KSK プロパティ\_EXTDEVICE\_ポート


KSK プロパティ\_EXTDEVICE\_PORT プロパティは、外部デバイスのポートの種類を取得します。

## <span id="ddk_ksproperty_extdevice_port_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_PORT_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、外部デバイスの接続ポートを指定する ULONG です。 たとえば、1394や USB などです。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_EXTDEVICE\_S 構造体の**Devport**メンバーは、外部デバイスのポートの種類を指定します。 **Devport**メンバーは、DEV\_port\_1394、DEV\_ポート\_USB などと等しいように設定できます。これらのトークンは、Microsoft DirectX SDK の*xprtdefs*ファイルで定義されています。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_EXTDEVICE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

 

 







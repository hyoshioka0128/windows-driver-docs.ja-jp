---
title: KSK プロパティ\_固定\_PHYSICALCONNECTION
description: オーディオアダプターのドライバーは、KSK プロパティ\_ピン留め\_PHYSICALCONNECTION プロパティを使用して、ミニポート間の物理的な接続を表します。
ms.assetid: a679ce41-93d2-4b46-a26d-ce05408ec6aa
keywords:
- KSPROPERTY_PIN_PHYSICALCONNECTION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PHYSICALCONNECTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e7c18cc45c48953a7ab335fdf4bb7ad5cf9898b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838846"
---
# <a name="ksproperty_pin_physicalconnection"></a>KSK プロパティ\_固定\_PHYSICALCONNECTION


オーディオアダプターのドライバーは、KSK プロパティ\_ピン留め\_PHYSICALCONNECTION プロパティを使用して、ミニポート間の物理的な接続を表します。

## <span id="ddk_ksproperty_pin_physicalconnection_ks"></span><span id="DDK_KSPROPERTY_PIN_PHYSICALCONNECTION_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection" data-raw-source="[&lt;strong&gt;KSPIN_PHYSICALCONNECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection)"><strong>KSPIN_PHYSICALCONNECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、KSP\_PIN を使用して指定します。この場合、メンバーは関連するピンファクトリを指定します。

KSK プロパティ\_ピン\_PHYSICALCONNECTION は、接続されている**Pinid**と接続されたフィルターのシンボリックリンク名を指定して、 [**KSPIN\_physicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection)型の構造を返します。

クラスドライバーは、このプロパティを処理しません。stream ミニドライバーは、独自の処理を提供する必要があります。

オーディオアダプターのドライバーは、 [**Pcregiphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)を使用して接続を登録します。

その後、SysAudio システムドライバー (*sysaudio .sys*) がこのプロパティに対してクエリを行い、それに応じてグラフを構築します。 SysAudio は、このプロパティを使用して、どの電波フィルターピンがどのトポロジフィルターピン留めに接続されているかを判断します。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ピン留め**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSPIN\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection)

[**Pcregiphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)

 

 







---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_EVCOMPENSATION
description: EV 補正プロパティを使用すると、露出単位またはゾーンシステムごとに露出制御を調整できます。
ms.assetid: 1109C533-89CA-4A23-BCF9-D44C28C0C6BF
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: ad2804df6d3e76383fa8a05428dab718f6ac631b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843241"
---
# <a name="ksproperty_cameracontrol_extended_evcompensation"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_EVCOMPENSATION


EV 補正プロパティを使用すると、露出単位またはゾーンシステムごとに露出制御を調整できます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造、および[**KSCAMERA\_EXTENDEDPROP\_evcompensation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_evcompensation) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、次の補正設定の1つ以上のビットごとの or の組み合わせが含まれています。

| EV 補正のステップ実行                    | 説明                                                             |
|---------------------------------------------|-------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_SIXTHSTEP   | エクスポージャーの補正は、露出値の6番目の (1/6) ステップで変更されます。  |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_QUARTERSTEP | EV の補正は、露出値の1番目の4つのステップ (1/4) で変更されます。 |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_THIRDSTEP   | EV の補正は、露出値の3番目の (1/3) ステップで変更されます。  |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_ハーフステップ    | EV 値の1半 (1/2) ステップで EV 補正が変更されます。   |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_FULLSTEP    | EV の補正は、露出値の1つの (1/1) ステップで変更されます。        |

 

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラの現在の EV 補正ステップ (1 つの値) が含まれています。最小 EV 補正ステップサイズに対してのみ、のサポートを提供するために、ドライバーを使用することをお勧めします。

このプロパティコントロールは非同期であり、キャンセルできません。

<a name="remarks"></a>注釈
-------

### <a name="getting-the-property"></a>プロパティを取得する

\_GET 要求の種類\_KSK プロパティに応答すると、ドライバーは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>バージョン</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_EVCOMPENSATION)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>ドライバーでサポートされているステップ実行フラグ。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のステッピング値のセット。</td>
</tr>
</tbody>
</table>

 

ドライバーは、現在の EV 補正ステップイン**フラグ**を設定します。 [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)のメンバーは、現在のステップ単位の範囲と、での補正のために使用されているステップの数を示します。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、使用する EV 補正ステップが含まれます。 補正に使用される新しいステップ単位の数は、 [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)の**値**メンバーで設定されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)

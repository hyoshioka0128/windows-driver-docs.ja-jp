---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOTRIGGERTIME
description: このプロパティは、カメラドライバーのトリガー時間を制御します。 トリガー時間は、フォトシーケンスの参照フレームの決定に使用されます。
ms.assetid: C0DE5F4D-9566-4D8C-9061-D397577E89E2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4905ddace589288de49af1a386138b61014bf28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824031"
---
# <a name="ksproperty_cameracontrol_extended_phototriggertime"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOTRIGGERTIME

このプロパティは、カメラドライバーのトリガー時間を制御します。 トリガー時間は、フォトシーケンスの参照フレームの決定に使用されます。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。 Photo トリガー時間 (100 ナノ秒単位) が設定されているか、 **KSCAMERA\_EXTENDEDPROP\_値**の値として返されます。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

トリガー時間は、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**flags**メンバーに含まれる次のフラグのいずれかを使用して設定またはクリアされます。

| トリガー時間フラグ                           | 説明                     |
|---------------------------------------------|---------------------------------|
| KSK プロパティ\_カメラ\_PHOTOTRIGGERTIME\_クリア | [トリガー時間] の設定をオフにします。 |
| KSK プロパティ\_カメラ\_PHOTOTRIGGERTIME\_設定   | 新しいトリガー時間値を設定します。   |

このプロパティコントロールは同期であり、キャンセルできません。

## <a name="remarks"></a>注釈

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
<td>フォト pin の pin ID。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) +</p>
<p>sizeof (KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td><p>最大フレームレートを読み取ろうとした結果のエラー値。</p>
<p>それ以外の場合は0です。</p></td>
</tr>
<tr class="odd">
<td>機能</td>
<td>0</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>フラグの設定またはクリア</td>
</tr>
</tbody>
</table>

トリガー時刻が現在の時刻値に設定されていない場合は、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、\_phototriggertime\_の値が指定されていなければ、ksk プロパティ\_カメラが含まれている必要があります。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の**u)** メンバーには、trigger time 値が格納されます。 トリガー時間は、操作フラグに基づいて設定またはクリアされます。 フラグが KSK プロパティ\_カメラ\_PHOTOTRIGGERTIME\_**KSCAMERA\_EXTENDEDPROP**の値をクリアすると\_値は使用されず、無視されます。

## <a name="requirements"></a>要件

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

---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_TORCHMODE
description: Torch モードは、低負荷状態でカメラのフラッシュをどのように使用するかを決定します。
ms.assetid: FB168F4E-EBF9-4925-B4F1-BC9305DB0109
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: aba1ce6a13a1bae78069499f1d2942a43e24ed65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823940"
---
# <a name="ksproperty_cameracontrol_extended_torchmode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_TORCHMODE

Torch モードは、低負荷状態でカメラのフラッシュをどのように使用するかを決定します。 フラッシュにより低輝度の光源が継続的に提供されるため、自動フォーカスなどの操作に十分な光を得ることができます。

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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、ドライバーでサポートされている次の torch モードの1つ以上のビットごとの or の組み合わせが含まれています。

| Torch モード                                              | 説明                                      |
|---------------------------------------------------------|--------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_OFF                 | Torchlight がオフになっています。                               |
| KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_ON                  | Torchlight は既定の強度レベルでオンになっています。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_\_ADJUSTABLEPOWER | Torchlight は特定の電源レベルでオンになっています。      |

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されている torch モードが含まれています。 カメラの既定の torch モードは KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_OFF で、ドライバーはこの torch モードをサポートしている必要があります。

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
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>Torch モードの値がサポートされています。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在の torch mode 値の設定 (1 つの値のみ)。</td>
</tr>
</tbody>
</table>

Torch モードが KSCAMERA\_EXTENDEDPROP\_\_ADJUSTABLEPOWER の VIDEOTORCH\_の場合、U) の KSCAMERA メンバー [ **\_extendedprop\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)には、0-100 ~ の範囲の値が含まれます **。** 明度が0の場合は最小レベル、輝度が100の場合は最大輝度レベルを示します。

シーンモードが以前に設定されていない場合、 **Flags**は KSCAMERA\_extendedprop\_VIDEOTORCH\_OFF (既定) に設定されます。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーに設定する torch モードが含まれます。 [**KSCAMERA\_extendedprop\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の**u)** メンバーには、**フラグ**が KSCAMERA\_EXTENDEDPROP\_VIDEOTORCH\_ON\_ADJUSTABLEPOWER に設定する輝度レベルが含まれます。

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

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)

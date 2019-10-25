---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL
description: このプロパティは、カメラのサムネイル機能を取得または設定します。
ms.assetid: 859620FD-02ED-4AA1-83B7-B92517F23B0C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ca52ff00eaa31ff4a8d5203bc540b6e3d93142ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824036"
---
# <a name="ksproperty_cameracontrol_extended_photothumbnail"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL

このプロパティは、カメラのサムネイル機能を取得または設定します。 スケールファクターが指定されている場合は、選択したスケールでサムネイルが有効になります。

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

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。 **KSCAMERA\_EXTENDEDPROP\_値**が必要ですが、**値**メンバーは無視されます。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、サポートされる次のスケール値の1つ以上のビットごとの or の組み合わせが含まれています。

| 縮小表示のスケールフラグ                            | 説明                            |
|-------------------------------------------------|----------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_DISABLE | サムネイルは無効になっています。               |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_2      | サムネイルの解像度は X/2 および Y/2 です。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_2      | サムネイルの解像度は X/4 および Y/4 です。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_8X      | サムネイルの解像度は X/8 と Y/8 です。   |
| KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_16X     | サムネイルの解像度は、X/16 および Y/16 です。 |

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されているサムネイルのスケール値が含まれます。 サムネイルの生成が有効になっていない場合は、KSCAMERA\_EXTENDEDPROP\_PHOTOTHUMBNAIL\_DISABLE が**フラグ**に設定されています。

このプロパティコントロールは非同期であり、キャンセルできません。

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
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td><p>サムネイルの設定を取得しようとしたときのエラー値。</p></td>
</tr>
<tr class="odd">
<td>機能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(サムネイルの小数点以下桁数はサポートされています)。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のサムネイル値の設定 (1 つの値のみ)。</td>
</tr>
</tbody>
</table>

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**flags**メンバーにサムネイルスケールフラグのいずれかが含まれます。

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

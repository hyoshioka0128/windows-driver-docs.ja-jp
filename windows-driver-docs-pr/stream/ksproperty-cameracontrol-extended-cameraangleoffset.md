---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_CAMERAANGLEOFFSET
description: "\"カメラアングルオフセット\" プロパティは、カメラの位置のピッチとヨーの角度に関する読み取り専用の情報を提供します。 ピッチとヨー角度は、水平軸と垂直軸からのオフセットとして定義されます。"
ms.assetid: 06F62EB9-DAF7-486F-9940-24EA2224BCB0
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c6a51073eaffb8f834f1836e0df1580f1b17748
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843243"
---
# <a name="ksproperty_cameracontrol_extended_cameraangleoffset"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_CAMERAANGLEOFFSET

"カメラアングルオフセット" プロパティは、カメラの位置のピッチとヨーの角度に関する読み取り専用の情報を提供します。 ピッチとヨー角度は、水平軸と垂直軸からのオフセットとして定義されます。

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
<td><p>必須ではない</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と、FIELDOFVIEW 構造体の[**KSCAMERA\_extendedprop\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_FIELDOFVIEW) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**と**フラグ**のメンバーは、このプロパティには使用されません。

ドライバーがカメラの正しいビューのフィールドを判別できない場合、ドライバーはこのプロパティのサポートを示すことはできません。

このプロパティコントロールは同期であり、キャンセルできません。

## <a name="remarks"></a>注釈

カメラセンサーとジャイロセンサーが両方とも同じ物理シャーシに格納されている場合は、カメラドライバーが適切なオフセット角度を報告することをお勧めします。これは0°にすることをお勧めします。 カメラセンサーとジャイロセンサーが同じ物理シャーシに置かれていない場合は、このプロパティのサポートを示さないようにドライバーを使用することをお勧めします。

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
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_CAMERAOFFSET)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>0</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>0</td>
</tr>
</tbody>
</table>

 

ドライバーは、 [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)構造体の角度オフセットを設定します。

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

[**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)

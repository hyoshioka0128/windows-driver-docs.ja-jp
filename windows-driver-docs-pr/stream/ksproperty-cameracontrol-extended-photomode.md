---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOMODE
description: このプロパティは、カメラの写真モード設定を設定または取得します。
ms.assetid: C9596B85-A07B-4DF7-852F-C9EBF43E1E44
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30ac87621ead72243c7e3eb2aca0ddab26229070
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824041"
---
# <a name="ksproperty_cameracontrol_extended_photomode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOMODE

このプロパティは、カメラの写真モード設定を設定または取得します。

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

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_photomode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)構造体が含まれています。 これらは、シーケンスモードが設定されている場合に、写真モードと履歴フレーム数を指定します。

目的の写真モードは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーで設定されます。 Photo モードは、次のいずれかに設定されます。

| 写真モード                                  | 説明                      |
|---------------------------------------------|----------------------------------|
| KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_通常   | 通常の写真操作     |
| KSCAMERA\_EXTENDEDPROP\_PHOTOMODE\_SEQUENCE | 写真シーケンスのキャプチャ操作 |

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_photomode) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

> [!NOTE]
> Photo モードの設定は非同期制御操作であり、KSCAMERA\_EXTENDEDPROP\_CAP\_ASYNCCONTROL は、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーで設定する必要があります。

## <a name="remarks"></a>注釈

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
<p>sizeof (KSCAMERA_EXTENDEDPROP_PHOTOMODE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td><p>フォトモードデータを取得しようとしたときのエラー値。</p>
<p>それ以外の場合は0です。</p></td>
</tr>
<tr class="odd">
<td>機能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在の写真モード。</td>
</tr>
</tbody>
</table>

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

[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)

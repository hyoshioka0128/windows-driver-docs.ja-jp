---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_の起動
description: ウォームスタートプロパティコントロールは、カメラの pin を維持して、障害のない操作を可能にするためのヒントをドライバーに提供します。
ms.assetid: EAC20371-6228-48F1-85FF-FAECC835B070
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART
api_type:
- NA
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0f246eb3a38e64f5bd3c7b4c1082bcee15d1ced9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837845"
---
# <a name="ksproperty_cameracontrol_extended_warmstart"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_の起動

ウォームスタートプロパティコントロールは、カメラの pin を維持して、障害のない操作を可能にするためのヒントをドライバーに提供します。

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

プロパティ値 (操作データ) には、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体が含まれています。

このプロパティの[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**flags**メンバーには、フラグが設定されていません。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

ウォームスタートは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーにある次のいずれかのフラグを使用して有効または無効にします。

| ウォーム開始フラグ                                  | 説明             |
|---------------------------------------------------|-------------------------|
| KSCAMERA\_EXTENDEDPROP\_\_モード\_無効 | ウォームスタートは無効になっています。 |
| KSCAMERA\_EXTENDEDPROP\_\_モード\_有効  | ウォームスタートが有効になっています。  |

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
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |KSCAMERA_EXTENDEDPROP_WARMSTART_MODE_DISABLED</p>
<p>\- または -</p>
<p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |KSCAMERA_EXTENDEDPROP_WARMSTART_MODE_ENABLED</p></td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>0</td>
</tr>
</tbody>
</table>

Get 操作では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**結果**メンバーは常に0に設定されます。

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSSTATE
description: Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSSTATE プロパティ ID\_で定義されている CAMERACONTROL\_拡張\_プロパティ列挙を使用して、ドライバーからフォーカス状態を取得します。 これは、読み取り専用のフィルターレベルのプロパティです。
ms.assetid: 53D54443-59AD-4078-BD13-CB193B89E488
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSSTATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSSTATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 28c7cbf816661519837be2aadef01c2d6dd31410
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844835"
---
# <a name="ksproperty_cameracontrol_extended_focusstate"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSSTATE

Ksk プロパティ **\_CAMERACONTROL\_extended\_FOCUSSTATE**プロパティ ID\_で定義されている[**CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙を使用して、フォーカス状態をdriver. これは、読み取り専用のフィルターレベルのプロパティです。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>適用範囲</th>
<th>コントロール</th>
<th>タスクバーの検索ボックスに</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>フィルター</p></td>
<td><p>同期 (読み取り専用)</p></td>
</tr>
</tbody>
</table>

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の場合、flags 値にはカメラドライバーによって返されるフォーカス状態が含まれます。 これは、同期 get のみの制御です。 使用可能なフォーカス状態の値は、 [**KSCAMERA\_EXTENDEDPROP\_FOCUSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)列挙に示されます。

次の表には、フォーカス状態コントロールを使用する場合の**KSCAMERA\_EXTENDEDPROP\_ヘッダー**構造のフィールドの説明と要件が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは1である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これは<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) である必要があります</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは読み取り専用フィールドです。 これには、ドライバーによって返されるフォーカス状態が含まれます。 フォーカス状態の詳細については、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_FOCUSSTATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)"><strong>KSCAMERA_EXTENDEDPROP_FOCUSSTATE</strong></a>のトピックを参照してください。</p></td>
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
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>

---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS
description: KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS プロパティ ID に定義されています。\_拡張\_プロパティ列挙型を使用して、ROI 機能のクエリを実行します。
ms.assetid: 29722CE2-81D3-453E-82C5-98C8E7115448
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_CONFIGCAPS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_CONFIGCAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2731b0512dfc024b99dab0e4a4df51d472938163
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823985"
---
# <a name="ksproperty_cameracontrol_extended_roi_configcaps"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS

**Ksk プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**プロパティ ID で定義されている\_[**CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙を使用して roi をクエリします。機能.

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

ドライバーを使用して ROI 機能のクエリを実行するために、 **Ksk プロパティ\_CAMERACONTROL\_extended\_ROI\_CONFIGCAPS**拡張プロパティコントロールが、標準の[**KSCAMERA\_extendedprop と共にドライバーに送信され @no**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) [**KSCAMERA\_extendedprop\_ROI\_CONFIGCAPSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)構造体の後に続けて1つ以上の[**KSCAMERA\_extendedprop\_roi\_configcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)が続きます。構成. 次の一覧は、2つの ROI 構成キャップを持つデータ構造を示しています。

-   **KSCAMERA\_EXTENDEDPROP\_ヘッダー**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER** (configcapcount = 2)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

次の表には、Ksk プロパティ\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS を使用する場合の**KSCAMERA\_EXTENDEDPROP\_ヘッダー**構造のフィールドの説明と要件が含まれています。拡張された ROI コントロールのプロパティ。

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
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong> + Sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPSHEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPS</strong>) * configcapcount である必要があります。</p></td>
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
<td><p>これは読み取り専用フィールドです。 0にする必要があります。</p></td>
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

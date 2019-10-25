---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL
description: KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL に定義されている ISPCONTROL プロパティ ID\_CAMERACONTROL\_拡張\_プロパティ列挙を使用して、ROI 設定を取得または構成します。必要な処理を適用します。
ms.assetid: 47F6C327-3279-44C2-9B18-50E6EC9C5E77
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_ISPCONTROL ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_ISPCONTROL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b8e79ec63ea37191d1038c9498e18bf0725a140
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823954"
---
# <a name="ksproperty_cameracontrol_extended_roi_ispcontrol"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL

**Ksk プロパティ\_CAMERACONTROL\_拡張\_ROI\_ispcontrol**に定義されている ISPCONTROL プロパティ ID [ **\_CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙を使用して、またはを取得します。ROI 設定を構成し、必要な処理を適用します。

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
<td><p>非同期、キャンセル可能</p></td>
</tr>
</tbody>
</table>

現在の ROI 設定をドライバーから取得するか、ROI 設定を構成して必要な処理 (3As) を適用するには、 **Ksk プロパティ\_CAMERACONTROL\_extended\_ROI\_ISPCONTROL**拡張プロパティコントロールがに送信されます。ドライバーと共に、標準の[**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と共に、 [**KSCAMERA\_EXTENDEDPROP\_ROI\_ispcontrolheader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)構造体の後に[**KSCAMERA\_EXTENDEDPROP は、\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)構造を\_し、次に1つ以上の対応する ISP 固有のコントロールペイロード構造を指定します。 次の一覧は、1つのフォーカス ROI と2つの露出 ROIs を持つデータ構造のレイアウトを示しています。

-   **KSCAMERA\_EXTENDEDPROP\_ヘッダー**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**

-   **KSCAMERA\_EXTENDEDPROP の\_ROI\_ISPCONTROL** (フォーカス)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_焦点**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** (2 つの ROIs で公開)

-   **KSCAMERA\_EXTENDEDPROP\_roi\_露出**(roi 1)

-   **KSCAMERA\_EXTENDEDPROP\_roi\_露出**(roi 2)

次の表には、Ksk プロパティ\_CAMERACONTROL\_拡張\_の ROI\_ISPCONTROL を使用する場合の**KSCAMERA\_EXTENDEDPROP\_ヘッダー**構造のフィールドの説明と要件が含まれています。拡張された ROI コントロールのプロパティ。

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
<td><p>最初の GET 呼び出しの場合 (SET 呼び出しが行われていない場合) は、sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROLHEADER</strong>) である必要があります。 さらに、ドライバーは、ISO コントロールヘッダーペイロードの ControlCount 内で0を返す必要があります。</p>
<p>その他の SET または GET 呼び出しでは、sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<strong>KSCAMERA_EXTENDEDPROP_ ROI_ISPCONTROLHEADER</strong>) + Controlcount * sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROL</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_FOCUS</strong>) * ROICount (FOCUS) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_EXPOSURE</strong>) * ROICount (露出) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_WHITEBALANCE</strong>) * ROICount (ホワイトバランス)。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。 値0は、構成されているすべての ISP コントロールでエラーが検出されなかったことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、ビット単位または<strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCONTROL</strong>と<strong>KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE</strong>である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは読み取り/書き込みフィールドです。これは、SET 呼び出しの<strong>KSCAMERA_EXTENDEDPROP_FLAG_CANCELOPERATION</strong>である可能性があります。 GET 呼び出しの場合は、0である必要があります。</p></td>
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

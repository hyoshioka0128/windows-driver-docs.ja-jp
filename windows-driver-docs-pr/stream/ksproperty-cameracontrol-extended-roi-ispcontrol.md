---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL
description: KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL プロパティ ID、KSPROPERTY で定義されている\_CAMERACONTROL\_拡張\_プロパティ列挙は、取得または ROI 設定を構成し、目的の処理の適用に使用されます。
ms.assetid: 47F6C327-3279-44C2-9B18-50E6EC9C5E77
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_ISPCONTROL ストリーミング メディア デバイス
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
ms.openlocfilehash: 2fd09ba9f2267d5a5e78493eff0b4ae42aa35715
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560728"
---
# <a name="kspropertycameracontrolextendedroiispcontrol"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL

**KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL**で定義されているプロパティ ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)を取得または ROI 設定を構成して、目的の処理を適用する列挙を使用します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope</th>
<th>コントロール</th>
<th>種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>フィルター</p></td>
<td><p>非同期のキャンセル</p></td>
</tr>
</tbody>
</table>

ドライバーから現在の ROI 設定を取得または ROI 設定を構成し、目的の処理 (3As) を適用する、 **KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL**拡張プロパティのコントロールを標準と共にドライバーに送信[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 続く構造体[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)構造が続く、 [ **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)構造体とし、1 つ以上の対応する ISP の特定のコントロールのペイロード構造。 次の一覧は、1 つのフォーカス ROI と Roi の 2 つの公開データ構造体のレイアウトを示しています。

-   **KSCAMERA\_EXTENDEDPROP\_ヘッダー**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** (フォーカス設定)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_フォーカス**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** (2 Roi による公開)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_露出**(ROI 1)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_露出**(ROI 2)

次の表には、説明と要件が含まれています、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー**フィールドを構造体を使用する場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL**拡張、ROI コントロールのプロパティ。

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
<td><p>これは、1、</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これでなければなりません<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0 xffffffff)</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>最初の GET 呼び出し (設定の呼び出しがこれまで行われていない) 場合これあります sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROLHEADER</strong>)。 さらに、ドライバーは、その ISO コントロールのヘッダーのペイロードで ControlCount 内の 0 を返す必要があります。</p>
<p>その他の SET または GET 呼び出し、に対する sizeof があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ ROI_ISPCONTROLHEADER</strong>) + ControlCount * sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROL</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_FOCUS</strong>) * ROICount(focus) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_EXPOSURE</strong>) * ROICount (露出) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_WHITEBALANCE</strong>) * ROICount(whitebalance) します。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。 値 0 は、構成されているすべての ISP コントロールのエラーが検出されなかったことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>ビットごとの OR の必要があります<strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCONTROL</strong>と<strong>KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE</strong>します。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは読み取り/書き込みフィールドがあります<strong>KSCAMERA_EXTENDEDPROP_FLAG_CANCELOPERATION</strong>セット呼び出し。 これは、GET 呼び出しの場合は 0 でなければなりません。</p></td>
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

---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSSTATE
description: KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSSTATE プロパティ ID、KSPROPERTY で定義されている\_CAMERACONTROL\_拡張\_プロパティの列挙を使用して、取得、フォーカス状態のドライバーから。 これは、読み取り専用フィルター レベルのプロパティです。
ms.assetid: 53D54443-59AD-4078-BD13-CB193B89E488
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSSTATE ストリーミング メディア デバイス
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
ms.openlocfilehash: 6ac971f909c30fcf96fbc31f98c407dec98e1d66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355377"
---
# <a name="kspropertycameracontrolextendedfocusstate"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSSTATE

**KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSSTATE**で定義されているプロパティ ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙型を使用して、ドライバーからフォーカス状態を取得します。 これは、読み取り専用フィルター レベルのプロパティです。

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
<td><p>同期 (読み取り専用)</p></td>
</tr>
</tbody>
</table>

[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)フラグ値には、カメラのドライバーによって返されるフォーカスの状態が含まれています。 これは、同期 get 唯一のコントロールです。 使用可能なフォーカス状態の値が提供されている、 [ **KSCAMERA\_EXTENDEDPROP\_FOCUSSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)列挙体。

次の表には、説明と要件が含まれています、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー**フォーカス状態のコントロールを使用する場合は、フィールドを構造体します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
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
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、0 でなければなりません。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、0 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り専用フィールドです。 これには、ドライバーによって返されるフォーカスの状態が含まれています。 フォーカス状態の詳細については、次を参照してください。、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_FOCUSSTATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_extendedprop_focusstate)"> <strong>KSCAMERA_EXTENDEDPROP_FOCUSSTATE</strong> </a>トピック。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>必要条件

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

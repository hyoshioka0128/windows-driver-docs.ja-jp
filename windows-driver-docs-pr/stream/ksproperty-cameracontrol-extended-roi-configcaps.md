---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS
description: KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS プロパティ ID、KSPROPERTY で定義されている\_CAMERACONTROL\_拡張\_プロパティ列挙は、ROI 機能の照会に使用されます。
ms.assetid: 29722CE2-81D3-453E-82C5-98C8E7115448
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_CONFIGCAPS ストリーミング メディア デバイス
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
ms.openlocfilehash: 643aad2d1371acb45e71dc5310543a78a488ca55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351830"
---
# <a name="kspropertycameracontrolextendedroiconfigcaps"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS

**KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**で定義されているプロパティ ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/dn917962)列挙体は、ROI 機能のクエリに使用されます。

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

クエリのドライバーと ROI の機能を**KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**と共にドライバーに拡張プロパティのコントロールが送信される、標準[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造が続く、 [ **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)構造体は、1 つまたは複数続く[ **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)構造体。 次の一覧は、2 つの ROI 設定キャップを持つデータ構造を示しています。

-   **KSCAMERA\_EXTENDEDPROP\_ヘッダー**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER** (ConfigCapCount = 2)

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**

次の表には、説明と要件が含まれています、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー**フィールドを構造体を使用する場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_ROI\_CONFIGCAPS**拡張、ROI コントロールのプロパティ。

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
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong> + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPSHEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPS</strong>) * ConfigCapCount します。</p></td>
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
<td><p>これは、読み取り専用フィールドです。 これは、0 でなければなりません。</p></td>
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

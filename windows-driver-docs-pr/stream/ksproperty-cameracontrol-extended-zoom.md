---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ZOOM
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ZOOM は、デジタルズームの制御に使用されます。
ms.assetid: 93CFCBFC-69B3-4241-913F-94615599BE8E
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 195a54a2e13b5757479d3b3de034642fc7fc8540
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827432"
---
# <a name="ksproperty_cameracontrol_extended_zoom"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ZOOM

**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_ZOOM**は、デジタルズームの制御に使用されます。 このプロパティは、 [**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙型に定義されており、ズーム比率を取得および設定し、ドライバーからズーム範囲を取得するために使用されます。 Windows 10 では、このコントロールはスムーズズームもサポートするように拡張されています。

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
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグは、 **KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。** スムーズズームと直接ズームを制御するフラグフィールド。 既定値はドライバーによって定義されます。

```cpp
#define KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT  0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH   0x0000000000000002
```

ドライバーがこのコントロールをサポートしている場合は、 **KSCAMERA\_EXTENDEDPROP\_ZOOM\_既定値**をサポートする必要があります。

ドライバーでデジタルズームがサポートされていない場合、ドライバーはこのコントロールを実装しないでください。

次の表では、フラグ機能について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT</strong></p></td>
<td><p>これは必須の機能です。 指定すると、ドライバーは、直接ズームまたはスムーズズームを適用する必要があるかどうかを決定し、それに応じて、VideoProc. Value. ul に指定されたターゲットのズームファクターにズームします。 このフラグは、直接および SMOOTH フラグと同時に指定することはできません。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT</strong></p></td>
<td><p>これは必須の機能です。 指定した場合、ドライバーは、可能な限り迅速に VideoProc. Value. ul に指定された目標のズーム率にズームします。 このフラグは、AUTO および SMOOTH フラグと同時に指定することはできません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH</strong></p></td>
<td><p>この機能は省略可能です。 この値を指定すると、ドライバーは、VideoProc で指定された目標のズーム率にズームします。 フレームの数は、指定したズーム率になるまで、ドライバーによって決まります。 このフラグは、AUTO および DIRECT フラグと同時に指定することはできません。</p></td>
</tr>
</tbody>
</table>

**GET**呼び出しごとに、ドライバーは現在の構成またはセットアップに基づいて許可されている現在のズーム範囲を報告する必要があります。

次の表は、 **Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_ZOOM**プロパティを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件を示しています。

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
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>は、前に定義したサポートされているフラグのビットごとの OR である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上で定義したサポートされているフラグのいずれかを指定できます。</p></td>
</tr>
</tbody>
</table>

次の表には、 **Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_ZOOM**プロパティの**KSCAMERA\_EXTENDEDPROP\_videoの設定**構造のフィールドの説明と要件が含まれています。

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
<td><p>[モード]</p></td>
<td><p>これは使用されておらず、0である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>Min/Max/Step には、Q16 形式でカメラドライバーでサポートされているズーム比率の最小/最大/増分が含まれます。 ドライバーは、 <strong>GET</strong>操作のためにこれらの値を返す必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p><strong>設定</strong>操作の場合、videoproc は、Min/Max/Step パラメーターで表される範囲内のズーム比を指定する必要があります。 <strong>GET</strong>操作の場合、ドライバーは現在のズーム比率を返す必要があります。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>これは使用されません。 これは、ドライバーによって無視される必要があります。</p></td>
</tr>
</tbody>
</table>

このプロパティコントロールは同期であり、キャンセルできません。

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

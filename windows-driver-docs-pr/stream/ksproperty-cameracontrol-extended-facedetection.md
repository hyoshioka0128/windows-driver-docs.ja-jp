---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEDETECTION
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEDETECTION は、顔検出をオンまたはオフにするために使用されるプロパティ ID です。
ms.assetid: F503939D-D6EF-47BD-855B-4404E1AAA15C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEDETECTION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEDETECTION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2d25c6cd9ac4798ed38b14c49d146286b6cc577e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843236"
---
# <a name="ksproperty_cameracontrol_extended_facedetection"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEDETECTION

KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEDETECTION は、顔検出をオンまたはオフにするために使用されるプロパティ ID です。

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

次のフラグは、KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。ドライバーの顔検出を制御するフラグフィールド。 既定では、ドライバーは FACEDETECTION\_オフになっている必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW         0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO           0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO           0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK           0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE           0x0000000000000010
```

ドライバーがこのコントロールをサポートしている場合は、FACEDETECTION\_OFF と FACEDETECTION\_PREVIEW、FACEDETECTION\_VIDEO、FACEDETECTION\_のいずれかの写真をサポートする必要があります。 顔検出が有効になっている場合、ドライバーはさらに優位面分析を行い、優位面を3A に直接フィードする必要があります。

ドライバーが顔検出をサポートしていない場合、ドライバーはこのコントロールを実装しません。

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
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF</p></td>
<td><p>これは必須の機能です。 指定すると、ドライバーで顔検出が無効になります。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW</p></td>
<td><p>これはオプションの機能です。 指定すると、ドライバーで顔検出が有効になり、ドライバーは顔情報と、サポートされている場合に関連付けられているタイムスタンプを、プレビューピンを介したメタデータとして提供する必要があります。 このフラグは、OFF フラグと同時に指定することはできません。また、他のフラグと共に使用することもできます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO</p></td>
<td><p>この機能は省略可能です。 指定すると、ドライバーで顔検出が有効になり、このような機能をサポートするドライバーは、ビデオ pin を介してメタデータとして、顔情報と、サポートされている場合に関連付けられているタイムスタンプを提供する必要があります。 このフラグは、OFF フラグと同時に指定することはできません。また、他のフラグと共に使用することもできます。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO</p></td>
<td><p>この機能は省略可能です。 指定すると、ドライバーで顔検出が有効になります。このような機能をサポートするドライバーは、顔情報と、サポートされている場合に関連付けられているタイムスタンプを、フォト pin を介したメタデータとして提供する必要があります。 このフラグは、OFF フラグと同時に指定することはできません。また、他のフラグと共に使用することもできます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK</p></td>
<td><p>この機能は省略可能です。 このフラグは、PREVIEW、VIDEO、施し PHOTO フラグが指定されている場合にのみ指定できます。 指定する場合、このような機能をサポートするドライバーは、さらに、対応する pin を通じて点滅情報をメタデータとして提供する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE</p></td>
<td><p>この機能は省略可能です。 このフラグは、PREVIEW、VIDEO、施し PHOTO フラグが指定されている場合にのみ指定できます。 指定した場合、このような機能をサポートするドライバーは、さらに、対応する pin を使用してメタデータとして気に入った情報を提供する必要があります。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> MFT0 は、FACEROITIMESTAMPS\_\_メタデータをキャプチャし、メインフレームとしてのタイムスタンプ\_\_メタデータ\_、点滅や機能の情報を MF としてキャプチャ\_、face 情報を MF として追加する必要があり\_サンプルで\_メタデータ\_FACEROICHARACTERIZATIONS をキャプチャします。
> プレビュー、ビデオ、および写真機能は省略可能です。 ただし、このコントロールがサポートされている場合は、プレビュー、ビデオ、および写真機能の少なくとも1つをサポートする必要があります。

次の表に、コントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体のフィールドの説明と要件を示します。

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
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>は、上で定義したように、サポートされている KSCAMERA_EXTENDEDPROP_FACEDETECTION_ * フラグのビットごとの OR である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これは、上記で定義された KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF/PREVIEW/VIDEO/PHOTO フラグ、または KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK または KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE のいずれかの組み合わせを使用して、ビットごとに、あるいはその両方を行うことができます。KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW/VIDEO/PHOTO フラグ。</p></td>
</tr>
</tbody>
</table>

次の表には、KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FACEDETECTION プロパティの KSCAMERA\_EXTENDEDPROP\_VIDEOの設定構造フィールドの説明と要件が含まれています。 この構造体は、Ksmedia. h で定義されています。

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
<td><p>未使用. 0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>Min/Max/Step には、カメラドライバーが検出または検索できる顔の数の最小値/最大値 (&gt;分単位) が含まれます。この数は、1以上である必要があります。1にする必要があります。 ドライバーは、GET 操作のためにこれらを返す必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p><strong>FACEDETECTION_PREVIEW</strong>、FACEDETECTION_VIDEO、または<strong>FACEDETECTION_PHOTO</strong>が<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>の Flags フィールドに指定されている場合は、の最大数も指定<strong>する必要があります。</strong>ドライバーが検索する顔。</p>
<p>FACEDETECTION_OFF を指定した場合、設定操作では、VideoProc フィールドは無視されます。</p>
<p>GET 操作の場合、ドライバーは、ドライバーが現在検索している顔の最大数を返す必要があります。 顔検出がオフの場合、0が返されます。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>これは使用されません。 これは、ドライバーによって無視される必要があります。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>注釈

顔検出が有効になっている場合は、必要に応じて3A の処理を支援するために、顔領域 (ROIs) がドライバーによって直接使用されることがあります。 指定されたユーザーが ROIs を使用して構成されている場合\_CAMERACONTROL\_拡張\_ROI\_ISPCONTROL 同時に、ユーザーが指定した ROIs は、検出された顔よりも優先されます。 ユーザーが ROIs を指定した場合は、検出された face ROIs が有効になります。

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

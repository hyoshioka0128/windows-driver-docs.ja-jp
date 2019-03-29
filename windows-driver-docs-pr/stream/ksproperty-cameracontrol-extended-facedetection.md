---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FACEDETECTION
description: KSPROPERTY\_CAMERACONTROL\_拡張\_FACEDETECTION がオンとオフは、顔検出に使用するプロパティ ID。
ms.assetid: F503939D-D6EF-47BD-855B-4404E1AAA15C
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEDETECTION ストリーミング メディア デバイス
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
ms.openlocfilehash: d0b83feeae4883469109c254cfcee06ffc8cde65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580875"
---
# <a name="kspropertycameracontrolextendedfacedetection"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FACEDETECTION


KSPROPERTY\_CAMERACONTROL\_拡張\_FACEDETECTION がオンとオフは、顔検出に使用するプロパティ ID。

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
<th>型</th>
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

 

次のフラグは、KSCAMERA に配置できる\_EXTENDEDPROP\_ヘッダー。フィールドは、ドライバー内の顔検出を制御するフラグを設定します。 既定では、ドライバーが FACEDETECTION\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW         0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO           0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO           0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK           0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE           0x0000000000000010
```

FACEDETECTION をサポートする必要があります、ドライバーは、このコントロールをサポートする場合\_OFF および FACEDETECTION のいずれかの\_プレビュー、FACEDETECTION\_ビデオ、または FACEDETECTION\_写真。 ドライバーは dominate 顔の分析を実行し、顔検出を有効にするに 3A に dominate 顔を直接フィードさらにする必要があります。

ドライバーが顔検出をサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

次の表では、フラグの機能について説明します。

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
<td><p>これは、必須の機能です。 指定した場合、ドライバーでは、顔の検出は無効になっています。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW</p></td>
<td><p>これは、省略可能な機能です。 ドライバーの顔の検出が有効になっている、指定した場合と、ドライバーは、顔の情報とプレビューの暗証番号 (pin) をメタデータとして、サポートされている場合に関連付けられたタイムスタンプを提供する必要があります。 このフラグは OFF フラグで相互に排他的では、他のフラグで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_VIDEO</p></td>
<td><p>この機能は省略可能です。 ドライバーの顔の検出が有効になっている、指定した場合と、このような機能をサポートするドライバーは、顔の情報とビデオ ピンをメタデータとして、サポートされている場合に関連付けられたタイムスタンプを提供する必要があります。 このフラグは OFF フラグで相互に排他的では、他のフラグで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_PHOTO</p></td>
<td><p>この機能は省略可能です。 ドライバーの顔の検出が有効になっている指定した場合、および顔についてでは、およびタイムスタンプは写真の暗証番号 (pin) をメタデータとして、サポートされている場合、このような機能をサポートするドライバーが提供する必要があります。 このフラグは OFF フラグで相互に排他的では、他のフラグで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK</p></td>
<td><p>この機能は省略可能です。 このフラグは、プレビュー、ビデオや写真フラグが指定した場合にのみ指定できます。 指定した場合、このような機能をサポートしているドライバー、対応するピンをメタデータとして点滅情報を提供する必要がありますはさらにします。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE</p></td>
<td><p>この機能は省略可能です。 このフラグは、プレビュー、ビデオや写真フラグが指定した場合にのみ指定できます。 指定した場合、このような機能をサポートしているドライバー、対応するピンをメタデータとして気に入った機能の情報を提供する必要がありますはさらにします。</p></td>
</tr>
</tbody>
</table>

 

**注**  MFT0 ものと、MF と顔の情報をアタッチしてさらに\_キャプチャ\_メタデータ\_、MF としてタイムスタンプ、FACEROIS\_キャプチャ\_メタデータ\_FACEROITIMESTAMPS、や点滅や気に入った機能の情報を MF として\_キャプチャ\_メタデータ\_FACEROICHARACTERIZATIONS サンプルにします。

 

**注**  プレビュー、ビデオ、および写真の機能は省略可能です。 ただし、このコントロールがサポートされている場合、この機能のプレビュー、ビデオ、および写真を少なくとも 1 つをサポートする必要があります。

 

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)コントロールを使用する場合は、フィールドを構造体します。

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
<td><p>これは、1 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 xffffffff) 必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>これは、sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>上記に定義されているサポートされている KSCAMERA_EXTENDEDPROP_FACEDETECTION_ * フラグのビットごとの OR をする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 任意の組み合わせで、上記で定義された KSCAMERA_EXTENDEDPROP_FACEDETECTION_OFF/プレビュー/ビデオ/写真フラグまたは少し賢明 KSCAMERA_EXTENDEDPROP_FACEDETECTION_BLINK の OR のビット単位の OR や KSCAMERA_EXTENDEDPROP_FACEDETECTION_SMILE は、このKSCAMERA_EXTENDEDPROP_FACEDETECTION_PREVIEW/ビデオ/写真フラグ。</p></td>
</tr>
</tbody>
</table>

 

次の表には、説明と、KSCAMERA の要件が含まれています\_EXTENDEDPROP\_VIDEOPROCSETTING 構造のフィールド、KSPROPERTY\_CAMERACONTROL\_拡張\_FACEDETECTION プロパティです。 この構造体は、Ksmedia.h で定義されます。

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
<td><p>モード</p></td>
<td><p>使用されていません。 0 を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>最小/最大/ステップには、最小/最大/増分カメラのドライバーが検出または最小値がある必要があります内で検索できる顔の数が含まれています。 &gt;= 1 の手順が 1 にする必要があります。 ドライバーは、これらの GET 操作で返す必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>場合<strong>FACEDETECTION_PREVIEW</strong>、 <strong>FACEDETECTION_VIDEO</strong>または<strong>FACEDETECTION_PHOTO</strong>の Flags フィールドで指定されて、 <strong>KSCAMERA_EXTENDEDPROP_ヘッダー</strong>、 <strong>VideoProc.Value.ul</strong>ドライバーを検索する必要がある顔の最大数を指定する必要があります。</p>
<p>設定操作で、FACEDETECTION_OFF が指定されている場合、VideoProc フィールドは無視されます。</p>
<p>GET 操作では、ドライバーはドライバーが現在探している顔の最大数を返す必要があります。 顔検出が OFF の場合は 0 が返されます。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>これは使用されません。 これは、ドライバーによって無視する必要があります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a>コメント

顔検出をオンにすると、必要に応じて、3 a の処理を支援するために、ドライバーによって直接興味 (Roi) の顔の領域を使用できます。 Roi が KSPROPERTY 経由で構成されているすべてのユーザーが指定されている場合\_CAMERACONTROL\_拡張\_ROI\_Roi は優先顔検出 Roi ISPCONTROL と同時に、ユーザーを指定します。 Roi をオフに指定されたユーザー、顔検出 Roi が有効になります。

<a name="requirements"></a>必要条件
------------

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

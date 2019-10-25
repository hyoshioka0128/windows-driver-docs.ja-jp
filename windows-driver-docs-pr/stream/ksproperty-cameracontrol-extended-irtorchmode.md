---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_IRTORCHMODE
description: この拡張プロパティコントロールは、IR カメラの赤外線 torch の電源レベルとデューティサイクルを制御するために、クライアントによって使用されます。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/03/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.custom: 19H1
ms.openlocfilehash: f8833e4b946294c4c1a9a987d4e2d0c35ee66414
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843225"
---
# <a name="ksproperty_cameracontrol_extended_irtorchmode"></a>KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE

この拡張プロパティコントロールは、IR カメラの赤外線 torch の電源レベルとデューティサイクルを制御するために、クライアントによって使用されます。 これは、標準の[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と共にドライバーに送信され、その後に[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体が続きます。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| [購入] | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
| --- | --- | --- | --- | --- |
| [はい] | [はい] | フィルター | [KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) | [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)|

## <a name="remarks"></a>注釈

プロパティ要求には、 [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体が含まれています。

プロパティデータの合計サイズは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) です。 [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

KSCAMERA_EXTENDEDPROP_HEADER に配置できるフラグを次に示し**ます。Flags**と**KSCAMERA_EXTENDEDPROP_HEADER。機能**フィールド。  これらは、IR torch の動作モードを定義します。

| Torch モード                                                       | 説明                        |
|------------------------------------------------------------------|------------------------------------|
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF                            | [オフ]                                |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON                      | 常にオン                          |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATING_FRAME_ILLUMINATION | 他のすべてのフレームに対してオン           |

KSCAMERA_EXTENDEDPROP_IRTORCHMODE は常に同期コントロールです。  カメラがストリーミングされていない場合、コントロールには動作が定義されていません。

GET 要求の場合、ドライバーは次のフィールドを設定します。

- **KSCAMERA_EXTENDEDPROP_HEADER。** カメラでサポートされている動作モードを表す上記の KSCAMERA_EXTENDEDPROP_IRTORCHMODE_*XXX*フラグのビットマスクを持つ機能。
- **KSCAMERA_EXTENDEDPROP_HEADER。** 現在の動作モードを示すために、上記の KSCAMERA_EXTENDEDPROP_IRTORCHMODE_*XXX*フラグのいずれかにフラグを指定します。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。モード**を0にします。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。** 使用可能な最小電源レベルまでの最小値。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。** 最大電力レベルの最大値。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。** パワーレベル間の最小増分にステップアウトします。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。** 現在の電源レベルに対して VideoProc を行います。 この値は、既定では、face authentication コントロールで使用されるのと同じ電源レベルに設定する必要があります。

設定要求の場合、ドライバーは次のフィールドを使用します。

- **KSCAMERA_EXTENDEDPROP_HEADER。** 動作モードを設定するフラグ。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING。** パワーレベルを設定するには、VideoProc を行います。  この値は、KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF には影響しません。

次の表に、メタデータコントロールを使用する場合の[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) structure フィールドの説明と要件を示します。

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
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
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof ([KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>同期コントロールの場合、この値は無視されます。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p><strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>、 <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong> 、または<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>の任意の組み合わせを指定できます。  
このフィールドは、少なくとも1つの機能を報告する必要があります。  フィールドは、 <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>または<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>のいずれかまたは両方を報告する必要があります。 値<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>は省略可能です。
</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>機能に報告されたフラグのいずれかである必要があります。  既定値は<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>または<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>のいずれかである必要があります。</p></td>
</tr>
</tbody>
</table>

次の表は、IR torch mode コントロールを使用する場合の[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) structure フィールドの説明と要件を示しています。

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
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
<td><p>未使用.  0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>Min/Max/Step には、IR 電源設定の最小/最大/増分が含まれます。  ドライバーは、GET 操作のためにこれらを返す必要があります。  (Max – Min) は、手順によって均等に割り切れる必要があります。  ステップをゼロ (0) にすることはできません。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>設定操作の場合、VideoProc は、Min/Max/Step パラメーターで記述された範囲内のパワーレベルを指定する必要があります。  GET 操作の場合、ドライバーは現在の電源レベルを返す必要があります。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>未使用.  ドライバーによって無視される必要があります。</p></td>
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

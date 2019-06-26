---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_IRTORCHMODE
description: この拡張プロパティのコントロールは、IR カメラの赤外線 torch の電源レベルとデューティ サイクルを制御するクライアントによって使用されます。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE ストリーミング メディア デバイス
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
ms.openlocfilehash: d9aeba21b57ca4c895253684ebf95a97ece48964
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355382"
---
# <a name="kspropertycameracontrolextendedirtorchmode"></a>KSPROPERTY_CAMERACONTROL_EXTENDED_IRTORCHMODE

この拡張プロパティのコントロールは、IR カメラの赤外線 torch の電源レベルとデューティ サイクルを制御するクライアントによって使用されます。 標準と共にドライバーに送信される[KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造が続く、 [KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
| --- | --- | --- | --- | --- |
| 〇 | 〇 | フィルター | [KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) | [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)|

## <a name="remarks"></a>注釈

プロパティの要求に含まれる、 [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体。

プロパティの合計データ サイズとは、sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING) です。 **サイズ**のメンバー [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

配置できるフラグを次に、 **KSCAMERA_EXTENDEDPROP_HEADER します。フラグ**と**KSCAMERA_EXTENDEDPROP_HEADER します。機能**フィールド。  IR torch の動作モードを定義します。

| Torch モード                                                       | 説明                        |
|------------------------------------------------------------------|------------------------------------|
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF                            | オフ                                |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON                      | 常にオン                          |
| KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATING_FRAME_ILLUMINATION | 上の他のすべてのフレーム           |

KSCAMERA_EXTENDEDPROP_IRTORCHMODE は、常に同期コントロールです。  コントロールには定義された動作がない、カメラはストリーミングされません。

GET 要求では、ドライバーは、次のフィールドを設定します。

- **KSCAMERA_EXTENDEDPROP_HEADER します。機能**上記 KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ のビットマスクを*XXX*カメラでサポートされている動作モードを表すフラグ。
- **KSCAMERA_EXTENDEDPROP_HEADER します。フラグ**KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ を上記のいずれかに*XXX*を現在の操作モードを示すフラグ。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING します。モード**を 0 にします。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING します。Min**使用可能な最低限の電力レベルにします。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING します。最大**に利用できる最大電力レベル。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING します。手順**電力レベル間の最小のインクリメントにします。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING します。VideoProc.ul**現在の電力レベル。 この値は、通常顔認証の制御で使用される同じ電源のレベルを既定する必要があります。

セットの要求では、ドライバーは、次のフィールドを使用します。

- **KSCAMERA_EXTENDEDPROP_HEADER します。フラグ**動作モードを設定します。
- **KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING します。VideoProc.ul**電源レベルを設定します。  この値には、KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF に影響はありません。

次の表には、説明と要件が含まれています、 [KSCAMERA_EXTENDEDPROP_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)メタデータ コントロールを使用する場合は、フィールドを構造体します。

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
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
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 XFFFFFFFF) です。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof 必要があります ([KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting))、</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>コントロールの同期では、この値は無視されます。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>任意の組み合わせがあります<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>、 <strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>または<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME。_ILLUMINATION</strong>します。  
このフィールドは、少なくとも 1 つの機能をレポートする必要があります。  フィールドは、いずれかを報告する必要があります<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>または<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>またはその両方です。 値<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_OFF</strong>は省略可能です。
</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>報告する必要があるフラグのいずれかで機能します。  既定値する必要がありますか<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALWAYS_ON</strong>または<strong>KSCAMERA_EXTENDEDPROP_IRTORCHMODE_ALTERNATIVE_FRAME_ILLUMINATION</strong>します。</p></td>
</tr>
</tbody>
</table>

次の表には、説明と要件が含まれています、 [KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) IR を使用する場合、構造体のフィールド torch モード制御します。

<table>
<colgroup>
<col width="30%" />
<col width="70%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>未使用。  0 を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>最小/最大/ステップには、最小/最大/の増分 IR の電源設定が含まれています。  ドライバーは、これらの GET 操作で返す必要があります。  (最大値-最小値) の手順で割り切れる必要があります。  手順は、ゼロ (0) できない可能性があります。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p>設定操作で、VideoProc.Value.ul は最小/最大/ステップ パラメーターによって示された範囲内で電源レベルを指定する必要があります。  GET 操作では、ドライバーは、現在の電源レベルを返す必要があります。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>未使用。  ドライバーを無視する必要があります。</p></td>
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

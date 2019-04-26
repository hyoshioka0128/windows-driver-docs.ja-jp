---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_VFR
description: KSPROPERTY\_CAMERACONTROL\_拡張\_VFR は可変フレーム レートが、ドライバーで必要なかどうかを指定するために使用するプロパティ ID。
ms.assetid: 9B528421-B5AA-4092-9F7B-71A18732ABA8
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b4ea75cb9f6f30a1202724ca249790bea0594d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341880"
---
# <a name="kspropertycameracontrolextendedvfr"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_VFR

KSPROPERTY\_CAMERACONTROL\_拡張\_VFR は可変フレーム レートが、ドライバーで必要なかどうかを指定するために使用するプロパティ ID。 これは、暗証番号 (pin) レベルの制御のビデオ ピン留めするだけです。 プレビューと写真は、フレーム レートの可変性は、ドライバーの自由ですし、クライアントによって制御することはありません。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグを配置することができます、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー。フラグ**フィールドで、上、または変数のフレーム レートのビデオをオフにするために使用します。 既定では、ドライバーです。

```cpp
#define KSCAMERA_EXTENDEDPROP_VFR_OFF   0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_VFR_ON    0x0000000000000001
```
場合に VFR 設定\_ドライバー、ビデオの暗証番号 (pin) の固定フレーム レートを配信ものとします。

場合設定 VFR\_フレーム レートがドライバーによって自動的に決定し、キャプチャ条件とビデオの暗証番号 (pin) のシナリオによって異なることができます。 ときに VFR\_ON に設定されている、許可される最大フレーム レートは、固定のフレーム レートのビデオ記録用に選択されたメディアの種類に埋め込まれたによって決定します。

場合は、ドライバーは、ビデオの変数のフレーム レートをサポートしていない、ドライバーは、このコントロールを実装しないでくださいし、固定フレーム レートを暗黙的に指定されます。

このコントロールは、ビデオ記録 VFR 設定の即時の切り替えをサポートしていないドライバーの中には影響を与えません。 ドライバーは、アクティブなビデオの場合に記録中に受信したコントロールを無視ものとします。

これは、同期のコントロールとキャンセルできません。 このコントロールに対して定義されている機能はありません。

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
<td><p>ビデオの暗証番号 (pin) に関連付けられた暗証番号 (pin) の ID があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE) 必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、0 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義されたフラグのいずれかにできます。</p></td>
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

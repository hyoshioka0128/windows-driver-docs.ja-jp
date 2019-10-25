---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VFR
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VFR は、ドライバーで可変フレームレートが必要かどうかを指定するために使用されるプロパティ ID です。
ms.assetid: 9B528421-B5AA-4092-9F7B-71A18732ABA8
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR ストリーミングメディアデバイス
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
ms.openlocfilehash: 0b13e59c269bd345f045af64461cb8b768246e9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823934"
---
# <a name="ksproperty_cameracontrol_extended_vfr"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VFR

KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VFR は、ドライバーで可変フレームレートが必要かどうかを指定するために使用されるプロパティ ID です。 これは、ビデオ pin の pin レベルコントロールです。 プレビューと写真の場合、フレームレートの変動は完全にドライバーによって異なり、クライアントが制御することはできません。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグは、 **KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。Flags**フィールド。ビデオの可変フレームレートをオンまたはオフにするために使用されます。 既定では、ドライバーによって設定されます。

```cpp
#define KSCAMERA_EXTENDEDPROP_VFR_OFF   0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_VFR_ON    0x0000000000000001
```
VFR\_オフに設定した場合、ドライバーはビデオ pin の固定フレームレートを提供します。

VFR\_に設定した場合、フレームレートはドライバーによって自動的に決定され、ビデオ pin のキャプチャ条件とシナリオに応じて変化することがあります。 [VFR\_オン] が設定されている場合、許可される最大フレームレートは、ビデオ記録用に選択したメディアの種類に埋め込まれている固定フレームレートによってさらに決まります。

ドライバーがビデオの可変フレームレートをサポートしていない場合、ドライバーはこのコントロールを実装しないようにし、可変フレームレートを暗黙的に指定します。

このコントロールは、VFR の設定を実行しているときにサポートされていないドライバーのビデオ記録中には効果がありません。 この場合、アクティブなビデオ記録中に受信したコントロールはドライバーによって無視されます。

これは同期コントロールであり、キャンセルできません。 このコントロールに定義されている機能はありません。

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
<td><p>これは、ビデオ pin に関連付けられている Pin ID である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上で定義したフラグのいずれかを指定できます。</p></td>
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

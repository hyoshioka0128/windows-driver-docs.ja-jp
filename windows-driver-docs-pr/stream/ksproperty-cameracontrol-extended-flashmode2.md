---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE プロパティは、assistant flash をサポートするように拡張されています。
ms.assetid: 413B3A02-498A-4C5A-8940-9A0D10D6CE81
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: bb87cdccb34b4ea3267c154993754f82a6a1fd1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843230"
---
# <a name="ksproperty_cameracontrol_extended_flashmode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE

**Ksk プロパティ\_CAMERACONTROL\_extended\_FLASHMODE**プロパティは、assistant flash をサポートするように拡張されています。

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

機能フラグは、次のように定義されています。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_ON               0x0000000000000080
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_AUTO             0x0000000000000100
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_OFF              0x0000000000000000
```

**KSCAMERA\_EXTENDEDPROP\_FLASH\_ASSISTANT\_ON**

このフラグは、AF アシスタントライトがオンになっていることを示します。

**KSCAMERA\_EXTENDEDPROP\_FLASH\_ASSISTANT\_AUTO**

このフラグは、 **ASSISTANT\_ON**フラグに似ています。 常に AF アシスタントライトをオンにするのではなく、カメラドライバーは、現在の照明条件に基づいて AF アシスタントのライトをオンにするかどうかを決定します。

**KSCAMERA\_EXTENDEDPROP\_FLASH\_ASSISTANT\_オフ**

このフラグは、AF アシスタントライトがオフであることを示します。

**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE**プロパティを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造フィールドの説明は、Windows 8.1 DDI と同じです。

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

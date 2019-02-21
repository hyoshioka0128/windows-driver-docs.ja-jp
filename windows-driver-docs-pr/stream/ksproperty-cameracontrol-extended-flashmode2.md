---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE
description: KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE プロパティがアシスタント flash をサポートするために拡張します。
ms.assetid: 413B3A02-498A-4C5A-8940-9A0D10D6CE81
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE ストリーミング メディア デバイス
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
ms.openlocfilehash: f8806bf3588b8564c604d97cd6ad22c4d9832c51
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539349"
---
# <a name="kspropertycameracontrolextendedflashmode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE

**KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE**アシスタント flash をサポートするためにプロパティが拡張されます。

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
<td><p>同期</p></td>
</tr>
</tbody>
</table>

機能フラグの定義は次のとおりです。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_ON               0x0000000000000080
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_AUTO             0x0000000000000100
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_OFF              0x0000000000000000
```

**KSCAMERA\_EXTENDEDPROP\_FLASH\_アシスタント\_ON**

このフラグは、AF アシスタントの光が有効であることを示します。

**KSCAMERA\_EXTENDEDPROP\_FLASH\_アシスタント\_自動**

このフラグと似ています、**アシスタント\_ON**フラグ。 常に、AF アシスタントのライトの有効化ではなくかどうか AF アシスタントのライトをオンに現在の照明条件に基づいて、カメラのドライバーを決定します。

**KSCAMERA\_EXTENDEDPROP\_FLASH\_アシスタント\_OFF**

このフラグは、AF アシスタントのライトがオフであることを示します。

説明、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)フィールドを構造体を使用する場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE**プロパティは、Windows 8.1 DDI と同じです。

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

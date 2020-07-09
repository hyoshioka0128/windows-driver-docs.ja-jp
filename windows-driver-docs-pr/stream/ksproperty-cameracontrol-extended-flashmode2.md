---
title: KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE (assistant flash)
description: KSK プロパティ \_ CAMERACONTROL \_ extended \_ FLASHMODE プロパティは、assistant flash をサポートするように拡張されています。
ms.assetid: 413B3A02-498A-4C5A-8940-9A0D10D6CE81
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE (assistant flash)
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 07/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8899984231eb045492411750238dd7f300c66f47
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128879"
---
# <a name="ksproperty_cameracontrol_extended_flashmode"></a>KSK プロパティ \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE

**Ksk プロパティ \_ CAMERACONTROL \_ extended \_ FLASHMODE**プロパティは、assistant flash をサポートするように拡張されています。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| スコープ | Control | Type |
|--|--|--|
| Version 1 | フィルター | 同期 |

機能フラグは、次のように定義されています。

```cpp
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_ON               0x0000000000000080
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_AUTO             0x0000000000000100
#define KSCAMERA_EXTENDEDPROP_FLASH_ASSISTANT_OFF              0x0000000000000000
```

**KSCAMERA \_ EXTENDEDPROP \_ \_ の FLASH ASSISTANT \_**

このフラグは、AF アシスタントライトがオンになっていることを示します。

**KSCAMERA \_ EXTENDEDPROP \_ FLASH \_ ASSISTANT \_ AUTO**

このフラグは、 **ASSISTANT \_ ON**フラグに似ています。 常に AF アシスタントライトをオンにするのではなく、カメラドライバーは、現在の照明条件に基づいて AF アシスタントのライトをオンにするかどうかを決定します。

**KSCAMERA \_ EXTENDEDPROP \_ フラッシュ \_ アシスタント \_ オフ**

このフラグは、AF アシスタントライトがオフであることを示します。

**Ksk プロパティ \_ CAMERACONTROL \_ EXTENDED \_ FLASHMODE**プロパティを使用する場合の[**KSCAMERA \_ extendedprop \_ ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造フィールドの説明は、Windows 8.1 DDI と同じです。

## <a name="requirements"></a>必要条件

**ヘッダー:** Ksmedia .h (Ksk を含む)

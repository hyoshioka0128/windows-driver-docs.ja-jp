---
title: KSK PROPERTYSETID \_ NetworkCameraControl
description: ネットワークカメラの propertyset ID を定義します。
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 71c91210844cd0bc54b1219f0264c9a3b8d24cb3
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060853"
---
# <a name="kspropertysetid_networkcameracontrol"></a>KSK PROPERTYSETID \_ NetworkCameraControl

*Ksmedia .h*ヘッダーファイルは、次のように**ksk propertysetid \_ NetworkCameraControl**プロパティセット ID を定義します。

```cpp
#define STATIC_KSPROPERTYSETID_NetworkCameraControl \
    0xe780f09, 0x5745, 0x4e3a,  0xbc, 0x9f, 0xf2, 0x26, 0xea, 0x43, 0xa6, 0xec
DEFINE_GUIDSTRUCT("0E780F09-5745-4E3A-BC9F-F226EA43A6EC", KSPROPERTYSETID_NetworkCameraControl);
#define KSPROPERTYSETID_NetworkCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_NetworkCameraControl)
```

**Ksk Propertysetid \_ NetworkCameraControl**プロパティセットには、次のプロパティが含まれています。

[**KSPROPERTY_NETWORKCAMERACONTROL_NTP**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty_networkcameracontrol_ntp)

[**KSPROPERTY_NETWORKCAMERACONTROL_URI**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty_networkcameracontrol_uri)

これらのプロパティ名は、 [KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_property)列挙体で定義されます。

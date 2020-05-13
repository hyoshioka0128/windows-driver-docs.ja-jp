---
title: KSK PROPERTYSETID \_ NetworkCameraControl
description: ネットワークカメラのプロパティセット ID を定義します。
ms.date: 04/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: ebe84f7087c67a5f9b6c67e93c9a1ea77ae86da2
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270433"
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

[**KSPROPERTY_NETWORKCAMERACONTROL_NTP**](https://docs.microsoft.com/windows-hardware/drivers/stream/)

[**KSPROPERTY_NETWORKCAMERACONTROL_URI**](https://docs.microsoft.com/windows-hardware/drivers/stream/)

これらのプロパティ名は、 [KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/stream/ne-ksmedia-ksproperty_networkcameracontrol_property)列挙体で定義されます。

---
title: 使用できるインターフェイスと関連する API
description: デバイスごとに 3 つの GPIO インターフェイス 1 つがあります。 各インターフェイスは、GUID によって参照されます。
ms.assetid: 87A275B0-825A-47F1-9701-D7E91C493877
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1964a81972ae77c7034ae9d516437ab2f7b01274
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326117"
---
# <a name="available-interfaces-and-related-apis"></a>使用できるインターフェイスと関連する API


次の 3 つの GPIO インターフェイスがあります。 デバイスごとに 1 つ。 各インターフェイスは、GUID によって参照されます。

/\* 30ebfbf8-df5f-4d4d-9fc5-a26c7fd1df4a \*/define\_GUID (GUID\_GPIOBUTTONS\_通知\_インターフェイス、0x30ebfbf8、0xdf5f、0x4d4d、0x9f、0xc5、0xa2、0x6c、0x7f、0xd1、0 xdf、0x4a)。

/\* 317fc439-3f77-41c8-b09e-08ad63272aa3 \*/define\_GUID (GUID\_GPIOBUTTONS\_LAPTOPSLATE\_インターフェイス、0x317fc439、0x3f77、0x41c8、0xb0、0x9e、0x08、0xad など、0x27、0x2a、0xa3)。

/\* a84e689b-0dce-493a-a164-acde05478fc3 \*/define\_GUID (GUID\_GPIOBUTTONS\_DOCKMODE\_インターフェイス、0xa84e689b、0x0dce、0x493a、0xa1、0x64、0xac、0xde、0x05、0x47、0x8f、0xc3 です.)。

インターフェイスは、ボタンや、それぞれのデバイスのインターフェイスに対して WriteFile を呼び出すことによって切り替えるインジケーターの状態を許可します。

**注**  複数プロバイダー間の潜在的な競合を防ぐためには、デバイスを識別するハンドルは、デバイスへの排他アクセスを提供します。

 

``` syntax
typedef enum {
    GPIO_BUTTON_POWER,
    GPIO_BUTTON_WINDOWS,
    GPIO_BUTTON_VOLUME_UP,
    GPIO_BUTTON_VOLUME_DOWN,
    GPIO_BUTTON_ROTATION_LOCK,
} GPIOBUTTONS_BUTTON_TYPE;
```

 

 





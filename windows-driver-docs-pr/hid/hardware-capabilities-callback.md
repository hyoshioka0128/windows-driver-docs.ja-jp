---
title: ハードウェア機能コールバック
description: ハードウェア機能コールバック
ms.assetid: 407505e4-c0d7-4e12-80d7-55801a66f531
keywords:
- WDK ジョイスティックのコールバック
- ジョイスティックに WDK を非表示に機能
- ハードウェア機能コールバック WDK ジョイスティック
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 537057e18b0a1a297b5f57bce263b20173486a42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388934"
---
# <a name="hardware-capabilities-callback"></a>ハードウェア機能コールバック





```cpp
int __stdcall HWCapsRoutine( int joyid, LPJOYOEMHWCAPS pjhwc );
```

1 つは、デバイスのハードウェア機能を要求するたびに HWCapsRoutine が呼び出されます。 VJOYD から返す前に、VJoyD が HWCapsRoutine を呼び出すは具体的には、\_登録\_デバイス\_ドライバー。 そのため、ドライバーが、この呼び出し依存しているデバイスを登録する前に、初期化が完了したことが重要です。 これらの値は定数では一般的です。 4 つのボタンとうち、3 つ目をスロットルまたはラダー値のいずれか返す可能性があります、3 つの軸を持つデバイスを次に適切です。

```cpp
pjhwc->dwMaxButtons = 4;    /* This should always be the number of buttons */
pjhwc->dwMaxAxes = 4;       /* The largest axis number which may be requested */
pjhwc->dwNumAxes = 3;       /* The number of axes the device has */
```

 

 





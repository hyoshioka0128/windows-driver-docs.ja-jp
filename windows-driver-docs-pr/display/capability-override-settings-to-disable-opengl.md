---
title: 機能は、OpenGL を無効にする設定を上書き
description: すべてのボックスに表示 Inf のこのソフトウェアのデバイス設定では、既製の OpenGL ICDs で可能な相互運用性の問題にインボックス ドライバーを公開しないことが保証されます。
ms.assetid: 70903938-4A89-45A3-B1AD-B823C5735AB1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0d694a29aec1b1da8536772bf78d73b14e3a66d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558304"
---
# <a name="capability-override-settings-to-disable-opengl"></a>機能は、OpenGL を無効にする設定を上書き


すべてのボックスに表示 Inf のこのソフトウェアのデバイス設定では、既製の OpenGL ICDs で可能な相互運用性の問題にインボックス ドライバーを公開しないことが保証されます。

次に、例を示します。

``` syntax
[R200_SoftwareDeviceSettings]
HKR,, CapabilityOverride,                       %REG_DWORD%,    0x8
```

 

 






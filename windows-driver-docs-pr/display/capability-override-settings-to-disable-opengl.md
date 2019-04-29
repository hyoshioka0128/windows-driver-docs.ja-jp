---
title: OpenGL を無効にするための機能のオーバーライド設定
description: すべてのボックスに表示 Inf のこのソフトウェアのデバイス設定では、既製の OpenGL ICDs で可能な相互運用性の問題にインボックス ドライバーを公開しないことが保証されます。
ms.assetid: 70903938-4A89-45A3-B1AD-B823C5735AB1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0d694a29aec1b1da8536772bf78d73b14e3a66d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385681"
---
# <a name="capability-override-settings-to-disable-opengl"></a>OpenGL を無効にするための機能のオーバーライド設定


すべてのボックスに表示 Inf のこのソフトウェアのデバイス設定では、既製の OpenGL ICDs で可能な相互運用性の問題にインボックス ドライバーを公開しないことが保証されます。

次に、例を示します。

``` syntax
[R200_SoftwareDeviceSettings]
HKR,, CapabilityOverride,                       %REG_DWORD%,    0x8
```

 

 






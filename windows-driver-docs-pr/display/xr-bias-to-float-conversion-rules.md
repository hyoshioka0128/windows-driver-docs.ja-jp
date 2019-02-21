---
title: 変換規則のフローティング XR_BIAS
description: 変換規則のフローティング XR_BIAS
ms.assetid: fef4a1cb-6567-4d8f-aa8a-ceed00eefec8
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、XR_BIAS float への変換
- 拡張形式 XR_BIAS float への変換、Windows 7 の WDK の表示
- XR_BIAS を WDK Windows 7 の表示を float 型に変換します。
- XR_BIAS WDK Windows 7 の表示
- XR_BIAS WDK Windows 7 の表示、float 型に変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebaf3c24d26207973755fe44d1d5d512d118203b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529939"
---
# <a name="xrbias-to-float-conversion-rules"></a>XR\_変換規則のフローティング バイアス


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

次のコードが XR を変換する方法を示します\_float 型にバイアス。

```cpp
float XRtoFloat( UINT XRComponent ) {
// The & 0x3ff shows that only 10 bits contribute to the conversion. 
 return (float)( (XRComponent & 0x3ff) - 0x180 ) / 510.f;
}
```

 

 






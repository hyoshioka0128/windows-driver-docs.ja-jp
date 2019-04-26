---
title: 32 ビット ポインターと 64 ビット ポインター
description: 32 ビット ポインターと 64 ビット ポインター
ms.assetid: 641443b9-465f-4c7e-a13d-47a991304b46
keywords:
- 32 ビット ポインター、WdbgExts 拡張機能
- 64 ビットのポインター、WdbgExts 拡張機能
ms.date: 11/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 05a584cc956664402ec18ff9cf2de05f406fc8c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351504"
---
# <a name="32-bit-pointers-and-64-bit-pointers"></a>32 ビット ポインターと 64 ビット ポインター


## <span id="ddk_32_bit_pointers_and_64_bit_pointers_dbwx"></span><span id="DDK_32_BIT_POINTERS_AND_64_BIT_POINTERS_DBWX"></span>


WdbgExts.h ヘッダー ファイルには、ポインターを 32 ビットおよび 64 ビットの両方がサポートされています。 64 ビット ポインターを使用するには、次の順序には、コードの次の 2 行を含めるだけです。

```cpp
#define KDEXT_64BIT 
#include wdbgexts.h 
```

コードでは常に 64 ビット ポインターを使用することをお勧めします。 これにより、ターゲットが 32 ビットの場合は、デバッガーに 64 ビット ポインターを 32 ビットにはキャスト自動的に、拡張機能に、任意のプラットフォームで動作します。

32 ビット プラットフォーム上でのみ、拡張機能を使用する場合は、代わりに 32 ビットの拡張機能を記述できます。 その場合は、のみ、コードに次の行を含める必要があります。

```cpp
#include wdbgexts.h 
```
64 ビット ポインターの操作の詳細については、次を参照してください。 [DECLARE_API マクロを使用して](using-the-declare-api-macro.md)と[WdbgExts 拡張機能コードの記述](writing-wdbgexts-extension-code.md)します。 さらに、WDK の一部として含まれているサンプル コードを確認します。



 

 






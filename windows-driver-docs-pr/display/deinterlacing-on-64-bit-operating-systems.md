---
title: 64 ビット オペレーティング システムでのデインターレース
description: 64 ビット オペレーティング システムでのデインターレース
ms.assetid: ffac0c1a-2c92-4beb-9622-26d10e1a06aa
keywords:
- デインター レース WDK DirectX VA、64年ビット
- 64 ビットの WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ac6369578520237a9695065d6e84b5b250dd4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348899"
---
# <a name="deinterlacing-on-64-bit-operating-systems"></a>64 ビット オペレーティング システムでのデインターレース


実行されるようにする、32 ビット アプリケーションが開始したインター レース解除操作が正常に 64 ビットのオペレーティング システムで、ディスプレイ ドライバー コードする必要がありますまず検出アプリケーションは、32 ビットまたは 64 ビットかどうか。 検出を実行するドライバーを確認する必要があります、**サイズ**のメンバー、 [ **DXVA\_DeinterlaceBlt** ](https://msdn.microsoft.com/library/windows/hardware/ff563912)アプリケーションに渡される構造体。 DXVA の 32 ビット バージョンのサイズ\_DeinterlaceBlt は、32 ビットと 64 ビットのポインター サイズが異なるのため、64 ビット バージョンのサイズより小さい。 ドライバー、認識された場合、発信側アプリケーションが 32 ビット ドライバーでは、サンクによってデインター レースの操作を処理します。 サンクの詳細については、次を参照してください。 [、64 ビット ドライバーをサポートしている 32 ビットの I/O](https://msdn.microsoft.com/library/windows/hardware/ff563897)します。

次のコード例では、ドライバーがサンクを処理する方法を示しています。

```cpp
switch (lpData->dwFunction) {
case DXVA_DeinterlaceBltFnCode:
    {   
        DXVA_DeinterlaceBlt* pBlt = (DXVA_DeinterlaceBlt*)lpData->lpInputData; 
         if (pBlt->Size == sizeof(DXVA_DeinterlaceBlt)) {
            // correctly formed 64-bit or 32-bit structure, so use it
        }
#ifdef _WIN64
        else if (pBlt->Size < sizeof(DXVA_DeinterlaceBlt)) {
            // 32-bit structure, so thunk it!
        }
#endif
        else {
            // unknown structure, so return error;
        }
    }
```

 

 






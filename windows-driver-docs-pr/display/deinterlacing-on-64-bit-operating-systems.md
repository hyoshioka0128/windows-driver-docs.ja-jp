---
title: 64 ビット オペレーティング システムでのデインターレース
description: 64 ビット オペレーティング システムでのデインターレース
ms.assetid: ffac0c1a-2c92-4beb-9622-26d10e1a06aa
keywords:
- WDK DirectX VA、64ビットのノンインターレース
- 64-bit WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274d881b36689f6d2f0d89a88b8af43868e37a39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839757"
---
# <a name="deinterlacing-on-64-bit-operating-systems"></a>64 ビット オペレーティング システムでのデインターレース


32ビットアプリケーションによって開始されたノンインターレース操作が64ビットのオペレーティングシステムで正常に実行されるようにするには、アプリケーションが32ビットまたは64ビットのどちらであるかを、表示ドライバーコードで最初に検出する必要があります。 検出を実行するには、ドライバーは、アプリケーションが渡す[**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)構造体の**サイズ**メンバーを確認する必要があります。 32ビットバージョンの DXVA\_DeinterlaceBlt のサイズが64ビットバージョンのサイズよりも小さくなっています。これは、32ビットと64ビットの間でポインターサイズが異なるためです。 ドライバーが、開始アプリケーションが32ビットであると判断した場合、ドライバーは、サンキングによるノンインターレース化操作を処理する必要があります。 サンキングの詳細については、「 [64 ビットドライバーでの32ビット i/o のサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)」を参照してください。

次のコード例は、ドライバーがサンクを処理する方法を示しています。

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

 

 






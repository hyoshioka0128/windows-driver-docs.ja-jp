---
title: 64 ビット オペレーティング システムでのデインターレースと合成
description: 64 ビット オペレーティング システムでのデインターレースと合成
ms.assetid: af95b9f8-1329-4cba-a70f-4f1884f6a0f9
keywords:
- デインター レース WDK DirectX VA、64年ビット
- 64 ビットの WDK DirectX VA
- DXVA_DeinterlaceBltEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1c54f58b1621c844c25f8b7bbebab91dfd1f66b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572082"
---
# <a name="deinterlacing-and-compositing-on-64-bit-operating-systems"></a>64 ビット オペレーティング システムでのデインターレースと合成


このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

いることを確認する[サブストリーム合成の操作でデインター レース](performing-deinterlacing-with-substream-compositing-operations.md)32 ビット アプリケーションが 64 ビットのオペレーティング システムで正常に実行が開始されると、ディスプレイ ドライバー コードする必要があります最初検出アプリケーションは 32 ビットまたは 64 であるかどうかビット。 ドライバーの検出を実行するのサイズを確認する必要があります、 [ **DXVA\_DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563915)アプリケーションに渡される構造体。 ドライバー、認識された場合、発信側アプリケーションが 32 ビット ドライバーでは、サンクによってデインター レースの操作を処理します。 ドライバーを使用する必要があります、 [ **DXVA\_VideoSample32** ](https://msdn.microsoft.com/library/windows/hardware/ff564102)と[ **DXVA\_DeinterlaceBltEx32** ](https://msdn.microsoft.com/library/windows/hardware/ff563920)インター サンクを実行する構造体。 サンクの詳細については、次を参照してください。 [、64 ビット ドライバーをサポートしている 32 ビットの I/O](https://msdn.microsoft.com/library/windows/hardware/ff563897)します。

**注**   64 ビット ドライバーのコードがコンパイルされるとき、 [ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)構造体には、2 つの余分な DWORD メンバー、32 ビットのサイズを加えることにはが含まれています。バージョンの DXVA\_VideoSample2 64 ビット バージョンと異なります。 8 バイト アラインメントのため、32 ビット コンパイラは、32 ビット バージョンを--これら 2 つ余分な DWORD メンバー--なし、32 ビット バージョンでもポインターのサイズの差のアカウンティング、64 ビット バージョンと同じサイズの末尾に 4 バイトのパディングを追加します32 ビットと 64 ビットの間
DXVA に含まれる 2 つの余分な DWORD メンバーと\_64 ビット コンパイルの VideoSample2、ドライバーは、32 ビットおよび 64 ビット バージョンに基づくで区別できる、**サイズ**のメンバー、 [ **DXVA\_DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563915)構造体。

 

次のコード例では、ドライバーがサンクを処理する方法を示しています。

```cpp
switch (lpData->dwFunction) {
case DXVA_DeinterlaceBltExFnCode:
    {   DXVA_DeinterlaceBltEx* pBlt = (DXVA_DeinterlaceBltEx*)lpData->lpInputData; 
        switch (pBlt->Size) {
             case sizeof(DXVA_DeinterlaceBltEx): // should be 4400 bytes on Win64
                                                // should be 4144 bytes on Win32
                  break;
#ifdef _WIN64
             case sizeof(DXVA_DeinterlaceBltEx32): // should be 4144 bytes
                  // 32-bit structure, so thunk it!
                  break;
#endif
            default:
                  // unknown structure, so return error;
                  break;
            }
      }
```

 

 






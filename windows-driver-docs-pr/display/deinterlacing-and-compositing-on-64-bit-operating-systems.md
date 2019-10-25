---
title: 64 ビット オペレーティング システムでのデインターレースと合成
description: 64 ビット オペレーティング システムでのデインターレースと合成
ms.assetid: af95b9f8-1329-4cba-a70f-4f1884f6a0f9
keywords:
- WDK DirectX VA、64ビットのノンインターレース
- 64-bit WDK DirectX VA
- DXVA_DeinterlaceBltEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9cc9c9a11dfe4908148d650801f0b8dcbd2b3d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839759"
---
# <a name="deinterlacing-and-compositing-on-64-bit-operating-systems"></a>64 ビット オペレーティング システムでのデインターレースと合成


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

32ビットアプリケーションによって開始されるサブ[ストリーム合成操作によるノンインターレース](performing-deinterlacing-with-substream-compositing-operations.md)が64ビットオペレーティングシステム上で正常に実行されるようにするには、アプリケーションが32ビットまたは64ビットのどちらであるかを、表示ドライバーコードで最初に検出する必要があります。 検出を実行するには、ドライバーは、アプリケーションが渡す[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)構造体のサイズを確認する必要があります。 ドライバーが、開始アプリケーションが32ビットであると判断した場合、ドライバーは、サンキングによるノンインターレース化操作を処理する必要があります。 ドライバーは、 [**DXVA\_VideoSample32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample32)および[**DXVA\_DeinterlaceBltEx32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex32)構造体を使用して、インターレース解除サンクを実行する必要があります。 サンキングの詳細については、「 [64 ビットドライバーでの32ビット i/o のサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)」を参照してください。

**注**   ドライバーコードが64ビット用にコンパイルされている場合は、 [**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体に2つの追加の DWORD メンバーが含まれており、32ビットバージョンの DXVA\_VideoSample2 が64ビットバージョンとは異なるサイズになります。 8バイトのアラインメントのため、32ビットコンパイラは、32ビットバージョンの末尾に4バイトのパディングを追加します。この2つの余分な DWORD メンバーは含まれません。32ビットバージョンは、64ビットバージョンと同じサイズになります。ポインターサイズの違いについても考慮されます。32ビットから64ビット。
64ビットコンパイルの DXVA\_VideoSample2 に含まれる2つの追加の DWORD メンバーを使用すると、ドライバーは、 [**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)構造体の**サイズ**メンバーに基づいて、32ビットと64ビットの両方のバージョンを区別できます。

 

次のコード例は、ドライバーがサンクを処理する方法を示しています。

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

 

 






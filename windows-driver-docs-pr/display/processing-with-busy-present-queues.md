---
title: 現在ビジー状態のキューの処理
description: 現在ビジー状態のキューの処理
ms.assetid: 5fce137b-001c-49f6-85ad-94c9eead9aa0
keywords:
- ビジー状態に存在するキュー WDK DirectX 9.0
- 存在するキュー WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9ca64f2ad43c100ce617a6239331540319d4656
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580993"
---
# <a name="processing-with-busy-present-queues"></a>現在ビジー状態のキューの処理


## <span id="ddk_processing_with_busy_present_queues_gg"></span><span id="DDK_PROCESSING_WITH_BUSY_PRESENT_QUEUES_GG"></span>


DirectX 9.0 バージョンのドライバーが、DDERR を返す必要があります\_WASSTILLDRAWING 値への呼び出しからその[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)関数の場合は、ランタイムに渡される、DDFLIP\_DONOTWAIT フラグで、**dwFlags**のメンバー、 [ **DD\_FLIPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551520)構造と、ドライバーがない、プレゼンテーションをスケジュールする、現在キューは、完全またはドライバーが垂直同期の間隔で待機しているかどうかです。 ランタイムが呼び出す、ドライバーの*DdFlip* DDFLIP で関数を\_DONOTWAIT 設定、アプリケーションが呼び出された場合、 **IDirect3DSwapChain9::Present**メソッドを D3DPRESENT\_DONOTWAIT フラグを設定します。 場合は、ドライバーは、プレゼンテーションをスケジュールできませんその*DdFlip*返します DDERR\_で WASSTILLDRAWING、 **ddRVal** DD のメンバー\_FLIPDATA します。 アプリケーションの**存在**DDERR をさらに返します\_WASSTILLDRAWING で、アプリケーションで他の処理を実行することができます。

D3DPRESENT\_DONOTWAIT フラグは DirectX 9.0 の新機能です。 DDFLIP\_DONOTWAIT フラグ DirectX 7.0 以降が使用されています。 DirectX 7.0 アプリケーション DDFLIP を設定する場合\_DONOTWAIT への呼び出しで、 **IDirectDrawSurface7::Flip**メソッド、DirectX 7.0 またはそれ以降のドライバーの*DdFlip* DDFLIP を受け取る関数\_DONOTWAIT フラグ。

場合 D3DPRESENT\_DONOTWAIT が設定されていない**存在**DirectX 8.1 のように、以前に動作します。 つまり、**存在**エラーを返さずに、ハードウェアが無料、までスピンします。

詳細については**IDirect3DSwapChain*Xxx*:: 存在する**、DirectX SDK の最新のドキュメントを参照してください。

 

 






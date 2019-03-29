---
title: グラフィックス アダプターへのアクセス
description: グラフィックス アダプターへのアクセス
ms.assetid: 85c99b4b-690c-49f1-b6ed-4b72b6049026
keywords:
- ドライバー モデル WDK Windows 2000 では、グラフィックスを表示します。
- Windows 2000 のディスプレイ ドライバー モデル WDK、グラフィック
- ディスプレイ ドライバー WDK Windows 2000 では、グラフィック
- グラフィックス カード アクセス WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bfde5bd300e5e96b476078a714cef00629f93a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570458"
---
# <a name="accessing-the-graphics-adapter"></a>グラフィックス アダプターへのアクセス


## <span id="ddk_accessing_the_graphics_adapter_gg"></span><span id="DDK_ACCESSING_THE_GRAPHICS_ADAPTER_GG"></span>


パフォーマンスを表示するには、ディスプレイ ドライバーはグラフィックス カードを次の方法でアクセスできます。

-   Ioctl をグラフィックス アダプターのビデオのミニポート ドライバーに送信によって直接--します。 参照してください[通信ビデオのミニポート ドライバーに Ioctl](communicating-ioctls-to-the-video-miniport-driver.md)します。

-   読み取りと書き込みをビデオ メモリによって直接--(、*フレーム バッファー*) またはハードウェア レジスタ。 参照してください[フレーム バッファーとハードウェアにアクセスする登録](accessing-the-frame-buffer-and-hardware-registers.md)します。

 

 






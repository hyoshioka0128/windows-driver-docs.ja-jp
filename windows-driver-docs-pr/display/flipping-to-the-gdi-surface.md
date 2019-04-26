---
title: GDI サーフェスへの切り替え
description: GDI サーフェスへの切り替え
ms.assetid: e74e108d-f88c-4e42-9136-ef087378807a
keywords:
- 図面ページ WDK DirectDraw、GDI の画面を反転します。
- DirectDraw WDK Windows 2000 の表示、GDI の画面の回転
- 反転 WDK DirectDraw、GDI 画面ページします。
- WDK DirectDraw、GDI の画面の回転
- WDK DirectDraw を反転 GDI 画面
- WDK の DirectDraw を画面の回転
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5287f565c499a1325bc7b7d049946bc57359f1d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359404"
---
# <a name="flipping-to-the-gdi-surface"></a>GDI サーフェスへの切り替え


## <span id="ddk_flipping_to_the_gdi_surface_gg"></span><span id="DDK_FLIPPING_TO_THE_GDI_SURFACE_GG"></span>


GDI (デスクトップ) 画面が画面をプライマリになることができるように、ディスプレイ ドライバーを実装する必要があります。 これには、アプリケーションのダイアログ ボックスなど、GDI 側でレンダリングされるコンテンツを表示することができます。 ドライバーは、プライマリの表面に、GDI 画面に、次のメソッドのいずれかを使用できます。

-   ドライバーは、チェーンを反転ドライバーにバッファーの 1 つの GDI 画面を含めることができます。 このメソッドは、アプリケーションは GDI 画面に反転できるようにすることをお勧めの方法です。 既定では、アプリケーションが反転の要求を行うと DirectDraw 呼び出しを行うには、ドライバーの[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)ことで、相互に接続された順序でバッファーを順番に関数、チェーン。 アプリケーションは、GDI サーフェスのチェイン内の位置を決定することにより、反転要求の適切な数を使用して、GDI の画面に反転できます。

-   ドライバーを実装できる、 [ *DdFlipToGDISurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549335) GDI サーフェイスとの間、DirectDraw を反転するときに通知を受信する関数。 ドライバーが、GDI 画面にアクセスできる場合、ドライバーをこの通知を受信した後、GDI のサーフェイスに反転できます。 このメソッドを使用して、ドライバーのフリッピング チェーンの一部として、GDI 画面は必要ありません。

 

 






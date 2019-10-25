---
title: グラフィックスドライバーの GDI サポート
description: グラフィックスドライバーの GDI サポート
ms.assetid: ef42cda0-106f-4c1b-babc-29a1070e2a2f
keywords:
- GDI WDK Windows 2000 表示、リファレンス
- グラフィックスドライバー WDK Windows 2000 表示、リファレンス
- WDK GDI の描画、リファレンス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb40614162608e34f5249d20c63a8de776796f66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839683"
---
# <a name="gdi-support-for-graphics-drivers"></a>グラフィックスドライバーの GDI サポート


## <span id="ddk_gdi_support_for_graphics_drivers_gg"></span><span id="DDK_GDI_SUPPORT_FOR_GRAPHICS_DRIVERS_GG"></span>


ここでは、Microsoft Windows NT ベースのオペレーティングシステムグラフィックデバイスインターフェイス (GDI) について説明します。 その後、GDI がグラフィックスドライバーに提供するサポートの詳細について説明します。

このセクションの GDI への参照は、カーネルモード GDI への暗黙的な参照です。Microsoft Win32 GDI が明示的に識別されます。 カーネルモード GDI は、グラフィックスエンジンとも呼ばれます。

GDI 関数と構造体のリファレンスについては、「[表示デバイスのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」セクションを参照してください。 ほとんどの GDI 関数の宣言と構造体の定義は、 *Winddi .h*にあります。 ディスプレイドライバーの場合、Microsoft DirectDraw heap manager 関数は*Dmemmgr*で宣言されています。 両方のファイルには、Windows Driver Kit (WDK) が付属しています。

 

 






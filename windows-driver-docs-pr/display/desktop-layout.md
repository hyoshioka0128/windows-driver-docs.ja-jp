---
title: デスクトップ レイアウト
description: デスクトップ レイアウト
ms.assetid: f1c074ec-2fce-4e46-ba0d-62e05ca8a9e7
keywords:
- Windows 7 の WDK の表示、CCD 概念、デスクトップ レイアウトの接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、レイアウトをデスクトップの接続が表示されます。
- Windows 7 の WDK の表示、CCD 概念、デスクトップ レイアウトに表示を構成します。
- WDK の Windows Server 2008 R2 の表示、CCD 概念、レイアウトをデスクトップの構成が表示されます。
- CCD 概念 WDK Windows 7 のディスプレイ、デスクトップ レイアウト
- CCD 概念 WDK Windows Server 2008 R2 のディスプレイ、デスクトップ レイアウト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7ce5023643ffb028182eeb55701b114a11a910c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384890"
---
# <a name="desktop-layout"></a>デスクトップ レイアウト


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

呼び出し元を使用して、**位置**のメンバー、 [ **DISPLAYCONFIG\_ソース\_モード**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_source_mode)構造体への呼び出しで、 [ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)デスクトップでソースの配置を制御する CCD 関数を表示します。 **位置**メンバーをデスクトップ座標でソース画面の左上隅の位置を指定します。 配置されるソース画面 (0, 0) は、プライマリのサーフェスを検討してください。 GDI では、デスクトップ領域内のソースのサーフェスの配置方法についての厳密な規則があります。 たとえば、GDI には、ソース サーフェス ソース サーフェスとなしの重複の間のギャップはできません。

[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)しようとすると、再配置とソースの表面をこれらの GDI レイアウト規則の実施、呼び出し元はソースのサーフェスのレイアウトを指定する必要があります。 GDI がそのレイアウト ルールを適用するソース サーフェスを再配置する方法は未定義し、ソース サーフェスのレイアウトに実現するために必要に応じて、呼び出し元ができません。

 

 






---
title: グラフィックス システムの概要
description: グラフィックス システムの概要
ms.assetid: d120a9df-d8ed-4862-b421-2e7545be1ed0
keywords:
- グラフィックス システムについて、GDI WDK Windows 2000 の表示
- グラフィックス システムについて、グラフィック ドライバー WDK Windows 2000 の表示します。
- 描画の WDK GDI やグラフィックス システムについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b924e74279ec3a8fca7fe44b78245422100caa4d
ms.sourcegitcommit: 4a371c2e8a2aa42f2e2744df1544ea69e42f4fc3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2019
ms.locfileid: "57788777"
---
# <a name="graphics-system-overview"></a>グラフィックス システムの概要


## <span id="ddk_graphics_system_overview_gg"></span><span id="DDK_GRAPHICS_SYSTEM_OVERVIEW_GG"></span>


ベースの Microsoft Windows で nt (tm) オペレーティング システムでは、サード パーティ製のグラフィックス ハードウェアの企業は、ビデオの表示と印刷デバイス簡単に統合する堅牢なグラフィックス アーキテクチャを提供します。 これらのセクションでは、有効なグラフィック ドライバーを記述するためのデザイン ガイドラインを示します。

-   [**グラフィックス DDI**](using-the-graphics-ddi.md)

    このセクションでは、Windows グラフィックス デバイス インターフェイス (GDI) とグラフィックス デバイスのドライバー インターフェイス (DDI) について説明します。 ドライバーの表示と印刷の両方に共通する設計と実装の詳細に説明します。

-   [**Windows Display Driver Model (WDDM) 設計ガイド**](windows-vista-display-driver-model-design-guide.md)

    [**Windows 2000 Display Driver Model (XDDM) 設計ガイド**](windows-2000-display-driver-model-design-guide.md)

    これらのセクションでは、Windows NTâˆ でビデオ ディスプレイ環境を表す ' ベースのオペレーティング システムとの設計と実装の詳細表示、ビデオのミニポートを指定、およびドライバー開発者を監視します。 Windows 8 およびそれ以降のコンピューター上で Windows 2000 Display Driver Model ドライバーに準拠するをインストールできないことに注意してください。

-   [**印刷デバイスの設計ガイド**](https://msdn.microsoft.com/library/windows/hardware/ff561035)

    このセクションでは、ドライバーと印刷スプーラ Windows NTâˆ で印刷環境を構成するについて説明します。 ' ベースのオペレーティング システム。 Windows Driver Kit (WDK) のこの部分内のセクションでは、新しいプリンターのハードウェアとネットワークの構成をサポートできるように、カスタマイズされたドライバーとスプーラー コンポーネントを提供する方法を指定します。

 

 






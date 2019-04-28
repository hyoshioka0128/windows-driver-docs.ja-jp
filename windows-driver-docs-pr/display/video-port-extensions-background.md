---
title: 背景のビデオ ポート拡張機能
description: 背景のビデオ ポート拡張機能
ms.assetid: 77bed8d3-4fe5-4159-88e9-d6565aea9117
keywords:
- ビデオ ポートの拡張機能の詳細については、DirectX VPE サポート WDK DirectDraw、
- 描画 VPEs WDK DirectDraw のビデオ ポートの拡張機能について
- 拡張機能のビデオ ポートについて、DirectDraw VPEs WDK Windows 2000 の表示
- ビデオ ポートの拡張機能についてのビデオ ポート拡張 WDK DirectDraw、
- 拡張機能のビデオ ポートについて、VPEs WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 893d01ca1a6490c270c8825d43d4b67290f0fc9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365046"
---
# <a name="video-port-extensions-background"></a>背景のビデオ ポート拡張機能


## <span id="ddk_video_port_extensions_background_gg"></span><span id="DDK_VIDEO_PORT_EXTENSIONS_BACKGROUND_GG"></span>


ビデオ ポートの拡張機能 (VPE) テクノロジは、グラフィックス フレーム バッファーにビデオ デコーダーおよび autoflipping から直接ハードウェアの接続をサポートする DirectDraw 拡張機能です。

ビデオ データが、フレーム バッファーに配置されると、表示するにはビデオ オーバーレイを使用できます。 グラフィックス システムでビデオのオーバーレイでは、アナログ デジタル コンバーター (DAC) は通常表示されませんのリージョンでデータを表示するように指示します。 中は、データを表示する必要はないため、およびビデオのデータを表示フレーム バッファーよりも高い色深度で表示できるため、オーバーレイの使用は効率的です。

ハードウェアのビデオ ポートは、PCI、AGP バスではなく使用できるビデオ ストリーム配信オプションです。 PCI 帯域幅を必要とするその他のアプリケーションと同時に実行されるアプリケーションは、ハードウェアのビデオ ポートを使用してデコーダーと VGA グラフィックスのコント ローラー間の待機時間の短いビデオ伝送をことを確認することをお勧めします。 このルートは、特定のグラフィックス チップセット、デコーダーを結び付けることが必要な場合は、PCI バスをバイパスする機会を得られます、PCI バス ソリューションとしての柔軟性はありません。

説明されている、カーネル モードのビデオ トランスポート機能、[カーネル モードのビデオ トランスポート](kernel-mode-video-transport.md)セクションで、VPE ことを確認するためのサポートはビデオ再生の品質を強化し、ビデオのキャプチャのサポートが強化されても提供します。 ドライバーは、Windows 2000 以降で VPE をサポートするためにカーネル モードのビデオ トランスポートをサポートする必要があります。

VPE には、ハードウェア ベースのデータ接続のみがサポートしています。 カーネル モードのビデオ トランスポートでは、データ転送に直接アクセスをサポートしています。

VPE は WDM テクノロジではありません。 Windows 2000 以降、WDM、ディスプレイ ドライバーではなく、他の周辺機器に使用されます。

VPE サポートは、DirectX の最新バージョンの一部であるため、アプリケーションは、これらの機能とソリューションが VPE Windows 2000 以降をサポートする任意のグラフィック カードで動作する保証の利用できます。

 

 






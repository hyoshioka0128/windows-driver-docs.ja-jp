---
title: カーネル モードのビデオ トランスポート
description: カーネル モードのビデオ トランスポート
ms.assetid: 3acaabc7-8d9f-441b-9170-2e5a4e0ce114
keywords:
- 描画カーネル モードのビデオ トランスポート WDK DirectDraw、カーネル モードのビデオ トランスポートについて
- カーネル モードのビデオ トランスポートに関する、DirectDraw カーネル モードのビデオ トランスポート WDK Windows 2000 の表示します。
- カーネル モードのビデオ トランスポートに関するビデオ トランスポート WDK DirectDraw、カーネル モード
- ビデオ トランスポートのカーネル モードの WDK DirectDraw、カーネル モードのビデオ トランスポートについて
- カーネル モードのビデオ トランスポート WDK DirectDraw を描画
- DirectDraw カーネル モードのビデオ トランスポート WDK Windows 2000 の表示します。
- カーネル モードのビデオ トランスポート WDK DirectDraw
- ビデオのカーネル モードの WDK DirectDraw をトランスポート
- WDK DirectDraw を一元管理します。
- ビデオ キャプチャ WDK ビデオ トランスポート カーネル モード
- miniVDD WDK DirectDraw
- バス WDK DirectDraw をマスター
- V 同期 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e47a61baa89f585df507c30b8b10e263cee410a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530781"
---
# <a name="kernel-mode-video-transport"></a>カーネル モードのビデオ トランスポート


## <span id="ddk_kernel_mode_video_transport_gg"></span><span id="DDK_KERNEL_MODE_VIDEO_TRANSPORT_GG"></span>


このトピックでは、Microsoft Windows 2000 と以降のオペレーティング システムに存在するカーネル モードのビデオ トランスポートについて説明します。

カーネル モードのビデオ トランスポートは、ビデオの機能を強化する ring 0 (カーネル モード) で新しい Microsoft DirectDraw コンポーネントを指します。 このコンポーネントでは、DxApi インターフェイスにアクセスします。 このインターフェイスに追加されて、[ビデオのミニポート ドライバー](video-miniport-drivers-in-the-windows-2000-display-driver-model.md) Windows 2000 と以降のオペレーティング システム。

### <a name="span-idwindows2000andlaterspanspan-idwindows2000andlaterspanwindows-2000-and-later"></a><span id="windows_2000_and_later"></span><span id="WINDOWS_2000_AND_LATER"></span>Windows 2000 以降

カーネル モードのビデオ トランスポートは、DirectShow などのクライアントがビデオの機能を強化するために使用できる Microsoft DirectDraw コンポーネントを指します。 この機能の主な役割は、ハードウェアのビデオ ポートを実行し、V 同期が発生したときに、反転をオーバーレイするようにして、ミニポート ドライバーを呼び出されます。 この機能は、ハードウェアのビデオ ポート V 同期割り込み要求 (IRQ) をサポートしていれば、ハードウェアの制限の影響を受けずに最大 10 個のバッファーをサポートできます。 この機能は、DirectDraw autoflipping がクライアントによって指定され、ハードウェアできません autoflip Microsoft DirectX 5.0 およびそれ以降のバージョンに付属しているのバージョンによって自動的に使用されます。

カーネル モードのビデオ トランスポートでは、強化されたキャプチャのサポートも確認します。 Microsoft Windows 98]、[自分と Microsoft Windows 2000 以降の WDM ベースのビデオ キャプチャ ドライバーをフレーム バッファーに直接アクセスできる、カーネル モードで実行します。 キャプチャ ドライバーは、オーバーレイを反転「手動で」できます。 Windows 2000 およびミニポートのビデオ トランスポートの以降のバージョンのドライバーが V 同期の通知を表示し、またはハードウェアのビデオ ポートからを指定できます。フィールドの極性は、垂直帰線消去期間 (VBI) データをキャプチャするときに役に立ちます取得することもできます。

カーネル モード ドライバーの主な目的は、ハードウェアのビデオ ポート autoflipping 機能を強化するためには、ビデオ バス マスターは、カーネル モードでのデータを書き込むことができますもサポートします。 バス マスターは、モードが変更されたため、画面を失う前に通知が全画面表示のコマンド プロンプト インスタンスが起動されるので、または。 新しいドライバーのサポートは、変更が発生する前に呼び出されるバス マスターで、あるため、バス マスターできる問題を発生させることがなくシャット ダウンします。

 

 






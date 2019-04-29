---
title: DirectX のビデオ ポート拡張機能
description: DirectX のビデオ ポート拡張機能
ms.assetid: 42309279-e98a-4091-8f01-5d0d418e9ef2
keywords:
- DirectX VPE サポート WDK DirectDraw
- 描画 VPEs WDK DirectDraw
- DirectDraw VPEs WDK Windows 2000 の表示
- 拡張機能のビデオ ポート WDK DirectDraw
- VPEs WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd29117ae39430b4feb1ff95f982883fc772a14d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389606"
---
# <a name="video-port-extensions-to-directx"></a>DirectX のビデオ ポート拡張機能


## <span id="ddk_video_port_extensions_to_directx_gg"></span><span id="DDK_VIDEO_PORT_EXTENSIONS_TO_DIRECTX_GG"></span>


ハードウェアのビデオ ポートを使用したデバイスのドライバー開発者向けには、Microsoft DirectX にビデオ ポート拡張機能 (VPE) を実装する必要があります。 ハードウェアのビデオ ポート VGA グラフィックス コント ローラーには、フレーム バッファーにデータを取得するための高速なメカニズムを提供します。 ハードウェアのビデオ ポートは、通常ハードウェア Moving Pictures Experts Group (MPEG) デバイスまたは National テレビ標準委員会 (NTSC) のデコーダーおよびビデオ カードの間のビデオ デバイス間専用接続です。 この専用の接続は、水平方向の同期 (sync H) と垂直方向の同期 (V sync) の情報、ビデオ データを実行します。 ハードウェアのビデオ ポートとオーバーレイは、別、オーバーレイが表示されている間、1 つの画面への書き込み、複数のバッファー間で自動的に反転する、この同期情報を使用することができます。 これにより、アプリケーションの負荷をかけずに終了処理のないビデオです。

VPE でビデオ ポートを MPEG または NTSC デコーダーとハードウェアの間の接続をネゴシエートするクライアント--Microsoft DirectShow 通常--にできます。 VPE では、クライアントはのトリミングおよびスケーリングなど、ビデオ ストリームの効果を制御することもできます。 だけは、クライアントによってその要求内容が VPE 実装を行う必要があります。たとえば、場合にのみをトリミング クライアント要求トリミングにする必要があります。

Microsoft DirectDraw VPE オブジェクトが受信シグナルを監視し、反転のイメージを変更するには、そのインターフェイス メソッドの実行にパラメーター セットを使用して、フレーム バッファーにイメージ データを渡すやその他のサービスを実行します。 ビデオ デコーダーまたはビデオ ソース VPE オブジェクトは制御されません。

Microsoft Windows 2000 とビデオ ポートを後でシステムのモジュールに関連付けられていない、VPEs *videoprt.sys*します。

 

 






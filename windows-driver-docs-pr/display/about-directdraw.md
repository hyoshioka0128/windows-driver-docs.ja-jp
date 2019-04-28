---
title: DirectDraw について
description: DirectDraw について
ms.assetid: f2ab4863-8ec8-4eaf-b59f-635570aef470
keywords:
- 描画の WDK DirectDraw、DirectDraw について
- DirectDraw について、DirectDraw WDK Windows 2000 の表示
- WDK DirectDraw を破棄します。
- 画面のちらつき WDK DirectDraw
- GDI WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e390ecaad27c60aac89329c271eb9cc3b7f20615
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381891"
---
# <a name="about-directdraw"></a>DirectDraw について


## <span id="ddk_about_directdraw_gg"></span><span id="DDK_ABOUT_DIRECTDRAW_GG"></span>


Microsoft DirectDraw は、ソフトウェア設計者は表示メモリ、ハードウェア blitters、ハードウェアのオーバーレイ、反転サーフェスを直接操作できるようにする Microsoft DirectX の表示のコンポーネントです。 DirectDraw では、ゲームや 3D グラフィックス パッケージや特定のディスプレイ デバイスの機能にアクセスする、デジタル ビデオ コーデックなどの Windows サブシステム ソフトウェアをデバイスに依存しない方法を提供します。

DirectDraw では、デバイス固有の表示機能は、32 ビットの直接パスへのデバイスに依存しないアクセスを提供します。 DirectDraw は、ディスプレイ カードを直接、Windows グラフィックス デバイス インターフェイス (GDI) またはデバイスに依存しないビットマップ (DIB) エンジンの介入なしにアクセスするドライバーの重要な機能を呼び出します。

この直接パスを利用して高速に実行ゲームやその他の表示処理を要するアプリケーションと分裂を回避します。 A*破棄*イメージが表示され、同時に書き込まれるによる画面のちらつきが。 直接アクセスするには、ゲームのパフォーマンスの表示のカードのパフォーマンスによってのみ制限を多くの場合、できます。 DirectDraw も使用ページの反転を滑らかなアニメーションを提供します。

迅速なモーションと多くのゲームやマルチ メディア アプリケーションの画面を絶えず変化する、表示プロセスに大きな負荷を配置および解除を行うたびに悪化する傾向があります。 GDI は図面スプレッドシート、グラフ、TrueType フォントのレンダリングに非常に高速ですが、リアルタイムのグラフィックス API には行われません。 DirectDraw は、GDI を強化し、32 ビット ドライバーのデバイスに依存するハードウェア アクセラレータ機能を処理します。

 

 






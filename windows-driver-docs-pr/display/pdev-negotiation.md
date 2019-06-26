---
title: PDEV ネゴシエーション
description: PDEV ネゴシエーション
ms.assetid: d3172dd2-ecf1-4ad8-ba52-776bf712ab7c
keywords:
- GDI WDK Windows 2000 の表示、PDEV ネゴシエーション
- グラフィックス ドライバー WDK Windows 2000 の表示、PDEV ネゴシエーション
- 描画 WDK GDI、PDEV ネゴシエーション
- WDK GDI のネゴシエーション
- PDEV WDK GDI
- DrvEnablePDEV
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db8bc6196338c85b439b1605ec429510ac8b5f64
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353838"
---
# <a name="pdev-negotiation"></a>PDEV ネゴシエーション


## <span id="ddk_pdev_negotiation_gg"></span><span id="DDK_PDEV_NEGOTIATION_GG"></span>


任意のグラフィック ドライバーの主な責務の 1 つを有効にするのには、 *PDEV*ドライバーの初期化中にします。 PDEV は、物理デバイスの論理表現です。 この表現は、ドライバーによって定義され、プライベート データ構造体を通常は。 参照してください[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev) PDEVs を有効にする方法の詳細について。

を通じて、 *DrvEnablePDEV*関数の場合、ドライバーする必要がありますに情報を提供 GDI を要求されたデバイスとその機能について説明します。 重要な情報が、ドライバーは、GDI ことの 1 つはグラフィックス機能フラグのセット (GCAPS\_Xxx と GCAPS2\_Xxx フラグ) で、 **flGraphicsCaps**と**flGraphicsCaps2**のメンバー、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

機能フラグを使用すると、GDI PDEV、サポートされる操作を決定します。 GDI で示す処理かどうか、PDEV できますベジエ曲線と幾何学的線 GDI を呼び出す前に機能フラグをテストするなど、 [ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)でパスを描画するために関数これらのプリミティブ型。 PDEV がこれらのプリミティブ型を処理できないことで機能フラグを示す場合は、ドライバーに呼び出しを単純なことができるように、直線や曲線を GDI が中断されます。

ドライバーの側から、ドライバーは、GDI から、高度なパスに関連する呼び出しを取得するたびに返すことができます**FALSE**パスまたはクリッピングが複雑すぎるため、デバイスを処理する場合。

ドライバーは、返すことはできません**FALSE**から*DrvStrokePath*処理するときに、[表面的な行](cosmetic-lines.md)のため、ドライバーは、任意の複雑なクリッピングまたは表面的な行のスタイルを処理する必要があります。 ただし、 *DrvStrokePath*返せる**FALSE**ベジエ曲線または幾何学的行にパスがある場合。 この場合、GDI が機能ビットが設定されていない場合と同様に呼び出しを単純な呼び出しを代行させますが中断します。 たとえば場合、 *DrvStrokePath*返します**FALSE** GDI が行と呼び出しを簡略化 geometric ラインを送信するとき、 [ **DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)関数。

場合*DrvStrokePath* 、エラーをレポートには、DDI を返す必要があります\_エラー。

この種の GDI と、ドライバーは、PDEV に依存する関数の間のネゴシエーションでは、余分な通信を行わない高品質な出力を生成するには、GDI とドライバーを許可します。

 

 






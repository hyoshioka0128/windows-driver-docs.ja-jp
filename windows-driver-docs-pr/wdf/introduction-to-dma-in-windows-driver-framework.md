---
title: Windows Driver framework での DMA の概要
description: Windows Driver framework での DMA の概要
ms.assetid: 9bcd8ac1-f3dd-4bb3-a671-51c9465f8efa
keywords:
- DMA 操作 WDK KMDF、DMA 操作について
- DMA 操作について、バス マスター DMA の WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a862b13160c7f079c6b82584d01d60b30e6c075
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579613"
---
# <a name="introduction-to-dma-in-windows-driver-framework"></a>Windows Driver framework での DMA の概要


\[KMDF にのみ適用されます。\]




Windows 7 以降、カーネル モード ドライバー フレームワーク (KMDF) には、バス マスター ダイレクト メモリ アクセス (DMA) デバイスのみがサポートしています。 このようなデバイスには、独自の DMA コント ローラーが含まれています。

チップ (SoC) のシステムに – ベースのプラットフォームが Windows 8 を実行し、後で、フレームワークは、システム モードの DMA を使用して、複数のデバイスが共有する単一のマルチ チャンネル DMA コント ローラーもをサポートします。

DMA のフレームワークのサポートは、で構成されます。

-   I/O 要求を DMA 操作に変換するドライバーが使用されるフレームワーク DMA オブジェクトとメソッドのセット。

-   さまざまなイベントが発生したときに、デバイスの DMA の動作を構成するドライバーが指定したイベントのコールバック関数のセット。

フレームワークには、両方の単一パケットとスキャッター/ギャザー DMA 転送がサポートされています。 一般的なバッファーの使用もサポートしています。

Windows 8 以降を実行している SoC ベースのプラットフォームでは、フレームワークには、単一パケットのシステム モード DMA の転送がサポートされています。 詳細については、[をサポートしているシステム モード DMA](supporting-system-mode-dma.md)を参照してください。

フレームワークは、PC ベースのプラットフォームでサポート システム モードの DMA 転送されません。

 

 






---
title: Windows Driver framework での DMA の概要
description: Windows Driver framework での DMA の概要
ms.assetid: 9bcd8ac1-f3dd-4bb3-a671-51c9465f8efa
keywords:
- DMA 操作 WDK KMDF、DMA 操作について
- バスマスタ DMA WDK KMDF、DMA 操作について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8a50cb13e6778122d13df46a4c62ca80cddd4ff
ms.sourcegitcommit: 2d999dcf63d3b67bf74777d6fae29d96b98141ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84714827"
---
# <a name="introduction-to-dma-in-windows-driver-framework"></a>Windows Driver framework での DMA の概要


\[KMDF にのみ適用されます\]




Windows 7 以前では、カーネルモードドライバーフレームワーク (KMDF) は、バスマスタダイレクトメモリアクセス (DMA) デバイスのみをサポートしています。 このようなデバイスには、独自の DMA コントローラーが含まれています。

Windows 8 以降を実行しているチップ (SoC) ベースのプラットフォーム上では、複数のデバイスが1つのマルチチャネル DMA コントローラーを共有するシステムモードの DMA もサポートされています。

フレームワークの DMA サポートは次の要素で構成されます。

-   ドライバーが i/o 要求を DMA 操作に変換するために使用する一連のフレームワーク DMA オブジェクトとメソッド。

-   デバイスの DMA 動作を異なるイベントとして構成する、ドライバーが提供するイベントコールバック関数のセット。

フレームワークでは、シングルパケットとスキャッター/ギャザー DMA 転送の両方がサポートされています。 また、共通バッファーの使用もサポートしています。

Windows 8 以降を実行している SoC ベースのプラットフォームでは、フレームワークはシングルパケットシステムモードの DMA 転送をサポートしています。 詳細については、「[システムモードの DMA のサポート](supporting-system-mode-dma.md)」を参照してください。

このフレームワークでは、PC ベースのプラットフォームでのシステムモードの DMA 転送はサポートされていません。

 ## <a name="related-topics"></a>関連トピック
 
 [デバイス ドライバーのための DMA 再マッピングを有効にする](https://docs.microsoft.com/windows-hardware/drivers/pci/enabling-dma-remapping-for-device-drivers)

 






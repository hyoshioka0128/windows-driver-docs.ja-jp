---
title: Receive Side Scaling
description: Receive Side Scaling
ms.assetid: 380feb24-1f5e-4faa-9c98-1b3c8fdc27cb
keywords:
- ネットワーク ドライバー WDK、receive side scaling
- 受信側スケーリング WDK ネットワーク、NDIS 6.0
- ネットワーク、NDIS 6.0 RSS WDK
- ネットワーク受信 WDK RSS を処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0f7c58b1abeaf677c79cd6a10a825bd4cfb3c0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582623"
---
# <a name="receive-side-scaling"></a>Receive Side Scaling





受信側が scaling (RSS) マルチプロセッサ システムのネットワーク データの処理に関連するシステムのパフォーマンスが向上します。

RSS の概要については、[Receive Side Scaling の概要](introduction-to-receive-side-scaling.md)を参照してください。

Windows 10 バージョン 1709 以降 RSS バージョン 2 (RSSv2) は、ミニポート ドライバーを使用できます。 RSSv2 あたり VPort の拡散を提供することでは、基本の RSS モデルが向上します。 詳細については、[受信側のスケーリングのバージョン 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)を参照してください。 RSSv2 は、Windows 10 バージョン 1709 でのみプレビューです。

次のトピックでは、ハードウェアとソフトウェアのサポートのさまざまなレベルで使用できる RSS 実装について説明します。

[RSS 以外の受信処理](non-rss-receive-processing.md)

[受信キューに 1 つのハードウェアでの RSS](rss-with-a-single-hardware-receive-queue.md)

[ハードウェア キューでの RSS](rss-with-hardware-queuing.md)

[RSS をメッセージ シグナル割り込み](rss-with-message-signaled-interrupts.md)

次のトピックでは、RSS に関する追加情報を提供します。

[RSS ハッシュ型](rss-hashing-types.md)

[RSS ハッシュ関数](rss-hashing-functions.md)

[RSS ハッシュの計算結果を確認しています](verifying-the-rss-hash-calculation.md)

[RSS の構成](rss-configuration.md)

[RSS CPU 構成の設定](setting-the-rss-cpu-configuration.md)

[RSS の標準化された INF キーワード](standardized-inf-keywords-for-rss.md)

[データを受信するかを示す RSS](indicating-rss-receive-data.md)

[中間ドライバーまたはフィルター ドライバーで RSS をサポートしています。](supporting-rss-in-intermediate-drivers-or-filter-drivers.md)

 

 






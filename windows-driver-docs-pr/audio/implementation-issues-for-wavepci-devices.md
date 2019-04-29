---
title: WavePci デバイス用の実装に関する問題
description: WavePci デバイス用の実装に関する問題
ms.assetid: c286d745-6e76-4540-98e6-a46ce1dd0f5d
keywords:
- WDM オーディオ ドライバー WDK、WavePci
- オーディオ ドライバー WDK、WavePci
- WavePci デザイン ガイドライン WDK オーディオ
- スキャッター/ギャザー DMA WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50f5418f7657e8d178d2cd862723255895971f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333483"
---
# <a name="implementation-issues-for-wavepci-devices"></a>WavePci デバイス用の実装に関する問題


## <span id="implementation_issues_for_wavepci_devices"></span><span id="IMPLEMENTATION_ISSUES_FOR_WAVEPCI_DEVICES"></span>


ここでは、オーディオ ハードウェア ベンダーが WavePci デバイスの信頼性とパフォーマンスを向上させるために使用するハードウェアとソフトウェアの設計のガイドラインを示します。 オーディオ デバイスと Microsoft Windows XP 以降が動作するように設計されたドライバーをすべて次のガイドラインの適用が、多くは Windows 98 Second Edition に戻ると Windows の以前のバージョンにも適用されます。

説明したよう[Wave フィルター](wave-filters.md)、ポート クラス システム ドライバー Portcls.sys、wave レンダリングとキャプチャのデバイス ドライバーの 2 つの別のポートを提供します。

-   WaveCyclic はハードウェアとソフトウェアの要求が少なくなるが、バッファー間でデータをコピーするソフトウェア オーバーヘッドによって、パフォーマンスが制限されます。

-   WavePci がパフォーマンス指向の代替 WaveCyclic、方法がより高度なハードウェアとドライバー ソフトウェアが必要です。

名前が示す、PCI バスに接続するオーディオ デバイスを WavePci 実際には、WavePci デバイスの主な要件がスキャッター/ギャザー DMA コント ローラー システム メモリ内で任意の場所データにアクセスすることにはが含まれています。

-   一般的な WavePci デバイスは、PCI バス上しますが、理論上は、少なくとも、WavePci ミニポート ドライバーでした書き込まが存在するデバイスの PCI (たとえば、AGP) 以外のシステム バス。

-   PCI バス上に存在するが、スキャッター/ギャザーがありません wave デバイス WavePci ドライバーではありませんが、WaveCyclic ドライバーによって、DMA を表すことができます。

これまで、一部のベンダーでは、WavePci デバイスを完全に機能の実装の難しさがありました。 2 つの主な問題領域は次のとおりです。

1.  パフォーマンスが低下するハードウェア設計の欠陥です。

2.  パフォーマンスや信頼性に影響を与えるドライバーの実装のエラー。

このエクスペリエンスは次のトピックは、主要なハードウェアや WavePci デバイス用のソフトウェア設計の問題の対処に distilled:

[WavePci デバイスのハードウェア要件](hardware-requirements-for-wavepci-devices.md)

[WavePci ミニポート ドライバーのパフォーマンスの問題](performance-issues-for-a-wavepci-miniport-driver.md)

[WavePci ミニポート ドライバーの信頼性の問題](reliability-issues-for-a-wavepci-miniport-driver.md)

 

 





---
title: WaveRT ポート ドライバーの概要
description: WaveRT ポート ドライバーの概要
ms.assetid: 48b2b59e-385e-4814-ac20-c4b1a08f32dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 624a4c0524fde1a19e701bf6ff9c4c54fad1b15f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333421"
---
# <a name="introducing-the-wavert-port-driver"></a>WaveRT ポート ドライバーの概要


Windows Vista およびそれ以降のオペレーティング システムでは、サポートは、wave リアルタイム (WaveRT) ポートれるドライバーのパフォーマンスの向上を実現がの表示、およびオーディオ ストリームをキャプチャするための単純な循環バッファーを使用して提供されます。

WaveRT ポート ドライバーのパフォーマンス向上にはには、次の特性が含まれています。

-   Wave キャプチャ中に低待機時間と wave レンダリング

-   障害回復力のあるオーディオ ストリーム

WaveRT ポート ドライバーがの汎用機能を提供する Microsoft Windows の以前のバージョンで WaveCyclic と WavePci ポート ・ ドライバーのように、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS) フィルター。 WaveRT ポート ドライバーは、次のオーディオ デバイスのサポートを提供します。

-   PCI Express バスなど、システム バスに接続することができます。

-   Wave データを再生または録音できます (で説明されているオーディオ データを[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)または[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)構造)。

-   オーディオのストリームの待ち時間を減らすための Windows Vista で利用できるスケジュール サポートの強化を使用できます。

機能強化を活用するために、オーディオ デバイスの場合オーディオで提供される、Windows オーディオ デバイスは、再生やストリーミング中にドライバー ソフトウェアが、ほとんどまたはまったくなしオーディオ データをキャプチャすることである必要があります。 WaveRT ポート ドライバーを使用する適切にデザインされたオーディオ デバイス オーディオ ストリームが入った時刻からドライバー ソフトウェアからのほとんどまたはまったくのヘルプが必要です、*実行*がその状態から終了までの状態します。

WaveRT ポート ドライバーの主なクライアントは、共有モードで実行されているオーディオ エンジンです。 Windows Vista のオーディオ エンジンの詳細については、次を参照してください。、 [、Windows Vista のオーディオ エンジンが調べる](exploring-the-windows-vista-audio-engine.md)トピック。

 

 





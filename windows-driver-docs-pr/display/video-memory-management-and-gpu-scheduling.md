---
title: ビデオ メモリ管理と GPU がスケジュール設定
description: ビデオ メモリ管理と GPU がスケジュール設定
ms.assetid: 33fc9f0a-57ed-479f-9cb0-3f3f540047ab
keywords:
- ドライバー モデル WDK Windows Vista では、ビデオ メモリ管理の表示します。
- Windows Vista ディスプレイ ドライバー モデル WDK、ビデオ メモリ管理
- ビデオ メモリ管理 WDK の表示
- GPU スケジューリング WDK の表示
- ドライバー モデル WDK Windows Vista では、表示する GPU がスケジュール設定
- Windows Vista のディスプレイ ドライバー モデル WDK、GPU がスケジュール設定
- ユーザー モード ドライバー WDK Windows Vista では、ビデオ メモリ管理の表示します。
- ミニポート ドライバー WDK の表示、ビデオ メモリ管理
- ユーザー モードのディスプレイ ドライバー WDK Windows Vista では、GPU がスケジュール設定
- ミニポート ドライバー WDK を表示する GPU がスケジュール設定
ms.date: 01/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 986f7e00453d6cefab58fa6759f62801c1bf2acc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529159"
---
# <a name="video-memory-management-and-gpu-scheduling"></a>ビデオ メモリ管理と GPU がスケジュール設定


## <span id="ddk_video_memory_management_and_gpu_scheduling_gg"></span><span id="DDK_VIDEO_MEMORY_MANAGEMENT_AND_GPU_SCHEDULING_GG"></span>

ビデオ メモリ マネージャーは現在、次の OS ファイルで実装されます。 

* dxgkrnl.sys
* dxgmms1.sys
* dxgmms2.sys

これらのファイルとして使用できるのみ、OS のインストール、および個別のダウンロードとして使用できないの一部です。 これらのファイルは、それに伴うその他の OS ファイルと連動するのみ設計されています。 これらのファイルの間で一致していないバージョンは、Microsoft でサポートされていないと、日常的に動作しません。

次のセクションでは、ビデオ メモリ管理とグラフィックス処理ユニット (GPU) のモデルのスケジュール設定について説明します。

[メモリのセグメントの処理](handling-memory-segments.md)

[コマンドおよび DMA バッファー処理](handling-command-and-dma-buffers.md)

[GDI のハードウェア高速化](gdi-hardware-acceleration.md)

[ビデオ メモリのプランと再利用](video-memory-offer-and-reclaim.md)

[GPU のプリエンプション](gpu-preemption.md)

 

 






---
title: チューニング可能な信号までスキャン
description: チューニング可能な信号までスキャン
ms.assetid: cc934079-5d00-42e0-a024-1b7548bb88e4
keywords:
- シグナルの WDK ビデオ キャプチャのスキャン
- 調整可能な信号を WDK のビデオのキャプチャのスキャン
- 調整可能な信号 WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc89b92cfb080464f8f3a4722d477fe6fbe35a47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358423"
---
# <a name="scanning-to-tunable-signals"></a>チューニング可能な信号までスキャン


**このセクションでは、Microsoft Windows Vista 以降のオペレーティング システムにのみ適用されます。**

シグナルのスキャンは、ケーブルまたはアンテナのシステム上の頻度の値の範囲に沿ってにブロードキャストされる (上下) は、次の調整可能なシグナルにロックのプロセスです。 オペレーティング システム以前、Windows Vista よりも信号ソフトウェアによって主駆動型は、スキャンの (、 *KsTvTune.ax*モジュール) のブロードキャストのスペクトルの頻度に基づくスキャンではなく、チャネルの既知のマップのスキャンに基づいています。 Windows Vista で実行されている AVStream ミニドライバーが Windows の新しい Vista プロパティを通じて信号スキャン機能を報告する場合、 [PROPSETID\_チューナー](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-tuner)プロパティ セットには、チューナーのフィルター (*KsTvTune.ax*) 上記のアプリケーションは、それらの機能を使用して、スキャンの用とします。 ドライバーは、新しい頻度に基づくスキャン機能をサポートしていない場合*KsTvTune.ax*前者チャネルに基づくスキャンの機能にフォールバックします。

使用して、新しい頻度に基づくスキャン機能を処理できるチューナー フィルターと、AVStream ミニドライバーを[スキャン アルゴリズムのハードウェアによる](hardware-assisted-scanning-algorithm.md)。

スキャンが完了したら、ミニドライバーは、イベント ハンドルを通知する必要があります。 イベントの操作フローについては、次を参照してください。[イベント メカニズムと Flow](event-mechanism-and-flow.md)します。

新しい頻度に基づくスキャン機能をサポートするために、ミニドライバーは、次の一覧で、必要なプロパティを実装し、必要に応じて残りのプロパティとイベントを実装する必要があります。

[**KSPROPERTY\_チューナー\_スキャン\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps) (必須)

[**KSPROPERTY\_チューナー\_スキャン\_状態**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status) (省略可能)

[**KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps) (省略可能)

[**KSEVENT\_チューナー\_開始\_スキャン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan) (省略可能)

 

 





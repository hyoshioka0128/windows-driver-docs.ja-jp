---
title: 調整可能な信号をスキャン
description: 調整可能な信号をスキャン
ms.assetid: cc934079-5d00-42e0-a024-1b7548bb88e4
keywords:
- シグナルの WDK ビデオ キャプチャのスキャン
- 調整可能な信号を WDK のビデオのキャプチャのスキャン
- 調整可能な信号 WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad799f32d8ea09db75f01d8565171aafcdbc3777
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537155"
---
# <a name="scanning-to-tunable-signals"></a>調整可能な信号をスキャン


**このセクションでは、Microsoft Windows Vista 以降のオペレーティング システムにのみ適用されます。**

シグナルのスキャンは、ケーブルまたはアンテナのシステム上の頻度の値の範囲に沿ってにブロードキャストされる (上下) は、次の調整可能なシグナルにロックのプロセスです。 オペレーティング システム以前、Windows Vista よりも信号ソフトウェアによって主駆動型は、スキャンの (、 *KsTvTune.ax*モジュール) のブロードキャストのスペクトルの頻度に基づくスキャンではなく、チャネルの既知のマップのスキャンに基づいています。 Windows Vista で実行されている AVStream ミニドライバーが Windows の新しい Vista プロパティを通じて信号スキャン機能を報告する場合、 [PROPSETID\_チューナー](https://msdn.microsoft.com/library/windows/hardware/ff567800)プロパティ セットには、チューナーのフィルター (*KsTvTune.ax*) 上記のアプリケーションは、それらの機能を使用して、スキャンの用とします。 ドライバーは、新しい頻度に基づくスキャン機能をサポートしていない場合*KsTvTune.ax*前者チャネルに基づくスキャンの機能にフォールバックします。

使用して、新しい頻度に基づくスキャン機能を処理できるチューナー フィルターと、AVStream ミニドライバーを[スキャン アルゴリズムのハードウェアによる](hardware-assisted-scanning-algorithm.md)。

スキャンが完了したら、ミニドライバーは、イベント ハンドルを通知する必要があります。 イベントの操作フローについては、次を参照してください。[イベント メカニズムと Flow](event-mechanism-and-flow.md)します。

新しい頻度に基づくスキャン機能をサポートするために、ミニドライバーは、次の一覧で、必要なプロパティを実装し、必要に応じて残りのプロパティとイベントを実装する必要があります。

[**KSPROPERTY\_チューナー\_スキャン\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff565887) (必須)

[**KSPROPERTY\_チューナー\_スキャン\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff565893) (省略可能)

[**KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff565881) (省略可能)

[**KSEVENT\_チューナー\_開始\_スキャン**](https://msdn.microsoft.com/library/windows/hardware/ff561898) (省略可能)

 

 





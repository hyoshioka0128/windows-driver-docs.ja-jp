---
title: データ コピーの回避
description: データ コピーの回避
ms.assetid: bf4dab5e-5800-4888-af96-68a152ac5e39
keywords:
- データ コピーの WDK オーディオ
- オーディオ データのコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf46bb249d2b66574910651a6c88f0cb491f197
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333912"
---
# <a name="avoiding-data-copying"></a>データ コピーの回避


## <span id="avoiding_data_copying"></span><span id="AVOIDING_DATA_COPYING"></span>


不要なデータのコピーを回避するためにオーディオ ハードウェアの設計では、ドライバーのパフォーマンスを向上できます。

True スキャッター/ギャザー DMA を実行するためにハードウェアを実装することによって、ハードウェアを管理する WavePci ミニポート ドライバーを記述することで、最適な結果を実現できます。 デバイスに直接アクセスできますデータ バッファーの再生、または空のレコードのバッファー システム メモリ内にある任意の場所。 これにより、多くの不要なソフトウェアの操作と時間のかかるデータのコピーがなくなります。

WaveCyclic デバイスを設計する場合はただし、そのハードウェアのバッファーをシステム メモリとして直接アクセスできるようにして、パフォーマンスを向上できます。 これにより、システム メモリ内で、中間バッファーからのデータのコピーのオーバーヘッドがなくなります。

また、デバイスは、標準の WDM オーディオ形式と互換性がない順序付けするチャネルを持つオーディオ形式を必要とする場合、ドライバーは、ハードウェアが処理できる前に、中間のバッファーでオーディオの各フレームのインプレース変換を実行する必要があります。 これにより、パフォーマンスが低下することができます。 詳細については、複数のチャネルのオーディオ データおよび WAVE ファイルでというタイトルのホワイト ペーパーを参照してください、[オーディオ テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8751)web サイト。

 

 





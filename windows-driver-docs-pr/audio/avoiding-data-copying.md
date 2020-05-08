---
title: データ コピーの回避
description: データ コピーの回避
ms.assetid: bf4dab5e-5800-4888-af96-68a152ac5e39
keywords:
- WDK オーディオのデータコピー
- オーディオデータのコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce8de70e44e04be690ed464b3e638ee0ebfc9fca
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925617"
---
# <a name="avoiding-data-copying"></a>データ コピーの回避

## <span id="avoiding_data_copying"></span><span id="AVOIDING_DATA_COPYING"></span>

不要なデータコピーを回避するためにオーディオハードウェアを設計することで、ドライバーのパフォーマンスを向上させることができます。

最適な結果を得るには、ハードウェアを実装して、真のスキャッター/ギャザー DMA を実行し、ハードウェアを管理するための WavePci ミニポートドライバーを作成します。 デバイスは、システムメモリに配置されているすべての場所で、再生データバッファーまたは空のレコードバッファーに直接アクセスできます。 これにより、不必要なソフトウェアの介入や、時間のかかるデータのコピーが不要になります。

ただし、WaveCyclic デバイスを設計する場合は、ハードウェアバッファーをシステムメモリとして直接アクセスできるようにすることで、パフォーマンスを向上させることができます。 これにより、システムメモリ内の中間バッファーからデータをコピーするオーバーヘッドがなくなります。

また、デバイスが、標準の WDM オーディオ形式と互換性のないチャネルの順序を持つオーディオ形式を必要とする場合、ドライバーは、ハードウェアが処理できるようにする前に、中間バッファー内の各オーディオフレームのインプレース変換を実行する必要がある場合があります。 これにより、パフォーマンスが低下する可能性があります。 詳細については、「[複数チャネルのオーディオデータと WAVE ファイル](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653308(v=vs.85))」を参照してください。

---
title: Pscript 固有のカスタマイズされたレンダリング
description: Pscript 固有のカスタマイズされたレンダリング
ms.assetid: e984f0f0-1435-4cfd-9a99-297f6a9521f5
keywords:
- プラグインの WDK の印刷、Pscript5 のレンダリング
- 印刷、Pscript WDK レンダリングをカスタマイズします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebca7cc64b90826bf20a286b4f188a2b4e12a8a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356001"
---
# <a name="pscript-specific-customized-rendering"></a>Pscript 固有のカスタマイズされたレンダリング





Pscript5 はにより Pscript5 ドライバーはプリンター デバイスに送信するデータ ストリームに Postscript コマンドを挿入するカスタマイズされたコードをデバイスに固有です。 実装するプラグインのレンダリングを指定する必要がありますこの種類のカスタマイズ コードを提供する場合、 [ **IPrintOemPS::Command** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-command)メソッド。

Pscript5 呼び出し、 **IPrintOemPS::Command**で印刷ジョブのデータ ストリーム内のポイントのさまざまな方法です。 関数の引数の 1 つには、データ ストリームの現在のポイントを表すインデックス値を指定します。 関数が呼び出されるたびには、インデックス値を確認でき、かどうか追加ストリームにデータを提供するか。

 

 





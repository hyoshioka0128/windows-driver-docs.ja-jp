---
title: Pscript に固有のレンダリングをカスタマイズします。
description: Pscript に固有のレンダリングをカスタマイズします。
ms.assetid: e984f0f0-1435-4cfd-9a99-297f6a9521f5
keywords:
- プラグインの WDK の印刷、Pscript5 のレンダリング
- 印刷、Pscript WDK レンダリングをカスタマイズします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a41d7be6c9277e895ba32d029c6218fbf7218305
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549578"
---
# <a name="pscript-specific-customized-rendering"></a>Pscript に固有のレンダリングをカスタマイズします。





Pscript5 はにより Pscript5 ドライバーはプリンター デバイスに送信するデータ ストリームに Postscript コマンドを挿入するカスタマイズされたコードをデバイスに固有です。 実装するプラグインのレンダリングを指定する必要がありますこの種類のカスタマイズ コードを提供する場合、 [ **IPrintOemPS::Command** ](https://msdn.microsoft.com/library/windows/hardware/ff553199)メソッド。

Pscript5 呼び出し、 **IPrintOemPS::Command**で印刷ジョブのデータ ストリーム内のポイントのさまざまな方法です。 関数の引数の 1 つには、データ ストリームの現在のポイントを表すインデックス値を指定します。 関数が呼び出されるたびには、インデックス値を確認でき、かどうか追加ストリームにデータを提供するか。

 

 





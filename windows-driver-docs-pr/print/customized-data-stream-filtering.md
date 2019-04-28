---
title: カスタマイズされたデータ ストリーム フィルター処理
description: カスタマイズされたデータ ストリーム フィルター処理
ms.assetid: 768d4b95-4d8d-4460-9a8c-c80785f7f799
keywords:
- Unidrv、データ ストリームのフィルター処理
- データ ストリームのフィルター処理の WDK Unidrv
- カスタマイズされたデータ ストリームの WDK Unidrv をフィルター処理
- WDK Unidrv をフィルター処理
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a6c4f2681062f9f3cbb76b03765c8ace093e1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365550"
---
# <a name="customized-data-stream-filtering"></a>カスタマイズされたデータ ストリーム フィルター処理





Unidrv は、スプールが前に、イメージ データの最後の後処理を実行するコードをカスタマイズできます。 このような処理を隣接するドット、またはフィルター処理操作 Unidrv が提供されないその他のデータを削除するから構成されます。

イメージ データの最後の後処理を実行する提供プラグイン レンダリング実装する、 [ **IPrintOemUni::FilterGraphics** ](https://msdn.microsoft.com/library/windows/hardware/ff554252)メソッド。

[ **IPrintOemUni::FilterGraphics** ](https://msdn.microsoft.com/library/windows/hardware/ff554252)メソッドは入力としてスキャン ラインのデータを受け取ります。 メソッドが、データを処理し、呼び出すことによって、印刷スプーラーを送信する必要があります[ **IPrintOemDriverUni::DrvWriteSpoolBuf**](https://msdn.microsoft.com/library/windows/hardware/ff553138)します。 場合、 **IPrintOemUni::FilterGraphics**メソッドを実装する、Unidrv はプリンター データをスプールしていません。 代わりに、すべてのデータ ブロックを送信、 **IPrintOemUni::FilterGraphics**メソッド。

 

 





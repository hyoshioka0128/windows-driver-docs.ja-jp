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
ms.openlocfilehash: dc6bf2541d2341e1233771285971c37155496550
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372408"
---
# <a name="customized-data-stream-filtering"></a>カスタマイズされたデータ ストリーム フィルター処理





Unidrv は、スプールが前に、イメージ データの最後の後処理を実行するコードをカスタマイズできます。 このような処理を隣接するドット、またはフィルター処理操作 Unidrv が提供されないその他のデータを削除するから構成されます。

イメージ データの最後の後処理を実行する提供プラグイン レンダリング実装する、 [ **IPrintOemUni::FilterGraphics** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)メソッド。

[ **IPrintOemUni::FilterGraphics** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)メソッドは入力としてスキャン ラインのデータを受け取ります。 メソッドが、データを処理し、呼び出すことによって、印刷スプーラーを送信する必要があります[ **IPrintOemDriverUni::DrvWriteSpoolBuf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)します。 場合、 **IPrintOemUni::FilterGraphics**メソッドを実装する、Unidrv はプリンター データをスプールしていません。 代わりに、すべてのデータ ブロックを送信、 **IPrintOemUni::FilterGraphics**メソッド。

 

 





---
title: カスタマイズされたデータストリームのフィルター処理
description: カスタマイズされたデータストリームのフィルター処理
ms.assetid: 768d4b95-4d8d-4460-9a8c-c80785f7f799
keywords:
- Unidrv、データストリームのフィルター処理
- データストリームフィルター WDK Unidrv
- カスタマイズされたデータストリームフィルター WDK Unidrv
- WDK Unidrv のフィルター処理
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac5b6962c59394030af7f38b864ff237432bccd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837979"
---
# <a name="customized-data-stream-filtering"></a>カスタマイズされたデータストリームのフィルター処理





Unidrv を使用すると、イメージデータをスプールする前に最終的な後処理を実行できます。 このような処理では、隣接するドットや、Unidrv が提供しないその他のデータフィルタリング操作が削除されます。

イメージデータの最終的な後処理を実行するには、 [**Iprintoemuni:: FilterGraphics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)メソッドを実装するレンダリングプラグインを提供します。

[**Iprintoemuni:: FilterGraphics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)メソッドは、スキャンラインデータを入力として受信します。 メソッドは、 [**Iprintoemdriveruni::D rvwritespoolbuf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)を呼び出すことによって、データを処理し、それを印刷スプーラに送信する必要があります。 **Iprintoemuni:: FilterGraphics**メソッドが実装されている場合、Unidrv はプリンターデータをスプールしません。 代わりに、すべてのデータブロックが**Iprintoemuni:: FilterGraphics**メソッドに送信されます。

 

 





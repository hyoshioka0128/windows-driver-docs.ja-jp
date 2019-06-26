---
title: ラスター データのフィルター処理
description: ラスター データのフィルター処理
ms.assetid: 179a2dc0-8794-4934-99b9-eb3f7900536c
keywords:
- Unidrv、ラスター データのフィルター処理
- GPD ファイル WDK Unidrv、ラスター データのフィルター処理
- 印刷の WDK ラスター データのフィルター処理
- ラスター データの WDK Unidrv をフィルター処理
- 処理後のスキャン ラインのデータ ストリームの WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f5a25a6a9207d8f2af551f8c0dcc481f424b8d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382567"
---
# <a name="filtering-raster-data"></a>ラスター データのフィルター処理





スプールが前に、スキャン ラインのデータ ストリームのカスタマイズされた処理の後を指定する場合は、これを行う実装することによって、 [ **IPrintOemUni::FilterGraphics** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)メソッドで、 [プラグインのレンダリング](rendering-plug-ins.md)します。 この Unidrv 機能に関連付けられている GPD ファイルのエントリがありません。

詳細については、次を参照してください。[データ Stream のフィルター処理をカスタマイズ](customized-data-stream-filtering.md)します。

 

 





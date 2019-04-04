---
title: ラスターのデータのフィルター処理
description: ラスターのデータのフィルター処理
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
ms.openlocfilehash: 0200779d2e6f72317be85889cbcc40cb06fe8611
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552164"
---
# <a name="filtering-raster-data"></a>ラスターのデータのフィルター処理





スプールが前に、スキャン ラインのデータ ストリームのカスタマイズされた処理の後を指定する場合は、これを行う実装することによって、 [ **IPrintOemUni::FilterGraphics** ](https://msdn.microsoft.com/library/windows/hardware/ff554252)メソッドで、 [プラグインのレンダリング](rendering-plug-ins.md)します。 この Unidrv 機能に関連付けられている GPD ファイルのエントリがありません。

詳細については、[データ Stream のフィルター処理をカスタマイズ](customized-data-stream-filtering.md)を参照してください。

 

 





---
title: カスタマイズされたデータ ストリーム圧縮
description: カスタマイズされたデータ ストリーム圧縮
ms.assetid: 7e42f3c7-c833-49ee-976b-ed32b921af95
keywords:
- Unidrv、データ ストリームの圧縮
- データ ストリーム圧縮 WDK Unidrv
- カスタマイズされたデータ ストリームの圧縮 WDK Unidrv
- 圧縮データ ストリームの WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0c21b363a5e646e21b429f55a9eaf07ed828b4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365536"
---
# <a name="customized-data-stream-compression"></a>カスタマイズされたデータ ストリーム圧縮





Unidrv カスタマイズ コードを使用してデータの圧縮操作を実行することができます。 カスタマイズされた圧縮操作を実行するには、次の手順を実行します。

1.  実装するプラグインのレンダリングを提供、 [ **IPrintOemUni::Compression** ](https://msdn.microsoft.com/library/windows/hardware/ff554224)メソッド。

2.  プリンターの CmdEnableOEMComp コマンドの入力を含める*GPD*ファイル。

IPrintOemUni::Compression メソッドは、スキャン ラインのデータを入力として受け取ります。 メソッドは、データを圧縮し、Unidrv に結果を返す必要があります。 **CmdEnableOEMComp**コマンドのエントリをプリンターが圧縮されたデータを受け入れるように、プリンターに送信する必要がありますのコマンドを指定します。 プリンターに送信するのには、各スキャン ライン Unidrv のスキャン ラインのデータを圧縮する IPrintOemUni::Compression を呼び出し。 次に、これが唯一の圧縮方法である場合は、Unidrv プリンターに送信で指定されたコマンド、 **CmdEnableOEMComp**コマンド エントリ、圧縮されたデータが続きます。

プリンター ミニドライバーに Unidrv でサポートされている圧縮方法を有効にも GPD エントリが含まれている場合、Unidrv は各スキャン ラインの場合は、各圧縮アルゴリズムを試行し、最適な結果を生成するアルゴリズムを選択します。 Unidrv の圧縮機能の詳細については、次を参照してください。[ラスター データの圧縮](compressing-raster-data.md)します。

1 つだけのカスタマイズされた圧縮方法は、一度に 1 つ有効にできます。

 

 





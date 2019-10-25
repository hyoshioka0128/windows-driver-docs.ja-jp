---
title: カスタマイズされたデータ ストリーム圧縮
description: カスタマイズされたデータ ストリーム圧縮
ms.assetid: 7e42f3c7-c833-49ee-976b-ed32b921af95
keywords:
- Unidrv、データストリームの圧縮
- データストリームの圧縮 WDK Unidrv
- カスタマイズされたデータストリームの圧縮 WDK Unidrv
- 圧縮されたデータストリーム WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93964f4a0185ed4c8068241db74424c4d04d7fb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838007"
---
# <a name="customized-data-stream-compression"></a>カスタマイズされたデータ ストリーム圧縮





Unidrv では、カスタマイズされたコードを使用してデータ圧縮操作を実行できます。 カスタマイズした圧縮操作を実行するには、次の手順を実行します。

1.  [**Iprintoemuni:: Compression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression)メソッドを実装するレンダリングプラグインを提供します。

2.  Cmデ Ableoemcomp コマンドエントリをプリンターの*GPD*ファイルに含めます。

IPrintOemUni:: Compression メソッドは、スキャンラインデータを入力として受信します。 メソッドは、データを圧縮してから、結果を Unidrv に返す必要があります。 **Cm、Ableoemcomp**コマンドエントリは、プリンターが圧縮データを受け入れることができるように、プリンターに送信する必要があるコマンドを指定します。 Unidrv は、プリンターに送信される各スキャンラインに対して IPrintOemUni:: Compression を呼び出してスキャンラインデータを圧縮します。 これが使用可能な唯一の圧縮方法である場合、Unidrv は、 **Cmカンプ Ableoemcomp**コマンドエントリによって指定されたコマンドをプリンターに送信し、その後に圧縮データを送信します。

ミニドライバーによってサポートされる圧縮方法を有効にする GPD エントリがプリンターに含まれている場合、Unidrv はスキャンラインごとに各圧縮アルゴリズムを試行し、最適な結果を生成するアルゴリズムを選択します。 Unidrv の圧縮機能の詳細については、「[ラスターデータの圧縮](compressing-raster-data.md)」を参照してください。

カスタマイズされた圧縮方法は一度に1つしか有効にできません。

 

 





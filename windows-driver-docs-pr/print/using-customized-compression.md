---
title: カスタマイズされた圧縮の使用
description: カスタマイズされた圧縮の使用
ms.assetid: 959c0015-4b31-4790-8d2b-26d6acc19ac7
keywords:
- ラスターデータ圧縮 WDK Unidrv
- ラスターデータの圧縮 WDK Unidrv
- カスタマイズされたラスターデータ圧縮 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 483abc98a6d583288bca3b31f0236ef77af9afd5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844200"
---
# <a name="using-customized-compression"></a>カスタマイズされた圧縮の使用





カスタマイズされた圧縮アルゴリズムを提供する場合は、Cmデ Ableoemcomp コマンドエントリをインクルードして、アルゴリズムを有効にするコマンドを指定します。 プリンターで圧縮を無効にできる場合は、必要に応じて CmdDisableCompression エントリを追加して、圧縮を無効にするコマンドを指定することができます。 [**Iprintoemuni:: Compression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression)メソッドを実装する[レンダリングプラグイン](rendering-plug-ins.md)も用意する必要があります。

カスタマイズした圧縮アルゴリズムを提供する場合は、Unidrv でサポートされているアルゴリズムの使用を有効にすることもできます。 各スキャンラインで、Unidrv は各圧縮アルゴリズムを試行し、最も圧縮された結果を生成するアルゴリズムを選択します。 (Unidrv でサポートされているアルゴリズムの詳細については、「 [unidrv がサポートさ](using-unidrv-supported-compression.md)れている圧縮の使用」を参照してください)。Unidrv が最適なアルゴリズムを見つけたら、スキャンラインデータを圧縮します。 次に、適切なコマンドエントリによって指定されたコマンドをプリンターに送信し、その後に圧縮データを入力します。

CmCmdDisableCompression のエントリの詳細については、「[ラスターデータ圧縮コマンド](raster-data-compression-commands.md)」を参照してください。

カスタマイズした圧縮の詳細については、「カスタマイズされた[データストリームの圧縮](customized-data-stream-compression.md)」を参照してください。

 

 





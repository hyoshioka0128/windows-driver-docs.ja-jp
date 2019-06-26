---
title: カスタマイズされた圧縮の使用
description: カスタマイズされた圧縮の使用
ms.assetid: 959c0015-4b31-4790-8d2b-26d6acc19ac7
keywords:
- データ圧縮のラスター WDK Unidrv
- ラスター データ WDK Unidrv を圧縮します。
- カスタマイズされたラスター データ圧縮 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4483c88b9d4958e3040d1e82fce33ef01686c898
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362740"
---
# <a name="using-customized-compression"></a>カスタマイズされた圧縮の使用





カスタマイズされた圧縮アルゴリズムを指定する場合は、コマンドにより、アルゴリズムを指定する CmdEnableOEMComp コマンドの入力が含まれます。 プリンターでは、圧縮を無効にする場合は、圧縮を無効にするコマンドを指定する CmdDisableCompression エントリを必要に応じて含めることができます。 指定することも必要があります、[プラグインでレンダリング](rendering-plug-ins.md)を実装する、 [ **IPrintOemUni::Compression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-compression)メソッド。

カスタマイズされた圧縮アルゴリズムを指定する場合も、Unidrv でサポートされているアルゴリズムの使用を有効にできます。 各スキャン ライン Unidrv 各圧縮アルゴリズムを試行し、最も圧縮の結果を生成するアルゴリズムを選択します。 (Unidrv でサポートされているアルゴリズムについては、次を参照してください[Using Unidrv-Supported 圧縮](using-unidrv-supported-compression.md)。)。Unidrv には、最適なアルゴリズムが検出されると、スキャン ラインのデータを圧縮します。 その後、圧縮されたデータの後に、適切なコマンドの入力で指定されたコマンドをプリンターに送信します。

CmdEnableOEMComp と CmdDisableCompression エントリの詳細については、次を参照してください。[ラスター データ圧縮コマンド](raster-data-compression-commands.md)します。

カスタマイズされた圧縮の詳細については、次を参照してください。[カスタマイズされたデータ Stream 圧縮](customized-data-stream-compression.md)します。

 

 





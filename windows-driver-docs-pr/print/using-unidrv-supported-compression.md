---
title: Unidrv でサポートされている圧縮の使用
description: Unidrv でサポートされている圧縮の使用
ms.assetid: feda6898-da2c-403f-a159-1423891f3dd5
keywords:
- データ圧縮のラスター WDK Unidrv
- ラスター データ WDK Unidrv を圧縮します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ba602f74762c59bcc83e4bab97bc033f93ab6ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579261"
---
# <a name="using-unidrv-supported-compression"></a>Unidrv でサポートされている圧縮の使用





CmdEnableTIFF4 コマンドの入力を GPD ファイルに含める場合、Unidrv は TIFF 4.0 の圧縮を使用します。

CmdEnableDRC コマンドの入力を GPD ファイルに含める場合、Unidrv は民主共和国の圧縮を使用します。

CmdEnableFE を含める場合\_RLE コマンドが Unidrv、GPD ファイル内のエントリは FE RLE 圧縮を使用します。

プリンターでは、これらの圧縮方法の 1 つ以上をサポートする場合は、サポートされている各メソッドのコマンドの入力を含めることができます。 各スキャン ライン Unidrv 各圧縮アルゴリズムを試行し、最も圧縮の結果を生成するアルゴリズムを選択します。 (含めることも、カスタマイズされたアルゴリズム。 参照してください[圧縮を使用してカスタマイズされた](using-customized-compression.md))。Unidrv には、最適なアルゴリズムが検出されると、スキャン ラインのデータを圧縮します。 その後、圧縮されたデータの後に、適切なコマンドの入力で指定されたコマンドをプリンターに送信します。

CmdDisableCompression コマンドの入力を指定する場合、使用可能な圧縮方法に関係なく Unidrv 一時的に無効を圧縮してより小さい圧縮されていないデータ ブロックを見つけたときに、圧縮されたデータを送信します。

不要な計算を制限するにはないで有効に圧縮方法 (そのコマンドの入力を指定する) 場合は、メソッドが使用可能な結果を生成する可能性があります。

ほとんどのプリンターには、圧縮されたデータの受信を有効またはデータ ブロックの外部でのコマンド文字列を送信することによって無効にすることができます。 CmdEnableTIFF4、CmdEnableDRC、CmdEnableFE を指定すると\_RLE、CmdDisableCompression エントリと、これらのプリンター用には、コマンド文字列が含まれます。 します。

一部のプリンター (プリンターが通常東アジア) CmdSendBlockData コマンドを使用して、圧縮の選択コマンドが送信されるラスター データに埋め込まれます。 CmdEnableTIFF4、CmdEnableDRC、または CmdEnableFE を指定すると\_RLE エントリは、これらのプリンターをコマンド文字列を含めないでください。 代わりに、コマンドを表すための空の引用符で囲まれた文字列を指定します。 これにより、Unidrv 圧縮を使用するが、有効にする別のコマンドを送信するように指示します。 これらのプリンターの 1 つだけの圧縮アルゴリズムを使用していることができます。 Unidrv ここで圧縮をオフにするための方法がないために、CmdDisableCompression エントリは必要ありません。

CmdEnableTIFF4、CmdEnableDRC、CmdEnableFE の詳細については\_RLE、CmdDisableCompression のエントリを参照してくださいと[ラスター データ圧縮コマンド](raster-data-compression-commands.md)します。

CmdSendBlockData の詳細については、次を参照してください。[ラスター データ出力コマンド](raster-data-emission-commands.md)します。

 

 





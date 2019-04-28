---
title: カスタマイズされた色フォーマット
description: カスタマイズされた色フォーマット
ms.assetid: 309d33e8-6338-4c32-8e03-d6cbf3371e16
keywords:
- Unidrv、色の形式
- 色は WDK Unidrv を書式設定します。
- カスタマイズした色が WDK Unidrv を書式設定します。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2940f05a625320c5effb4e8dd87441d3d6ca27
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365528"
---
# <a name="customized-color-formats"></a>カスタマイズされた色フォーマット





Unidrv 内に示されているいくつかの色形式をサポートしている[色形式の処理](handling-color-formats.md)します。 これらの形式は、Unidrv は、GDI ビットマップをプリンターに送信する前に、正しい形式に変換します。 実装するプラグインのレンダリングを提供する必要があります、プリンターが Unidrv でサポートされていない形式を受け入れる場合、 [ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)メソッド。

実装する場合[ **IPrintOemUni::ImageProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff554261)かどうかには、ユーザーが処理できない Unidrv 色形式 (返さオプション) を選択し、GDI ビットマップ データのバッファーを毎回とは、印刷の準備Unidrv は、メソッドを呼び出すし、ビットマップのアドレスを入力引数として渡します。 メソッドがビットマップを指定した形式に変換する必要がありますで実行[カスタマイズ ハーフトーン](customized-halftoning.md)操作に応じて、および呼び出し、 [ **IPrintOemDriverUni::DrvWriteSpoolBuf** ](https://msdn.microsoft.com/library/windows/hardware/ff553138)印刷スプーラーに変更されたビットマップを送信する方法。 呼び出す必要があります、 [ **IPrintOemDriverUni::DrvXMoveTo** ](https://msdn.microsoft.com/library/windows/hardware/ff553141)と[ **IPrintOemDriverUni::DrvYMoveTo** ](https://msdn.microsoft.com/library/windows/hardware/ff553144)カーソルを更新する方法位置。 これらの操作の詳細については、の説明を参照してください。 **IPrintOemUni::ImageProcessing**します。

レンダリングのプラグインを実装する場合[ **IPrintOemUni::ImageProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff554261)も実装できます[ **IPrintOemUni::MemoryUsage**](https://msdn.microsoft.com/library/windows/hardware/ff554264)します。

 

 





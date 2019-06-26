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
ms.openlocfilehash: f735c106c89c4f02920f9be64fd2dbf79ae6b13a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372418"
---
# <a name="customized-color-formats"></a>カスタマイズされた色フォーマット





Unidrv 内に示されているいくつかの色形式をサポートしている[色形式の処理](handling-color-formats.md)します。 これらの形式は、Unidrv は、GDI ビットマップをプリンターに送信する前に、正しい形式に変換します。 実装するプラグインのレンダリングを提供する必要があります、プリンターが Unidrv でサポートされていない形式を受け入れる場合、 [ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッド。

実装する場合[ **IPrintOemUni::ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)かどうかには、ユーザーが処理できない Unidrv 色形式 (返さオプション) を選択し、GDI ビットマップ データのバッファーを毎回とは、印刷の準備Unidrv は、メソッドを呼び出すし、ビットマップのアドレスを入力引数として渡します。 メソッドがビットマップを指定した形式に変換する必要がありますで実行[カスタマイズ ハーフトーン](customized-halftoning.md)操作に応じて、および呼び出し、 [ **IPrintOemDriverUni::DrvWriteSpoolBuf** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)印刷スプーラーに変更されたビットマップを送信する方法。 呼び出す必要があります、 [ **IPrintOemDriverUni::DrvXMoveTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto)と[ **IPrintOemDriverUni::DrvYMoveTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto)カーソルを更新する方法位置。 これらの操作の詳細については、の説明を参照してください。 **IPrintOemUni::ImageProcessing**します。

レンダリングのプラグインを実装する場合[ **IPrintOemUni::ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)も実装できます[ **IPrintOemUni::MemoryUsage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)します。

 

 





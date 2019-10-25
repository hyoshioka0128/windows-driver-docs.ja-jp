---
title: カスタマイズされた色フォーマット
description: カスタマイズされた色フォーマット
ms.assetid: 309d33e8-6338-4c32-8e03-d6cbf3371e16
keywords:
- Unidrv、色の形式
- WDK Unidrv の色形式
- カスタマイズされた色の形式 WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f2125aa3e39e8a9382d8b01b65e378f08d1c5bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842846"
---
# <a name="customized-color-formats"></a>カスタマイズされた色フォーマット





Unidrv は、[色の書式を処理](handling-color-formats.md)する際に一覧表示されるいくつかの色形式をサポートしています。 これらの形式では、Unidrv は GDI ビットマップをプリンターに送信する前に正しい形式に変換します。 プリンターが Unidrv でサポートされていない形式を受け入れる場合は、 [**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドを実装するレンダリングプラグインを指定する必要があります。

[**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)を実装し、ユーザーが Unidrv で処理できないカラーフォーマット (ColorMode オプション) を選択した場合、次に、GDI ビットマップデータのバッファーが印刷できる状態になるたびに、unidrv はメソッドを呼び出し、ビットマップのアドレスを渡します。入力引数として指定します。 メソッドはビットマップを指定された形式に変換し、必要に応じて[カスタムのハーフトーン](customized-halftoning.md)演算を実行し、 [**Iprintoemdriveruni::D rvwritespoolbuf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)メソッドを呼び出して、変更したビットマップを印刷スプーラに送信する必要があります。 また、 [**Iprintoemdriveruni::D rvXMoveTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto)および[**iprintoemdriveruni::D rvymoveto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto)メソッドを呼び出して、カーソル位置を更新する必要があります。 これらの操作の詳細については、 **Iprintoemuni:: ImageProcessing**の説明を参照してください。

レンダリングプラグインが[**iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)を実装している場合は、 [**Iprintoemuni:: memoryusage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)を実装することもできます。

 

 





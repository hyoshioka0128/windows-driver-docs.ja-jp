---
title: AVStream DMA サービス
description: AVStream DMA サービス
ms.assetid: ba1c525b-26b0-4778-b58b-f4169cfb972e
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA サービス WDK AVStream
- ダイレクトメモリアクセス WDK AVStream
- キャプチャバッファー WDK AVStream
- WDK AVStream のバッファー
- AVStream DMA WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b306c6294911a4d943048d6784a7b4f7e6d00add
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840624"
---
# <a name="avstream-dma-services"></a>AVStream DMA サービス





ダイレクトメモリアクセス (DMA) を使用する AVStream ミニドライバーを開発するには、標準の DMA をユーザーモードのキャプチャバッファーに直接実行するか、一般的なバッファー DMA を実装します。

どちらの方法でも、 [**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)を呼び出すことによって、ドライバーが DMA アダプターを取得する必要があります。

 

 





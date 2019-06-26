---
title: AVStream DMA サービス
description: AVStream DMA サービス
ms.assetid: ba1c525b-26b0-4778-b58b-f4169cfb972e
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA は、WDK AVStream をサービスします。
- ダイレクト メモリ アクセスの WDK AVStream
- WDK AVStream のバッファーをキャプチャします。
- WDK AVStream のバッファー
- AVStream DMA WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d16c18fb65ac3e735f0965bdaf632f753a53263
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386694"
---
# <a name="avstream-dma-services"></a>AVStream DMA サービス





共通バッファー DMA を実装するまたはダイレクト メモリ アクセス (DMA) を使用する AVStream ミニドライバーを開発するには、ユーザー モード キャプチャ バッファーに直接標準 DMA を実行できます。

どちらの方法は、ドライバーが呼び出すことによって、DMA アダプターを取得を必要としています。 [ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)します。

 

 





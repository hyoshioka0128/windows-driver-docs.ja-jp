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
ms.openlocfilehash: 937dee14c371b241bfff8bcfd19333c6c4d9bef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390188"
---
# <a name="avstream-dma-services"></a>AVStream DMA サービス





共通バッファー DMA を実装するまたはダイレクト メモリ アクセス (DMA) を使用する AVStream ミニドライバーを開発するには、ユーザー モード キャプチャ バッファーに直接標準 DMA を実行できます。

どちらの方法は、ドライバーが呼び出すことによって、DMA アダプターを取得を必要としています。 [ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)します。

 

 





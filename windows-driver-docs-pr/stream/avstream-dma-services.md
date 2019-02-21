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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552821"
---
# <a name="avstream-dma-services"></a>AVStream DMA サービス





共通バッファー DMA を実装するまたはダイレクト メモリ アクセス (DMA) を使用する AVStream ミニドライバーを開発するには、ユーザー モード キャプチャ バッファーに直接標準 DMA を実行できます。

どちらの方法は、ドライバーが呼び出すことによって、DMA アダプターを取得を必要としています。 [ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)します。

 

 





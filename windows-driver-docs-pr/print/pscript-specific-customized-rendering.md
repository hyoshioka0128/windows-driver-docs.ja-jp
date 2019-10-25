---
title: Pscript 固有のカスタマイズされた表示
description: Pscript 固有のカスタマイズされた表示
ms.assetid: e984f0f0-1435-4cfd-9a99-297f6a9521f5
keywords:
- レンダリングプラグイン WDK print、Pscript5
- Pscript WDK print、カスタマイズされたレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34c1c60cae673ac499c8d7b228cc740559bf733
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840418"
---
# <a name="pscript-specific-customized-rendering"></a>Pscript 固有のカスタマイズされた表示





Pscript5 を使用すると、デバイス固有のカスタマイズされたコードで、Pscript5 ドライバーがプリンターデバイスに送信するデータストリームに Postscript コマンドを挿入できます。 この種のカスタマイズされたコードを提供する場合は、 [**IPrintOemPS:: Command**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command)メソッドを実装するレンダリングプラグインを指定する必要があります。

Pscript5 は、印刷ジョブのデータストリーム内のさまざまなポイントで**IPrintOemPS:: Command**メソッドを呼び出します。 関数の引数の1つに、データストリーム内の現在のポイントを表すインデックス値を指定します。 関数が呼び出されるたびに、インデックス値を確認し、追加のストリームデータを提供するかどうかを指定できます。

 

 





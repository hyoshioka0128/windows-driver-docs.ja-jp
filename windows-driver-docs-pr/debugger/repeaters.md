---
title: repeater
description: repeater
ms.assetid: 10f4f033-f6c1-4b4f-a35f-eadb4e15686d
keywords:
- リモート デバッグの repeater を
- repeater
- repeater, 概要
- DbEngPrx
- DbEngPrx, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f8f49369db782d1995d3e2cf92b3a077827add8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382077"
---
# <a name="repeaters"></a>repeater


## <span id="ddk_repeaters_dbg"></span><span id="DDK_REPEATERS_DBG"></span>


A *repeater*は軽量のプロキシ サーバーをコンピューターで実行し、その他の 2 つのコンピューター間でデータを中継します。 Repeater では、任意の方法でデータを処理しません。 その他の 2 台のコンピューターには、repeater; ほとんどに注意してください。ユーザーの観点からは、互いに直接接続されているかのように思えます。

その他の 2 台のコンピューターで実行されているプロセスが呼び出される、 *server*と*クライアント*します。 違いはありますありません、基本的な repeater の観点からそれらの間、サーバーが開始最初は、し、repeater、および最後に、クライアントにはほとんどの場合である点が。

Windows のツールをデバッグ パッケージには、DbEngPrx (dbengprx.exe) と呼ばれるリピータが含まれています。

このセクションの内容:

[**Repeater をアクティブ化します。**](activating-a-repeater.md)

[Repeater を使用します。](using-a-repeater.md)

[Repeater の例](repeater-examples.md)

 

 






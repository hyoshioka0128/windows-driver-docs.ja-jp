---
title: 動的生成プリンター コマンド
description: 動的生成プリンター コマンド
ms.assetid: ba395716-6906-4f23-a050-79d808ccd44b
keywords:
- Unidrv、動的に生成されたコマンド
- 動的に生成された印刷コマンド WDK Unidrv
- GPD ファイル WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2224e35dd11d04be01dd7a62edb5a6df49812f29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579234"
---
# <a name="dynamically-generated-printer-commands"></a>動的生成プリンター コマンド





毎回、Unidrv ミニドライバーのプリンター コマンド ファイルを指定する次の 2 つのメソッドのいずれかを使用できます。

-   GPD ファイルにコマンド文字列を配置します。

    GPD ファイルにコマンド文字列を配置すると Unidrv は、適切なタイミングで印刷スプーラーにコマンドを送信します。 これらのコマンド文字列には、標準的な変数は、コマンドを送信する前に評価される Unidrv を含めることができます。

-   コールバック関数を提供します。

    コールバック関数を指定する場合、Unidrv は、コマンドの送信時間であり、関数は、印刷スプーラーにコマンドを送信する場合に関数を呼び出します。 これにより、コマンド文字列を動的に生成し、プリンターに送信し、コードを含めることができます。

コマンド文字列を GPD ファイルに配置するにを含める必要があります、\*コマンドの内の Cmd 属性\*コマンドを入力します。

コマンド文字列を動的に生成するコードを提供するには、次の操作を行う必要があります。

-   実装するプラグインのレンダリングを提供、 [ **IPrintOemUni::CommandCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff554216)メソッド。

-   含める、 \*CallbackID コマンド属性と、必要に応じて、 \*Params 属性には、コマンドの内\*GPD ファイル内のエントリをコマンドします。

Unidrv プリンター コマンドを発行する準備ができたらでコマンドが指定されているかどうかを判断するミニドライバー データベースを確認します。、 \*Cmd 属性、または、 \*CallbackID 属性。 前者の場合は、Unidrv は、印刷スプーラーにコマンド文字列を送信します。 Unidrv を呼び出し、後者の場合、 **IPrintOemUni::CommandCallback**渡して、メソッド、 \*CallbackID と\*Params 引数の入力としての値します。

 

 





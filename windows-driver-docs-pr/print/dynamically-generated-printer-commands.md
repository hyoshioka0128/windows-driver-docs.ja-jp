---
title: 動的に生成されたプリンターコマンド
description: 動的に生成されたプリンターコマンド
ms.assetid: ba395716-6906-4f23-a050-79d808ccd44b
keywords:
- Unidrv、動的に生成されたコマンド
- 動的に生成された印刷コマンド WDK Unidrv
- GPD ファイル WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f2f6a7d9122ddb1565db3dc37a121497fed8d51
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841636"
---
# <a name="dynamically-generated-printer-commands"></a>動的に生成されたプリンターコマンド





Unidrv ミニドライバーのプリンターコマンドファイルを指定するたびに、次の2つの方法のいずれかを使用できます。

-   コマンド文字列を GPD ファイルに配置します。

    GPD ファイルにコマンド文字列を配置すると、適切なタイミングでコマンドが印刷スプーラに送信されます。 これらのコマンド文字列には、コマンドを送信する前に Unidrv が評価する標準変数を含めることができます。

-   コールバック関数を指定します。

    コールバック関数を指定した場合、Unidrv はコマンドの送信時に関数を呼び出し、関数はコマンドを印刷スプーラに送信します。 これにより、コマンド文字列を動的に生成し、それをプリンターに送信するコードを含めることができます。

GPD ファイルにコマンド文字列を配置するには、コマンドの \*コマンドエントリ内に \*Cmd 属性を含める必要があります。

コマンド文字列を動的に生成するコードを提供するには、次の操作を行う必要があります。

-   [**Iprintoemuni:: CommandCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)メソッドを実装するレンダリングプラグインを提供します。

-   GPD ファイルのコマンドの \*コマンドエントリ内に、\*の \*Params 属性を含めます (オプション)。

Unidrv がプリンターコマンドを発行する準備が整うと、ミニドライバーデータベースをチェックして、コマンドが \*Cmd 属性で指定されているか、または \*のの属性を使用して指定されているかどうかを確認します。 前者の場合、Unidrv はコマンド文字列を印刷スプーラに送信します。 後者の場合、Unidrv は**Iprintoemuni:: CommandCallback**メソッドを呼び出し、\*のコールバック id と \*Params の値を入力引数として渡します。

 

 





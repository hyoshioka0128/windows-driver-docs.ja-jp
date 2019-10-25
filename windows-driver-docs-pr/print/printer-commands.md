---
title: プリンター コマンド
description: プリンター コマンド
ms.assetid: 4f47ae57-cfca-4670-823e-526e2f40de82
keywords:
- Unidrv、コマンド
- GPD files WDK Unidrv、printer コマンド
- コマンド WDK Unidrv
- プリンターコマンド WDK Unidrv
- プリンターコマンド WDK Unidrv、プリンターコマンドについて
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b46b97bbb5a6dc42a8b1ad18f77dee583f6906b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824326"
---
# <a name="printer-commands"></a>プリンター コマンド





GPD 言語では、一般的に使用されるプリンター操作ごとに定義済みのコマンド名が提供されます。 また、カスタマイズされたコマンドをデバイス固有の[プリンターオプション](printer-options.md)に対して定義することもできます。

各プリンターコマンドは、次の2つの方法のいずれかで実装できます。

-   GPD ファイルには、デバイス固有のコマンド文字列を配置できます。 Unidrv は、適切なタイミングで印刷スプーラにコマンド文字列を送信します。

-   [**Iprintoemuni:: CommandCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback) COM メソッドを実装できます。これにより、コマンド文字列が動的に生成されます。 Unidrv は、スプーラにコマンドを送信する必要があるときに常にメソッドを呼び出します。 詳細については、「 [Microsoft のプリンタードライバーのカスタマイズ](customizing-microsoft-s-printer-drivers.md)」の「[動的に生成されたプリンターコマンド](dynamically-generated-printer-commands.md)」を参照してください。

次のトピックでは、GPD ファイルでプリンターコマンドを指定する方法について説明します。

[コマンド入力形式](command-entry-format.md)

[コマンド名](command-names.md)

[コマンド属性](command-attributes.md)

[コマンド文字列の形式](command-string-format.md)

[コマンドの実行順序](command-execution-order.md)

 

 





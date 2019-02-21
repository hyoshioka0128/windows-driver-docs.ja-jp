---
title: プリンター コマンド
description: プリンター コマンド
ms.assetid: 4f47ae57-cfca-4670-823e-526e2f40de82
keywords:
- Unidrv、コマンド
- GPD ファイル WDK Unidrv、プリンター コマンド
- WDK Unidrv コマンド
- プリンターの WDK Unidrv コマンドします。
- プリンターはプリンター コマンドに関する WDK の Unidrv をコマンドします。
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18de40713521aa72349c99cf97836bb3f5d9c205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527714"
---
# <a name="printer-commands"></a>プリンター コマンド





それぞれの定義済みのコマンド名は、プリンターの操作をよく使用 GPD 言語を提供します。 カスタマイズしたコマンドを定義して、デバイスに固有のさらに、[プリンター オプション](printer-options.md)します。

各プリンターのコマンドは、2 つの方法のいずれかで実装できます。

-   GPD ファイルには、デバイス固有のコマンド文字列を配置できます。 Unidrv では、適切なタイミングで印刷スプーラーにコマンド文字列を送信します。

-   実装することができます、 [ **IPrintOemUni::CommandCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff554216) COM メソッドは、コマンド文字列を動的に生成されます。 Unidrv は、スプーラーにコマンドを送信する必要があるたびに、メソッドを呼び出します。 詳細については、次を参照してください。[プリンター コマンドを動的に生成された](dynamically-generated-printer-commands.md)で[をカスタマイズする Microsoft のプリンター ドライバー](customizing-microsoft-s-printer-drivers.md)します。

次のトピックでは、GPD ファイルでプリンターのコマンドを指定する方法について説明します。

[コマンド エントリの形式](command-entry-format.md)

[コマンド名](command-names.md)

[コマンドの属性](command-attributes.md)

[コマンド文字列の形式](command-string-format.md)

[コマンドの実行順序](command-execution-order.md)

 

 





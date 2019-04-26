---
title: コマンド文字列形式
description: コマンド文字列形式
ms.assetid: 3b33b261-08c7-4441-94f5-6c9de53ae349
keywords:
- プリンターが WDK Unidrv、文字列をコマンドします。
- コマンド文字列を WDK Unidrv
- WDK Unidrv 文字列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f34b2a6588ce5d66f3557a0eed5a483fabf1954
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348091"
---
# <a name="command-string-format"></a>コマンド文字列形式





コマンド文字列を使用して、プリンターのハードウェアに Unidrv を送信する必要があるエスケープ シーケンスを指定します。 コマンド文字列は、次の要素で構成をできます。

-   次の形式の文字列を引用符で囲まれたは。

    "*ダイアログ*"

-   コマンド引数には、次の形式:

    %*ある*{*StandardVariableExpression*}

Unidrv では、コマンド文字列の最大 14 の引用符で囲まれたテキスト文字列とコマンド引数をサポートします。

たとえば、四角形の塗りつぶしの灰色の率を設定するプリンターのコマンドをよう指定可能性があります。

```cpp
*Command: CmdRectGrayFill: "<1B>*c" %d{GrayPercentage} "g2P"
```

パーセント記号を送信する (**%**)、プリンターに 2 つのパーセント記号の文字を含める (**%%**) コマンド文字列にします。 コマンド文字列の末尾にパーセント記号の場合は、としてのそれと同等の 16 進数を使用する必要があります。

**"**<em>文字列</em>  **&lt;25 25&gt;"** します。

 

 





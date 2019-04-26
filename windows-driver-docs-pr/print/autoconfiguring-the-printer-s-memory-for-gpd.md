---
title: GPD のプリンターのメモリを自動構成する
description: GPD のプリンターのメモリを自動構成する
ms.assetid: 5e8339a5-d515-4821-853e-bc6607b2d9c1
keywords:
- メモリの WDK プリンター autoconfig
- GPD は、WDK GDL 拡張機能、メモリをファイルします。
- ボックスの自動構成サポート WDK プリンター、メモリ
- autoconfiguring プリンター メモリ WDK
- プリンター メモリの構成の WDK の自動構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ece6688e56a9f3e601ff76272c83383268b1d313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349276"
---
# <a name="autoconfiguring-the-printers-memory-for-gpd"></a>GPD のプリンターのメモリを自動構成する


次のコード例では、GPD ファイル内の任意のメモリ オプションの GDL ファイルにエントリを追加する方法を示します。 次の例の後に表示される GPD のコード例は、メモリ機能の一般的な定義です。

```GPD
*Feature: Memory
{
  *rcNameID: =PRINTER_MEMORY_DISPLAY
  *DefaultOption: 4096KB

  *MemConfigKB: PAIR(4096, 3150)
  *MemConfigKB: PAIR(8192, 6750)
}
```

GDL ファイルに次の機能を追加することでメモリの自動構成を有効にすることができます。

```GDL
*% This feature definition merges with the definition in the GPD file
*Feature: Memory
{
  *% *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: Memory
  {
  *QueryString: "\Printer.Configuration.Memory:Size"
  }
  *BidiResponse: Memory
   {
    *ResponseType: BIDI_INT
    *ResponseData: ENUM_OPTION (Memory)
  }

  *Option: 4096KB
  {
    *% Names for the memory options already defined in GPD
    *BidiValue: INT(4096)
  }

  *Option: 8192KB
  {
    *BidiValue: INT(8192)
  }
}
```









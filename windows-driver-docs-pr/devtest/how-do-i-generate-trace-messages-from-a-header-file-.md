---
title: ヘッダー ファイルからのトレース メッセージを生成する方法
description: ヘッダー ファイルからのトレース メッセージを生成する方法
ms.assetid: 00b97f26-90e2-4efe-8bba-e3ffe7ba90ea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564b4f70862ab858ac0fd698e91d816c3340472e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329869"
---
# <a name="how-do-i-generate-trace-messages-from-a-header-file"></a>ヘッダー ファイルからトレース メッセージを生成する方法


.C、.c ファイルでは、.cpp、.cxx 以外のファイル名拡張子を持つソース ファイルからのトレース メッセージを生成するには、追加、 **- ext** 、実行するようにパラメーター\_WPP マクロは、Windows ソフトウェア トレース プリプロセッサを呼び出します。

たとえば、.c ファイルと .h ファイルからトレースを生成するには、次のステートメントを使用します。

```
RUN_WPP=$(SOURCES) -km -ext:.c.h
```
.H ファイルでスキャンする tracewpp ニーズが含まれていることを必ず`$(SOURCES)`コマンドラインに追加することもできます。  
例:

```
RUN_WPP=$(SOURCES) tracedrv.h -km -ext:.c.h
```
*いない*.h ファイルは、スキャンで指定されている: など、構成データ ファイルとしてオプション`trace.h`します。

**- Ext**パラメーターは、ソース ファイルとして WPP を認識するファイルの種類を指定します。 WPP は、別のファイル名拡張子の付いたファイルを無視します。 既定では、WPP は .c、.c ファイルでは、.cpp と .cxx ファイルのみを認識します。

このパラメーターの値は、大文字小文字を区別するためのバージョンの Windows Vista より前の Windows でのすべてのケースが一覧表示する必要があります。 次に、例を示します。

```
RUN_WPP=$(SOURCES) -km -ext:.c.C.h.H
```

また、ヘッダー ファイルでは、別のソース ファイルと同じ名前が付いている場合は、追加、 **- preserveext** 、実行するようにパラメーター\_WPP マクロ。 次に、例を示します。

```
RUN_WPP=$(SOURCES) -km -ext:.c.C.h.H  -preserveext:.c.h
```

**- Preserveext**パラメーターの名前を作成するときに、指定したファイル名拡張子が保持されます[トレース メッセージのヘッダー](trace-message-header-file.md) (.tmh) ファイル。 このパラメーターは、WPP が同じ名前の複数の TMH ファイルを作成することを防ぎます。 既定では、WPP はのみ .tmh ファイル名拡張子、tracedrv.tmh などを使用します。 **- Preserveext**パラメーター ファイルは代わりにという tracedrv.c.tmh tracedrv.h.tmh します。

実行の省略可能なパラメーターの完全な一覧については\_WPP を参照してください[WPP プリプロセッサ](wpp-preprocessor.md)します。

 

 






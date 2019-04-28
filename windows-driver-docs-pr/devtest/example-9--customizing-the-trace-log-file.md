---
title: 例 9 はトレース ログ ファイルをカスタマイズします。
description: 例 9 はトレース ログ ファイルをカスタマイズします。
ms.assetid: b65b4d15-f058-425a-b2b2-b040265d48ac
keywords:
- WDK のトレース ログ
- WDK のトレース ログに記録します。
- カスタムのトレース ログは、WDK
- イベント トレース ログは、WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eacb0221c65ec0afd4ce56364612bed3fd9aba0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378826"
---
# <a name="example-9-customizing-the-trace-log-file"></a>例 9:トレース ログ ファイルのカスタマイズ


## <span id="ddk_customizing_the_trace_log_file_tools"></span><span id="DDK_CUSTOMIZING_THE_TRACE_LOG_FILE_TOOLS"></span>


この例のコマンドは、トレース ログを生成するイベントのトレース ログ ファイルをカスタマイズするためのさまざまな方法を示します。

**循環ファイルです。** 次のコマンドは、循環ログ ファイルを使用してトレース ログ セッションを開始します。 使用して、 **-cir**パラメーターを 2 MB の最大サイズの循環ログ ファイルを指定します。

最大ファイル サイズの値を省略した場合 (この場合、 **2**)、トレース ログは、パラメーターを無視し、シーケンシャル トレース ログ ファイルと、セッションを開始します。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -cir 2
```

**事前に割り当てられるファイルです。** 次のコマンドは、事前に割り当てられたファイルを使用してトレース ログ セッションを開始します。 この場合、ファイルは、トレース セッションを開始する前にサイズが大きすぎることが対応することを確認する事前に割り当てられるでした。

このコマンドを使用して、 **-seq**最大ファイル サイズが 128 MB の連続したイベントのトレース ログ ファイルを指定するパラメーターを使用して、 **- prealloc**パラメーターを事前に割り当てられたファイルを要求します。 シーケンシャル ファイルは、既定値が、 **-seq**パラメーターが事前に割り当てられたファイルに必要なファイルの最大サイズを指定するために使用します。 **-Cir**パラメーターがの最大ファイル サイズを指定することもできます **- prealloc**円形のファイルが優先されます。

```
tracelog -start MyTrace -guid MyProvider.guid -f testtrace.etl -seq 128 -prealloc
```

**複数のファイル。** 次のコマンドは、一連の 1 つの大きなファイルではなくより小さな、シーケンシャル イベント トレース ログ ファイルを生成するトレース ログ セッションを開始します。

コマンドを使用して、 **- newfile**パラメーター ファイルの最大サイズの値を現在のログ ファイルが 1 MB に達するたびに、新しいトレース ログ ファイルを開始する 1 を使用します。 指定されたファイル名も、 **-f**パラメーターには、文字が含まれています。 **%d**を使用したときに必要な、 **- newfile**します。 ファイルのカウンター値で置き換えられます **%d**と各ファイルが作成されます。

```
tracelog -start MyTrace −guid MyProvider.guid -f testtrace%d.etl -newfile 1
```

結果として得られる 1 MB のファイルは、これらは作成されたこと、たとえば testtrace1.etl 順序で番号が付けられます。

 

 






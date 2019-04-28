---
title: ソース行の構文
description: ソース行の構文
ms.assetid: a4622a89-6419-4547-9650-eb10c3803462
keywords:
- ソース行番号の式
- ソース ファイルとパス、行番号の構文
- 行番号の構文
- ソース ファイルとパス、ファイル名の構文
- ファイル名の構文
- ソース行番号、コマンドの構文規則
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f2595e618906116bbe89a05e91082d3051912a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368099"
---
# <a name="source-line-syntax"></a>ソース行の構文


## <span id="ddk_source_line_syntax_dbg"></span><span id="DDK_SOURCE_LINE_SYNTAX_DBG"></span>


MASM 式の一部または全体としては、ソース ファイルの行番号を指定できます。 これらの数値は、このソース行に対応する実行可能コードのオフセットに評価されます。

**注**   C++ 式の一部としてソース行番号を使用することはできません。 詳細については、MASM および C++ の式の構文を使用する場合、次を参照してください。[を評価する式](evaluating-expressions.md)します。

 

アクサン グラーブによってソース ファイルと行番号の式を囲む必要があります ( **\`** )。 次の例では、完全なソース ファイルの行番号の形式を示します。

```text
`[[Module!]Filename][:LineNumber]`
```

同じファイルの名前を持つ複数のファイルがある場合*Filename*ディレクトリ全体のパスとファイル名を含める必要があります。 このディレクトリ パスには、コンパイル時に使用される 1 つを指定します。 ファイル名またはパスの一部のみを指定して、複数の一致がある場合は、デバッガーは、検出された最初の一致を使用します。

省略した場合*Filename*デバッガーは、現在のプログラム カウンターに対応するソース ファイルを使用します。

*LineNumber*する前にいない場合は、10 進数として読み取ら**0 x**の現在の既定の基数に関係なく、します。 省略した場合*LineNumber*、ソース ファイルに対応する実行可能ファイルの最初のアドレスに式が評価されます。

実行しない限り、CDB でソース行の式は評価されません、 [ **.lines (切り替えのソース行のサポート)** ](-lines--toggle-source-line-support-.md)コマンドが含まれて、 [ **-コマンド ライン オプション行**](cdb-command-line-options.md) WinDbg を開始する.

ソースのデバッグの詳細については、次を参照してください。[元のモードでデバッグ](debugging-in-source-mode.md)します。

 

 






---
title: Debugger Data Model - 命令オブジェクト
description: 命令オブジェクトは、単一のコンピューター命令を記述します。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2726da94f4efceb077b517c3a16a737072f3af1
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402303"
---
# <a name="instruction-objects"></a>命令オブジェクト

## <a name="summary"></a>まとめ

命令オブジェクトは、単一のコンピューター命令を記述し、命令ベースの逆アセンブリまたは[基本ブロック](dbgmodel-object-basic-block.md)オブジェクトの内容の一部として返されます。

## <a name="object-properties"></a>オブジェクトのプロパティ

|名前|説明|
|--- |--- |
|Address|コンピューター命令のアドレス。|
|属性|命令の詳細を記述する[命令属性](dbgmodel-object-instruction-attributes.md)オブジェクト。|
|Codebytes,|マシン命令を構成するバイトを表すバイト配列。|
|長さ|命令がメモリ内で取るバイト数。|
|LiveVariables|この特定の場所で、コンパイラオプティマイザーが変数に対して出力したデータを記述する[ライブ変数](dbgmodel-object-live-variable.md)オブジェクトの[コレクション](dbgmodel-namespace-collections.md)。|
|オペランド|命令のオペランドを記述する[オペランド](dbgmodel-object-operand.md)オブジェクトの[コレクション](dbgmodel-namespace-collections.md)。|
|SourceInformation|コンピューター命令と上位レベルのソースコードの関係を記述する[ソース情報](dbgmodel-object-source-information.md)オブジェクト。|
|SourceDataFlow フロー|コンピューター命令のソースオペランドのデータフローを構成する、関数内の[命令](dbgmodel-object-instruction.md)オブジェクトの[コレクション](dbgmodel-namespace-collections.md)。 **このメソッドでは、 [Codeflow 拡張機能](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)を読み込む必要があります。**|

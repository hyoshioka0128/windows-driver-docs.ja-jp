---
title: Debugger Data Model - 命令オブジェクト
description: 命令のオブジェクトには、1 台のマシン命令がについて説明します。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e4513cbdb5235341d962f212ab46b9267decfb75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376072"
---
# <a name="instruction-objects"></a>命令オブジェクト 
## <a name="summary"></a>概要
命令のオブジェクトが 1 台のマシン命令を記述して、いずれかの命令に基づく逆アセンブリを使用してまたはの内容の一部として返されます、[基本ブロック](dbgmodel-object-basic-block.md)オブジェクト。 
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|Address|マシン語命令のアドレス。|
|属性|[命令属性](dbgmodel-object-instruction-attributes.md)命令についての詳細を記述するオブジェクト。|
|CodeBytes|マシン命令を構成するバイト数を表すバイトの配列。|
|長さ|命令は、メモリのバイト数。|
|LiveVariables|A[コレクション](dbgmodel-namespace-collections.md)の[ライブ変数](dbgmodel-object-live-variable.md)コンパイラ オプティマイザーは、この特定の場所に変数の出力がデータを記述するオブジェクト。|
|オペランド|A[コレクション](dbgmodel-namespace-collections.md)の[オペランド](dbgmodel-object-operand.md)命令のオペランドを記述するオブジェクト。|
|SourceInformation|A[ソース情報](dbgmodel-object-source-information.md)マシン語命令とより高いレベルのソース コード間のリレーションシップを記述するオブジェクト。|
|SourceDataFlow|A[コレクション](dbgmodel-namespace-collections.md)の[命令](dbgmodel-object-instruction.md)関数内でのマシン命令のオペランドでソース データ フローを構成するオブジェクト。 **このメソッドは、見つかった CodeFlow 拡張機能を読み込む必要があります[ここ](https://github.com/Microsoft/WinDbg-Samples/tree/master/CodeFlow)します。**|
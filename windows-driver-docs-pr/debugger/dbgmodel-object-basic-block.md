---
title: Debugger Data Model - 基本ブロック オブジェクト
description: 基本的な要素は、(通常は) 1 つのエントリ ポイントと 1 つの終了ポイントを使用したコードの領域です。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c121f4969b21474dc301d6488dabaf166691f1cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376079"
---
# <a name="basic-block-objects"></a>基本的なブロックのオブジェクト 
## <a name="summary"></a>概要
基本的な要素は、(通常は) 1 つのエントリ ポイントと 1 つの終了ポイントを使用したコードの領域です。 [逆アセンブラー](dbgmodel-object-disassembler.md)DisassembleBlocks と DisassembleFunction メソッドは両方ともの基本的な要素のコレクションを返します。 DisassembleBlocks メソッドは、基本的な要素の簡単な分析を行い、複数のエントリ ポイントでブロックがあります。 DisassembleFunction では、1 つのエントリと 1 つの終了を使用して基本的な要素に関数の完全なフロー分析を実行します。
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|StartAddress|基本的なブロックの開始アドレス。|
|endAddress|基本的なブロックの終了アドレス。 ハーフ オープン セットによって、ブロックが定義されている [*StartAddress*、 *EndAddress*)。|
|手順|A[コレクション](dbgmodel-namespace-collections.md)の[命令](dbgmodel-object-instruction.md)基本ブロック内のオブジェクト。|
|InboundControlFlows|このプロパティは完全なフローの分析の結果である基本ブロック上に存在する (例。*DisassembleFunction*)。 [コレクション](dbgmodel-namespace-collections.md)の[制御フロー](dbgmodel-object-control-flow.md)他のブロックが受信したを記述するオブジェクトは、このフローへのリンクを制御します。|
|OutboundControlFlows|このプロパティは完全なフローの分析の結果である基本ブロック上に存在する (例。*DisassembleFunction*)。 [コレクション](dbgmodel-namespace-collections.md)の[制御フロー](dbgmodel-object-control-flow.md)送信制御を記述するオブジェクトがこのブロックから、関数では、他のブロックへのリンクをフローします。|
---
title: ログのマニフェストの概要
description: ログのマニフェストの概要
ms.assetid: abf550c5-6b70-4043-b2e9-d3dc5096cc4e
keywords:
- LogViewer、マニフェスト
- LogViewer、マニフェスト、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eea59260a5928503ff0e670758c24d5983bbf9b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366459"
---
# <a name="overview-of-the-logging-manifest"></a>ログのマニフェストの概要


## <span id="ddk_overview_of_the_logging_manifest_dtoolq"></span><span id="DDK_OVERVIEW_OF_THE_LOGGING_MANIFEST_DTOOLQ"></span>


ログ記録のマニフェストは、関数およびインターセプトされ、ログに記録される COM インターフェイスを定義する"header"ファイルのグループです。 これらは C++ ヘッダー ファイルの場合は true ではありません--情報を明示的に宣言するわずかに異なる形式で必要なロガーによってです。

たとえば、マニフェストの形式には、次の機能が容易になります。

-   OUT パラメーターの指定です。 これらは、パラメーターを関数とその方法を両方の方法でログ記録する必要がありますがなです。

-   フラグのマスクの定義。 この機能は、DWORD フラグを読みやすくするためには、その構成要素であるビット ラベルに分割する LogViewer を使用できます。

-   エラー ケースの定義。 この機能は、エラー状態コードまたは別のエラー コードが返される関数の行に影を付ける LogViewer を使用できます。 また場合は、関数は、スレッドの"LastError"値を設定、LogViewer できます離れたエラー コードを格納、対応する人間が判読できるエラー メッセージを展開します。

-   ログの差分のエイリアスは、パラメーターの指定です。 この機能は、LogViewer データをファイルにエクスポートするとき、ポインター、ハンドルなどの実行から実行するを変更する値に定数文字列を割り当てるオプションを提供します。 2 つの実行ログの不一致を比較するのに差分ツールを使用することができますし。 ポインター、ハンドル値がエイリアス化でない場合は、2 つのファイルを比較すると不要な相違点が生成されるは。

 

 






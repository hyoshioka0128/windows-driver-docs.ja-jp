---
title: Logger の制限事項と制約事項
description: Logger の制限事項と制約事項
ms.assetid: cb16c193-5420-4900-bf07-44b49859e296
keywords:
- ロガーの制限
- ロガー、制限事項
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1549e9ab32f9a156c454d92fe59319e0a1aeb3de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383326"
---
# <a name="logger-restrictions-and-limitations"></a>Logger の制限事項と制約事項


## <span id="ddk_logger_restrictions_and_limitations_dtoolq"></span><span id="DDK_LOGGER_RESTRICTIONS_AND_LIMITATIONS_DTOOLQ"></span>


ロガーでは、実際の関数呼び出しの前に追加の「ラッピング」関数を導入するため、プロセスのスタックの使用量が増加します。

これは、初期化されていない変数に関連する、通常、アプリケーションのバグを公開できます。 ロガーは、スタックの使用を変更、ため関数呼び出しで宣言されたローカル変数は、ロガーの介入なしにあるときよりも別の初期値をかかる場合があります。 場合は、プログラムでは、この変数を使用して初期化せず、プログラムがクラッシュかロガーが存在しなかった場合は異なる動作をそれ以外の場合。

残念ながら、簡単にこのような問題を回避することはありません。 唯一の回避策では、問題の原因となっている領域を分離するために関数のカテゴリを無効にしてください。

 

 






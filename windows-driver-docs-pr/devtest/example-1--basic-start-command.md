---
title: 例 1 の基本的な Start コマンド
description: 例 1 の基本的な Start コマンド
ms.assetid: be5abbf0-727d-430b-a427-66cc61f3445c
keywords:
- トレース セッションを開始、WDK
- コマンドを開始します。
- -コマンドの開始
- トレース セッションの起動
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65accf8e96bf70ccdd318b93e817e676db4d6e4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344791"
---
# <a name="example-1-basic-start-command"></a>例 1:基本的な開始コマンド


次のコマンドは、標準のトレース セッションを開始する最も簡単なコマンドの例を示します。

```
tracelog -start MyTrace
```

このコマンドは、"MyTrace"という名前のセッションを開始します。 セッションが既定の場所を C でのログ ファイルを含むその他のセッションのプロパティの既定値\\LogFile.etl します。

場合は、コマンドでは、セッション名は含まれませんが、トレース ログが開始した、既定値は、NT Kernel Logger トレース セッション。

コマンドが含まれていないため、 **- guid**パラメーターは、トレース セッションのプロバイダーが許可されていない、使用することが、 **tracelog-有効にする**このセッションの開始後にプロバイダーを追加するコマンド。 参照してください[例 5。トレース プロバイダーを有効にする](example-5--enabling-trace-providers.md)を使用する方法の例については、 **-有効にする**コマンド。

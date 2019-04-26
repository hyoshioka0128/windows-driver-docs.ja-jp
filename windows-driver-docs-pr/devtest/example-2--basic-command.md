---
title: 例 2 の基本的なコマンド
description: 例 2 の基本的なコマンド
ms.assetid: 5e66b7f4-5cf6-4bfc-b432-d531ac6ac53c
keywords:
- Tracefmt WDK、コマンド
- WDK Tracefmt コマンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb32465f493a45e20441ac9a0651e9724a7e0864
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344704"
---
# <a name="example-2-basic-command"></a>例 2:基本的なコマンド

Tracefmt を開始するために使用する基本的なコマンドの構文は次のとおりです。

```
tracefmt EtlFile -p TMFPath -o OutputFile
```

以下に例を示します。

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.txt
```

このコマンドは EtlFile パラメーターを使用してトレース ログ ファイルを指定 mytrace.etl します。 使用して、 **-p** TMF ファイルが格納されているディレクトリを表すパラメーターおよび **-o**出力ファイルの代替名を指定するパラメーター。

Tracefmt 応答として、c: TMF ファイルを使用して mytrace.etl トレース ログ ファイルにトレース メッセージの書式設定\\トレース ディレクトリ。 Mytrace.txt および mytrace.txt.sum をという名前の概要ファイルという名前の出力ファイルを作成します。

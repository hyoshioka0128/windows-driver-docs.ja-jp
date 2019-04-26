---
title: 例 4 のシーケンス番号
description: 例 4 のシーケンス番号
ms.assetid: 5b498267-c495-4a25-abb9-aa83a51559e1
keywords:
- Tracefmt WDK、シーケンス番号
- シーケンス番号の WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0c141cffa79d9188d7fff476f776d4aecd26052
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344674"
---
# <a name="example-4-sequence-numbers"></a>例 4:シーケンス番号


次のコマンドには、出力ファイルには中に、メッセージのローカルまたはグローバルのシーケンス番号が含まれます。 シーケンス番号が生成された場合、シーケンス フィールドには、ゼロが含まれています。

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.txt -seq
```

このコマンドは、c: TMF ファイルを使用して、mytrace.etl ログ ファイルからのメッセージを書式設定\\トレース ディレクトリ。 Mytrace.txt ファイルを書式設定されたメッセージを書き込みます。 コマンドを使用して、 **-seq**にシーケンス番号を出力ファイルに含める Tracefmt に出力するためのパラメーター。

出力ファイルの抜粋が表示されます。

```text
[0]0AF4.0C64::07/25/2003-13:55:39.998 00004ea4 [tracedrv]IOCTL = 1
[0]0AF4.0C64::07/25/2003-13:55:39.998 000047d0 [tracedrv]Hello, 1 Hi
[0]0AF4.0C64::07/25/2003-13:55:39.998 63966c89 [tracedrv]Hello, 2 Hi
...
```

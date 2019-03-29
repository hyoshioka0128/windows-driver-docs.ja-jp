---
title: Tracefmt の出力ファイル
description: Tracefmt の出力ファイル
ms.assetid: 55c8964c-992f-468c-83ea-0316fcb12110
keywords:
- Tracefmt WDK では、出力ファイル
- 出力ファイルは、WDK Tracefmt
- WDK Tracefmt ファイル
- .out ファイル
- ファイルを
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98132e51949b9c29b8affce8bc458fb4db42a04d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570230"
---
# <a name="tracefmt-output-file"></a>Tracefmt の出力ファイル


Tracefmt (.out) を出力ファイルは、人間が判読できる形式で、トレース ログまたはトレースのリアルタイムのセッションからのトレース メッセージを表示するテキスト ファイルです。 各トレース メッセージは、カスタマイズ可能な付いている[トレース メッセージのプレフィックス](trace-message-prefix.md)します。

Tracefmt 出力ファイルは省略可能です。 、トレース メッセージの表示が、出力ファイルを作成またはトレース メッセージを表示して、出力ファイルに記録する Tracefmt を指示することができます。

Tracefmt 出力ファイルが分析およびトレース メッセージをフィルター処理する他のプログラムへの入力としてよく使用されます。

Tracedrv、ソフトウェア トレース用にインストルメント化サンプル ドライバーでのトレース セッションが Tracefmt 出力ファイルの内容の抜粋を次に示します。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレースのように設計されたドライバーのサンプルが記載されて、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

```
EventTrace
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]IOCTL = 1
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 1 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 2 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 3 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 4 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 5 Hi
[0]0888.0D60::10/23/2003-12:27:40.173 [tracedrv]Hello, 6 Hi
```

 

 






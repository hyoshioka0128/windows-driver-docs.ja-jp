---
title: CSV ファイル形式を使用して 8 の例
description: CSV ファイル形式を使用して 8 の例
ms.assetid: 225365dd-57f8-4d35-a859-b881a104201f
keywords:
- Tracefmt WDK、CSV 形式
- CSV 形式 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19956cee86badc030dc3ca75ec866041f2142929
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578055"
---
# <a name="example-8-using-the-csv-file-format"></a>例 8:CSV ファイル形式の使用


次のコマンドを使用する Tracefmt トレース メッセージの出力ファイルの書式設定 (**-o**) コンマで区切り、可変長 (CSV) 形式のファイルとして。

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.csv -csv -csvheader
```

このコマンドは、mytrace.etl トレース ログ ファイルにトレース メッセージを書式設定します。 使用して、 **-p** TMF ファイルの場所を指定するパラメーター。

コマンドを使用して、 **-o**出力ファイルの場所と名前を指定するパラメーター ファイルを .csv ファイル拡張子を使用しています。 使用して、 **csv** 、CSV 形式を指定するパラメーター、および **- csvheader**ファイルに列ヘッダーの行を追加するパラメーター。 既定では、ファイルに列ヘッダーがありません。

応答として、Tracefmt はプレフィックスとメッセージ フィールドの間にコンマを使用して、トレース メッセージを書式設定し、mytrace.csv ファイルに保存します。

 

 






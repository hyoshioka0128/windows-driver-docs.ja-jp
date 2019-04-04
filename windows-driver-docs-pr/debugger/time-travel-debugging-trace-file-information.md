---
title: タイム トラベル デバッグ - トレース ファイルの使用
description: このセクションは、タイム トラベルのトレース ファイルを操作する方法を説明します
ms.date: 09/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c609e8104f15f0a2561af667e878ba1f0e3244e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578814"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---working-with-trace-files"></a>タイム トラベル デバッグ - トレース ファイルの使用

このセクションでは、作成、およびタイム トラベルのデバッグで使用されるファイルを操作する方法について説明します。

## <a name="trace-file-overview"></a>トレース ファイルの概要

タイム トラベルのデバッグは、次のファイルを使用して、デバッグ コードが実行します。

- トレース ファイルを選択し、コード実行の記録が含まれていますが、します。拡張機能を実行します。

- インデックス ファイルを選択し、トレース ファイルの情報にすばやくアクセスできますが、します。IDX 拡張機能。

- 記録のエラーとその他の記録の出力は、デバッガーのログ ファイルに書き込まれます。


## <a name="trace-run-files"></a>トレースします。ファイルを実行します。  

トレースします。使用して記録された後、実行ファイルを開くことができる**ファイル** > **デバッグを開始** > **トレース ファイルを開く**します。

![開いているトレースのオプションが強調表示を示すファイルを開くオプション](images/ttd-start-debugging-options.png) 

トレースのすべての出力ファイルは、既定では、ユーザーのドキュメント フォルダーに格納されます。 たとえば、User1 の TTD ファイルがここに保存。

```console
C:\Users\User1\Documents
```
記録を開始するときは、トレース ファイルの場所を変更できます。 詳細については、[タイム トラベル デバッグ - 記録](time-travel-debugging-record.md)を参照してください。

ファイルの最近使用した一覧は、ターゲットの構成ファイルに以前使用したアクセスすばやくできます。 いずれかの最近使用したトレース ファイルまたはダンプ ファイルがも一覧表示します。 

![ファイルが最近 5 つを示す実行トレース ファイルの一覧を開くトレース ファイルの使用](images/ttd-recent-trace-files.png) 


## <a name="index-idx-files"></a>インデックス。IDX ファイル  

インデックス。IDX ファイルは、関連するトレースに作成されます。WinDbg のプレビューでのトレース ファイルを開くときに、ファイルを自動的に実行します。 使用してインデックス ファイルを手動で作成することができます、! コマンドのインデックスを作成します。 インデックスは、トレース情報にすばやくアクセスできます。 

IDX ファイルは大きくなることも通常 2 倍のサイズします。ファイルを実行します。  

## <a name="recreating-the-idx-file"></a>再作成します。IDX ファイル
再作成することができます、します。IDX ファイルから、します。実行ファイルを使用して、`!index`コマンド。 詳細については、[時のデバッグ出張 -! インデックス (タイム トラベル)](time-travel-debugging-extension-index.md)を参照してください。

```dbgcmd
0:0:001> !index
Indexed 3/3 keyframes
Successfully created the index in 49ms.
```

## <a name="sharing-ttd-trace-run-files"></a>TTD トレースを共有します。ファイルを実行します。

TTD トレース ファイルは、コピーして他のユーザーと共有できる、します。ファイルを実行します。 これは、問題を把握する同僚のヘルプを持つ場合に便利です。 クラッシュしているアプリをインストールまたはこの問題を再現しようとするその他の関連のセットアップを実行する必要がありません。 だけ、トレース ファイルの読み込みし、自分の PC にインストールされている場合に、アプリのデバッグができます。 

日付やバグ番号などの追加情報を含めるよう、ファイルの名前を変更することができます。

します。IDX ファイルが再作成できますを使用して、コピーする必要はありません、! 上に示したコマンドのインデックスを作成します。


> [!TIP]
> 他のユーザーと共同作業をするときは、当面の問題に関連するすべての関連するトレース位置に渡します。 コラボレーターが使用できる、`!tt x:y`その正確なポイントで、コードの実行時に移動するコマンド。 時間位置の範囲は、考えられる問題が発生する可能性を追跡するためにバグの説明に含めることができます。
>


## <a name="error---log-file"></a>エラー - ログ ファイル

記録のエラーとその他の記録の出力は、デバッガーのログ ファイルに書き込まれます。 ログ ファイルを表示するには、次のように選択します。**ビュー** > **ログ**します。 

この例を起動し、実行可能ファイル、C:\Windows ディレクトリ内にない Foo.exe という名前を記録する際に、エラー ログのテキストを示します。

```console
2017-09-21:17:18:10:320 : Information : DbgXUI.dll : TTD: Output: 
Microsoft (R) TTD 1.01.02
Release: 10.0.16366.1000
Copyright (C) Microsoft Corporation. All rights reserved.
Launching C:\Windows\Foo.exe
2017-09-21:17:18:10:320 : Error : DbgXUI.dll : TTD: Errors: 
Error: Trace of C:\Windows\Foo.exe PID:0 did not complete successfully: status:27
Error: Could not open 'Foo.exe'; file not found.
Error: Corrupted trace dumped to C:\Users\User1\Documents\Foo01.run.err.
```


## <a name="see-also"></a>関連項目

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---







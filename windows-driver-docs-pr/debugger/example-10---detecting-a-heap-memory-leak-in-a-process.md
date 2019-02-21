---
title: プロセスのヒープ メモリ リークを検出する 10 の使用例
description: プロセスのヒープ メモリ リークを検出する 10 の使用例
ms.assetid: ec98dd96-b12b-4f83-85e8-2c5ee32fc17e
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e04334e3cf26dd734a7964d974e62f832f650ef0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550912"
---
# <a name="example-10-detecting-a-heap-memory-leak-in-a-process"></a>例 10:プロセスのヒープ メモリ リークを検出します。


## <span id="ddk_example_10___detecting_a_heap_memory_leak_in_a_process_dtools"></span><span id="DDK_EXAMPLE_10___DETECTING_A_HEAP_MEMORY_LEAK_IN_A_PROCESS_DTOOLS"></span>


この例では GFlags とユーザー モード ダンプ ヒープ (UMDH、umdh.exe)、デバッグ ツールの Windows Microsoft に含まれるツールです。

**Notepad.exe のヒープ メモリのリークを検出するには**

1.  設定、[ユーザー モードのスタック トレースのデータベースの作成](create-user-mode-stack-trace-database.md)(**ust**)、notepad.exe ファイルがイメージのフラグ。

    次のコマンドは GFlags を使用して、設定、**ユーザー モードのスタック トレースのデータベースの作成**フラグ。 使用して、 **/i**イメージ ファイルを識別するためにパラメーターおよび**ust**フラグの省略形。

    ```console
    gflags /i Notepad.exe +ust 
    ```

    このコマンドでは、結果として、Notepad プロセスのすべての新しいインスタンスのユーザー モードのスタック トレースが作成されます。

2.  シンボル ファイルのパスを設定します。

    次のコマンドは、シンボル ファイルのディレクトリへのパスを格納する環境変数を作成します。

    ```console
    set _NT_SYMBOL_PATH=C:\Windows\symbols
    ```

3.  メモ帳を起動します。

4.  メモ帳プロセスのプロセス id (PID) を検索します。

    タスク マネージャーまたは Windows XP Professional および Windows Server 2003 オペレーティング システムに付属するツールの Tasklist (tasklist.exe) から任意の実行中のプロセスの PID が見つかります。 この例では、メモ帳の PID は 1228 です。

5.  UMDH を実行します。

    次のコマンドは、UMDH (umdh.exe) を実行します。 使用して、 **-p:** をこの例では 1228 PID を指定するパラメーター。 使用して、 **/f:** ヒープ ダンプの出力ファイルの場所と名前を指定するパラメーター notepad.dmp します。

    ```console
    umdh -p:1228 -f:notepad.dmp 
    ```

    応答では、UMDH は、すべてのアクティブなヒープ notepad.dmp ファイルへの完全なダンプを書き込みます。

 

 






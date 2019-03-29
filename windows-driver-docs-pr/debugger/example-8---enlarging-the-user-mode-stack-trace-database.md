---
title: 例 8 ユーザー モードのスタック トレースのデータベースの拡大
description: 例 8 ユーザー モードのスタック トレースのデータベースの拡大
ms.assetid: b04f6b86-a210-4941-a4eb-a9059d9890d9
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b2a72106e22c3737782ceb0b48aca8d5d791971
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580142"
---
# <a name="example-8-enlarging-the-user-mode-stack-trace-database"></a>例 8:ユーザーモード スタック トレース データベースを拡大する


## <span id="ddk_example_8___enlarging_the_user_mode_stack_trace_database_dtools"></span><span id="DDK_EXAMPLE_8___ENLARGING_THE_USER_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


次の GFlags コマンドには、myapp.exe、8 MB ~ 24 MB からの架空のプログラムのユーザー モードのスタック トレース データベースの最大サイズが増加します。

コマンドを使用して、 **/i**イメージ ファイルを指定するパラメーター。 使用して、 **/tracedb**最大スタック トレースのデータベースのサイズと 24 サイズ (メガバイト単位) を示す値を設定するパラメーター。 コマンドは、10 進数のユニットを使用します。 (16 進数のユニットが無効です。)

```console
gflags /i MyApp.exe /tracedb 24
```

ため、このコマンドは失敗、次のエラー メッセージが示すとおり、[ユーザー モードのスタック トレースのデータベースの作成](create-user-mode-stack-trace-database.md)(+ ust) MyApp イメージ ファイルのフラグが設定されていません。 1 つを作成するまで、トレース データベースのサイズを設定することはできません。

```console
Failed to set the trace database size for `MyApp.exe'
```

次のコマンドは、このエラーを解決します。 最初のコマンドは、myapp.exe のトレースのデータベースを作成し、2 番目のコマンドは、24 MB にトレース データベースの最大サイズを設定します。 これらのコマンドは、1 つのコマンドにまとめることはできません。 次の表示では、コマンドと成功メッセージが GFlags から表示します。

```console
gflags /i MyApp.exe +ust

Current Registry Settings for MyApp.exe executable are: 00001000
    ust - Create user mode stack trace database

gflags /i MyApp.exe /tracedb 24

Trace database size for `MyApp.exe' set to 24 Mb.
```

GFlags がユーザー モードのスタック トレース データベースのサイズを変更できますが、表示されません。 トレース データベースのサイズを表示するには、値を確認するレジストリ Api、Regedit、または Reg (reg.exe)、Windows XP および Windows Server 2003 に付属するツールを使用、 **StackTraceDatabaseSizeInMB**レジストリ エントリ (HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\File Execution Options をイメージ\\*ImageFileName* \\ **StackTraceDatabaseSizeInMB**)。

(レジストリのバージョンが Windows xp の場合、含まれていますが、そのバージョンが許可されていません、 **/v**と **/s**同じコマンドにスイッチします)。

次のコマンドは Reg を使用してクエリの値を**StackTraceDatabaseSizeInMB**:

```console
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\MyApp.exe" /v StackTraceDatabaseSizeInMB 
```

応答として、Reg がの値を表示します。 **StackTraceDatabaseSizeInMB**、いることを確認する、新しい値を 24 (0x18) を設定します。 この値は、myapp.exe を再起動したときに有効になります。

```console
! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\MyApp.exe
    StackTraceDatabaseSizeInMB  REG_DWORD       0x18
```

**ヒント:**   型、 **reg クエリ**、メモ帳にコマンドの後、tracedb.bat として、ファイルを保存します。 その後の値を表示する**StackTraceDatabaseSizeInMB**、ただただ**TraceDb**します。

 

 

 






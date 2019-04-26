---
title: Remote.exe バッチ ファイル
description: Remote.exe バッチ ファイル
ms.assetid: e774d39f-4625-41e7-9309-9dbdd46e986e
keywords:
- remote.exe、バッチ ファイルをリモート デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e046856486e044f6c0cf6fb2d229fbebf6ab51a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353522"
---
# <a name="remoteexe-batch-files"></a>Remote.exe バッチ ファイル


## <span id="ddk_remote_exe_batch_files_dbg"></span><span id="DDK_REMOTE_EXE_BATCH_FILES_DBG"></span>


Remote.exe でのリモート デバッグの詳細な例としては、3 台のコンピューターのカーネル デバッグ シナリオでのローカル ホスト コンピューターについては、次を想定しています。

-   COM2 のヌル モデム ケーブルを介して実行する必要がありますをデバッグします。

-   シンボル ファイルがフォルダー c:\\winnt\\シンボル。

-   Debug.log をという名前のログ ファイルが作成された**c:\\temp**します。

ログ ファイルは、デバッグ セッション中にデバッグ画面に表示するすべてのコピーを保持します。 デバッグを実行するユーザーからのすべての入力と、ターゲット システムにカーネル デバッガーからのすべての出力は、そのログ ファイルに書き込まれます。

ローカル ホスト上のデバッグ セッションを実行するためのサンプル バッチ ファイルは次のとおりです。

```bat
set _NT_DEBUG_PORT=com2
set _NT_DEBUG_BAUD_RATE=19200
set _NT_SYMBOL_PATH=c:\winnt\symbols
set _NT_LOG_FILE_OPEN=c:\temp\debug.log
remote /s "KD -v" debug
```

**注**   Remote.exe と同じディレクトリにこのバッチ ファイルがないかどうかと Remote.exe がシステム パスに表示されているディレクトリにないし、このバッチ ファイルで Remote.exe を呼び出すときにユーティリティへの完全なパスを提供する必要があります。

 

このバッチ ファイルを実行するはすべてのユーザーがローカル ホスト コンピューターをネットワークに接続されている Windows コンピューターと、次のコマンドを使用して、デバッグ セッションを接続できます。

```console
remote /c computername debug 
```

場所*computername*ローカル ホスト コンピューターの NetBIOS 名です。

 

 






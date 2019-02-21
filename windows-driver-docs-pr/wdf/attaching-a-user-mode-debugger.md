---
title: ユーザー モード デバッガーのアタッチ
description: ユーザー モード デバッガーのアタッチ
ms.assetid: ba8eeabd-946d-46fa-b9ed-b9a674315bd4
keywords:
- WDK UMDF のデバッガー ユーザー モードのアタッチ
- WDK UMDF 複数デバイス デバッガーの添付ファイル
- WDK UMDF 単一デバイス デバッガーの添付ファイル
- ユーザー モード ドライバー フレームワーク WDK、ユーザー モード デバッガー
- UMDF WDK、ユーザー モード デバッガー
- ユーザー モード デバッガー WDK UMDF
- ユーザー モード デバッガーのアタッチ、WDK UMDF
- ユーザー モード ドライバー WDK UMDF、デバッグ
- ユーザー モード デバッガーのアタッチ、WDK UMDF ドライバーのデバッグ
- デバッグ、ユーザー モード デバッガーのアタッチ、WDK UMDF ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f712d2f24d038920b70f6a4c8439bef03bdc0e08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530190"
---
# <a name="attaching-a-user-mode-debugger"></a>ユーザー モード デバッガーのアタッチ


ドライバー マネージャーは、デバイスのドライバーのホスト プロセスの起動後は、ユーザー モード デバッガーをアタッチすることができます。 デバッガーをアタッチする方法は、コンピューターに関連付けられているデバイスの数によって異なります。

-   1 つのデバイスが接続されている場合は、次のコマンドを実行します。

    ```cpp
    windbg -pn WUDFHost.exe
    ```

    デバッグ ホスト プロセスが検出されるまで、このコマンドを繰り返し実行します。

-   複数のデバイスが接続されている場合は、次のコマンドを実行し、特定のホストのプロセス識別子 (PID) を確認します。

    ```cpp
    windbg -p PID
    ```

    オペレーティング システムが提供 Tasklist.exe を使用すると、ホスト プロセスの PID を決定します。 (Tasklist.exe とは、オペレーティング システムで実行されているプロセスの一覧をユーザーに提供するコマンド ライン アプリケーションです)。

 

 






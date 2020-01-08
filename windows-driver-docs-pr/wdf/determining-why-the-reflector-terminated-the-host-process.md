---
title: リフレクターがホスト プロセスを終了した理由の特定
description: このトピックでは、リフレクターがドライバーホストプロセス (WUDFHost .exe) を終了した理由を分析する方法について説明します。
ms.assetid: c80b117b-597a-494a-bc28-5a918d2a9279
keywords:
- デバッグシナリオ WDK UMDF、リフレクターはホストプロセスを終了します。
- UMDF WDK、デバッグシナリオ、リフレクターはホストプロセスを終了します。
- UMDF WDK、リフレクターはホストプロセスを終了します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0820f51e5e878c27ebadb7875248fa83f918c21d
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694244"
---
# <a name="determining-why-the-reflector-terminated-the-host-process"></a>リフレクターがホスト プロセスを終了した理由の特定


このトピックでは、リフレクターがドライバーホストプロセス (WUDFHost .exe) を終了した理由を分析する方法について説明します。

リフレクターがホストプロセスを終了する最も一般的な理由は、UMDF[ホストプロセスタイムアウト](how-umdf-enforces-time-outs.md)の有効期限です。

テストシステムにアタッチされたカーネルデバッガーで、UMDF ドライバーのすべての開発とテストを行い、WUDFHost で[アプリケーション検証ツール ()](../debugger/debugger-download-tools.md)を有効にすることを強くお勧めします。 次のコマンドを使用して、カーネルデバッガーをアタッチし、再起動します。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

## <a name="using-dump-files"></a>ダンプ ファイルの使用


多くのクラッシュについては、ダンプファイルの詳細で、終了が発生した原因を特定するだけで十分です。 ダンプファイルの情報を確認するには、次の手順を実行します。

1.  % Windir%\\system32\\ログファイル\\WUDF ディレクトリにある最新の .dmp ファイルを見つけます。

    **  UMDF** 2.15 以降では、ログディレクトリは *% programdata%* \\Microsoft\\WDF になります。

     

2.  次のコマンドを使用して、最新の .dmp ファイルをデバッガーに読み込みます。
    ```cpp
    WinDbg -z <path to the .dmp file>
    ```

3.  終了時のスレッドの状態を確認します。

## <a name="using-the-debugger"></a>デバッガーを使用する


また、場合によっては、ライブカーネルモードターゲットにアタッチして、リフレクターがホストプロセスを終了した理由を特定する必要があります。 デバッグセッションを設定するには、「 [UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md#kd)」で説明されている手順に従います。

接続を確立したら、! wdfkd. wdfumtriage を使用して、UMDF ドライバーを調べ、 [ **! wdfkd. wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)の umdf デバッガー拡張機能を使用して未処理の irp を表示します (たとえば、umdf version 1 の場合は[ **! wudfext**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umirps) )。

-   PnP IRP または電源 IRP が保留になっている場合は、ホストプロセス内のスレッドを調べることによって、ドライバーが IRP をハングする原因を特定します。

    [ **! Process**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)拡張機能を使用して、ホストプロセスで実行されているスレッドを調べることができます。 **0x1f**フラグ値には、各スレッドのスタックトレースが表示されます。

    **! プロセス** *&lt;プロセス addr&gt;* **0x1f**

-   ドライバーがキャンセルされた IRP を短時間で完了していない場合は、どの IRP が取り消されたか、および完了していない理由を特定します。
-   クリーンアップまたは閉じる IRP が保留中の場合は、IRP の処理に時間がかかっている理由を特定します。

 

 






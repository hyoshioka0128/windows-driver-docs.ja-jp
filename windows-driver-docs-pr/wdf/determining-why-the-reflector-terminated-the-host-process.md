---
title: リフレクターがホスト プロセスを終了した理由の特定
description: このトピックでは、reflector は、ドライバーのホスト プロセス (WUDFHost.exe) を終了する理由を分析する方法について説明します。
ms.assetid: c80b117b-597a-494a-bc28-5a918d2a9279
keywords:
- reflector は、WDK UMDF のシナリオをデバッグするには、ホスト プロセスを終了します。
- UMDF WDK、デバッグ シナリオでは、reflector は、ホスト プロセスを終了します。
- UMDF WDK、reflector は、ホスト プロセスを終了します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af7e4207a514cc7d45b4f24db1a627d301e03c45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383755"
---
# <a name="determining-why-the-reflector-terminated-the-host-process"></a>リフレクターがホスト プロセスを終了した理由の特定


このトピックでは、reflector は、ドライバーのホスト プロセス (WUDFHost.exe) を終了する理由を分析する方法について説明します。

ホスト プロセスを終了する reflector の最も一般的な理由は、UMDF の有効期限[ホスト プロセスのタイムアウト](how-umdf-enforces-time-outs.md)します。

## <a name="using-dump-files"></a>ダンプ ファイルの使用


多くのクラッシュ ダンプ ファイルの詳細は、終了が発生した理由を判断するための十分です。 ダンプ ファイルの情報を確認するには、次の手順を実行します。

1.  %Windir% に最新の .dmp ファイルを見つけます\\system32\\LogFiles\\WUDF ディレクトリ。

    **注**  ログ ディレクトリは、UMDF 2.15 以降、 *%programdata%*\\Microsoft\\WDF します。

     

2.  次のコマンドを使用して、デバッガーに最新 .dmp ファイルを読み込みます。
    ```cpp
    WinDbg -z <path to the .dmp file>
    ```

3.  終了時に、スレッドの状態を観察します。

## <a name="using-the-debugger"></a>デバッガーを使用します。


それ以外の場合は、リフレクターが、ホスト プロセスを終了した理由を判断するライブのカーネル モードのターゲットにアタッチする必要があります。 デバッグ セッションをセットアップする」に記載の手順に従います[UMDF ドライバーのデバッグを有効にする方法](enabling-a-debugger.md#kd)します。

接続が確立されると、使用して、未処理の Irp を表示、 [ **! wdfkd.wdfumirps** ](https://msdn.microsoft.com/library/windows/hardware/dn265384) UMDF デバッガー拡張機能 ([**! wudfext.umirps** ](https://msdn.microsoft.com/library/windows/hardware/ff566197) umdf バージョン 1)。

-   PnP IRP または電源 IRP が保留中の場合は、理由、ドライバーが原因で、ホスト プロセスでスレッドを調べることでハングする IRP を決定します。

    使用することができます、 [ **! プロセス**](https://msdn.microsoft.com/library/windows/hardware/ff564717)拡張機能をホスト プロセスで実行中のスレッドを調べます。 **0x1f**フラグの値は、各スレッドのスタック トレースを表示します。

    **! プロセス** *&lt;プロセス addr&gt;*  **0x1f**

-   場合は、ドライバーが取り消された IRP を迅速に完了していない、IRP が取り消されましたし、完了いない理由を決定します。
-   クリーンアップまたは閉じる IRP が保留中の場合は、なぜ IRP の処理に長い時間がかかってを決定します。

 

 






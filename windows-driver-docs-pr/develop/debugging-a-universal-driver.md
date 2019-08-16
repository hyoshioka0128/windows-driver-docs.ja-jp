---
title: ユニバーサル Windows ドライバーのデバッグ
description: ユニバーサル Windows ドライバーで使用できるデバッグ手法について説明します。
ms.date: 06/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89cab3d98efeddd87344dd56ce03034b00ae4aee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370761"
---
# <a name="debugging-a-universal-windows-driver"></a>ユニバーサル Windows ドライバーのデバッグ

Windows 10 以降では、KMDF または UMDF ドライバー バイナリをビルドするときに、[インフライト トレース レコーダー](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)を通じて追加のドライバー デバッグ情報を取得するように設定できます。 この機能をユニバーサル Windows ドライバーで利用できます。

さらに、Visual Studio の KMDF テンプレートを使用すると、ドライバーは Windows ソフトウェア トレース プリプロセッサ (WPP) を使ってトレース メッセージを書き込みます。 ドライバー バイナリは、プロバイダー GUID を持つ ETW プロバイダーです。

ドライバー バイナリからトレース メッセージを送信するには、次のコードを使用します。

   ```cpp
   TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");
   ```

ETW ログにアクセスするには、[TShell ツール](https://go.microsoft.com/fwlink/p/?linkid=617388)で Tracelog を使うか、デバッガー セッションで [!wmitrace](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-) を使います。

電話で Tracelog を使うには

1. ホスト コンピューターと電話間のカーネル モード デバッグ セッションを確立します。
2. ホスト コンピューター上の TShell で、次のコマンドを入力します。

       ```cpp
       exec-device tracelog -addautologger MyLogger05 -guid c:\SteveGuid.txt -level 4 -flag 0xF –kd
       ```

3. 電話を再起動し、デバッガーでトレース メッセージを監視します。

既存のすべてのカーネル モード デバッグ トランスポートは、デスクトップ エディションの Windows 10 であれば引き続き動作します。 ただし、Windows 10 Mobile をテストするには、ユーザー モード ドライバー バイナリとカーネル モード ドライバー バイナリのどちらでも、KDNET 経由でリモート デバッガー セッションを使う必要があります。 詳しくは、Visual Studio の「[ネットワーク ケーブル経由でカーネル モード デバッグを手動設定する](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)」をご覧ください。

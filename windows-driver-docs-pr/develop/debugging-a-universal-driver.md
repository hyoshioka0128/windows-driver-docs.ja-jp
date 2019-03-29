---
title: ユニバーサル Windows ドライバーのデバッグ
description: ユニバーサル Windows ドライバーで使用できるデバッグ手法について説明します。
ms.date: 06/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6c6b753c712548b6b90a6549c110871772a2cd2
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349021"
---
# <a name="debugging-a-universal-windows-driver"></a>ユニバーサル Windows ドライバーのデバッグ

Windows 10 以降では、KMDF または UMDF ドライバー バイナリをビルドするときに、[インフライト トレース レコーダー](https://msdn.microsoft.com/Library/Windows/Hardware/Dn914610)を通じて追加のドライバー デバッグ情報を取得するように設定できます。 この機能をユニバーサル Windows ドライバーで利用できます。

さらに、Visual Studio の KMDF テンプレートを使用すると、ドライバーは Windows ソフトウェア トレース プリプロセッサ (WPP) を使ってトレース メッセージを書き込みます。 ドライバー バイナリは、プロバイダー GUID を持つ ETW プロバイダーです。

ドライバー バイナリからトレース メッセージを送信するには、次のコードを使用します。

   ```cpp
   TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");
   ```

ETW ログにアクセスするには、[TShell ツール](https://go.microsoft.com/fwlink/p/?linkid=617388)で Tracelog を使うか、デバッガー セッションで [!wmitrace](https://msdn.microsoft.com/Library/Windows/Hardware/Ff561362) を使います。

電話で Tracelog を使うには

1. ホスト コンピューターと電話間のカーネル モード デバッグ セッションを確立します。
2. ホスト コンピューター上の TShell で、次のコマンドを入力します。

       ```cpp
       exec-device tracelog -addautologger MyLogger05 -guid c:\SteveGuid.txt -level 4 -flag 0xF –kd
       ```

3. 電話を再起動し、デバッガーでトレース メッセージを監視します。

既存のすべてのカーネル モード デバッグ トランスポートは、デスクトップ エディションの Windows 10 であれば引き続き動作します。 ただし、Windows 10 Mobile をテストするには、ユーザー モード ドライバー バイナリとカーネル モード ドライバー バイナリのどちらでも、KDNET 経由でリモート デバッガー セッションを使う必要があります。 詳しくは、Visual Studio の「[ネットワーク ケーブル経由でカーネル モード デバッグを手動設定する](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439346)」をご覧ください。

---
title: WinDbg Preview-リモート、プロセスサーバー、およびダンプファイルのセッション
description: ここでは、WinDbg preview デバッガーを使用して、リモート、プロセスサーバー、およびダンプファイルセッションを開始する方法について説明します。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1a204734b8a2dcaccfc9be1306ca3bcd763838e8
ms.sourcegitcommit: 44bccc9788690ae636b17d7d1cc576b8a17c9916
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81679219"
---
# <a name="windbg-preview---start-a-remote-process-server-and-dump-file-session"></a>WinDbg プレビュー-リモート、プロセスサーバー、ダンプファイルセッションの開始

![WinDbg プレビューの小さなロゴ](images/windbgx-preview-logo.png)

ここでは、WinDbg preview デバッガーを使用して、リモート、プロセスサーバー、およびダンプファイルセッションを開始する方法について説明します。

## <a name="remote-debug-server"></a>リモートデバッグサーバー

リモートデバッグサーバーに接続するには、このオプションを使用します。

![空の接続画面を示すリモートデバッグサーバーのデバッグを開始する](images/windbgx-remote-session.png)

リモートデバッグには、2つの異なる場所で実行される2つのデバッガーが含まれます。 デバッグを実行するデバッガーは、デバッグサーバーと呼ばれます。 デバッグクライアントと呼ばれる2番目のデバッガーは、リモートの場所からデバッグセッションを制御します。 リモートセッションを確立するには、まずデバッグサーバーをセットアップしてから、デバッグクライアントを使用してそれに接続する必要があります。

リモートセッションの詳細については、「 [WinDbg を使用したリモートデバッグ](remote-debugging-using-windbg.md)」を参照してください。

## <a name="process-debug-server"></a>プロセスデバッグサーバー

プロセスサーバーを使用したリモートデバッグでは、サーバーコンピューター上でプロセスサーバーと呼ばれる小規模なアプリケーションを実行します。 その後、ユーザーモードのデバッガーがクライアントコンピューターで開始されます。 このデバッガーは実際の処理をすべて実行するため、スマートクライアントと呼ばれます。

プロセスサーバーセッションの詳細については、「[プロセスサーバー (ユーザーモード)](process-servers--user-mode-.md)」を参照してください。

## <a name="open-a-dump-file"></a>ダンプ ファイルを開く

ダンプファイルを開くには、[指定されたファイル] ダイアログボックスで目的のファイルを参照して開きます。

さまざまな種類のダンプファイルの詳細については、「WinDbg を使用した[クラッシュダンプファイルの分析](crash-dump-files.md)」を参照してください。

---

## <a name="see-also"></a>参照

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)

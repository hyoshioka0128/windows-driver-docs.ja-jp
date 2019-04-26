---
title: ユーザー モード ドライバー フレームワークについてよく寄せられる質問
description: Windows Driver Frameworks (WDF) は、Windows オペレーティング システムで実行するデバイス ドライバーの記述に使用できるライブラリのセットです。
ms.assetid: 0c07e514-73f9-4d24-86ad-8ac036fdbcf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85b94151a985dfdfa262cfadeaff93b2da70f24e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337791"
---
# <a name="user-mode-driver-framework-frequently-asked-questions"></a>ユーザー モード ドライバー フレームワークについてよく寄せられる質問


Windows Driver Frameworks (WDF) は、Windows オペレーティング システムで実行するデバイス ドライバーの記述に使用できるライブラリのセットです。 WDF では、2 つのフレームワークでサポートされている 1 つのドライバー モデルを定義します。カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF)。 このトピックでは、UMDF についてよく寄せられる質問に対する回答を提供します。

## <a name="which-operating-systems-can-run-umdf-drivers"></a>どのオペレーティング システムでは、UMDF ドライバーを実行できますか。


UMDF ドライバーは、次のオペレーティング システムで実行できます。

-   Windows 10
-   Windows 8.1
-   Windows 8
-   Windows 7
-   Windows Vista
-   Windows XP

## <a name="what-is-the-most-recent-version-of-umdf"></a>UMDF の最新バージョンとは何ですか。


UMDF バージョン 2 (2.0 および 2.1) は、Windows 10 に含まれる以降です。

## <a name="what-is-the-difference-between-umdf-version-2-and-the-previous-version-111-one-dot-eleven"></a>UMDF バージョン 2 と以前のバージョン 1.11 (1 つドット 11) の違いは何ですか。


UMDF バージョン 2 で作成されたドライバーは、C プログラミング言語で記述されます。 この同じドライバーは、kmdf 簡単にコンパイルします。 さらに、COM プログラミング モデルに従って UMDF バージョン 1 のドライバーを記述する必要があります。 

詳細については、次を参照してください。 [UMDF 入門](getting-started-with-umdf-version-2.md)します。

## <a name="which-operating-systems-support-umdf-2"></a>UMDF 2 でサポートされるオペレーティング システムですか。


UMDF ドライバーのバージョン 2 では、Windows 8.1 以降を実行します。

## <a name="which-umdf-versions-can-i-build-against-in-windows-driver-kit-wdk10"></a>UMDF バージョンをビルドできますに対して Windows Driver Kit (WDK) 10 でしょうか。


UMDF 2.1、2.0、1.11、および 1.9 のドライバーを Windows Driver Kit (WDK) 10 と Microsoft Visual Studio を使用して構築できます。 Windows のバージョンに関するこれら UMDF バージョンを使用して構築されたドライバーを実行できるは、次を参照してください。 [UMDF バージョン履歴](umdf-version-history.md)します。

## <a name="can-i-write-part-of-my-driver-to-run-in-user-mode-and-part-in-kernel-mode"></a>カーネル モードでユーザー モードで実行するには、ドライバーの部品と部品を作成しますか。


[はい]。 ドライバーは、いくつかのカーネル モードのリソースや機能へのアクセスを必要とする場合でも、ドライバーを 2 つの部分に分割することがあります。 このアプローチでは、開発およびユーザー モードでドライバーを実行する利点の一部を活用することができます。

UMDF ドライバーでは、カーネル モード ドライバーからの I/O 要求を受信できます。 詳細について*カーネル モードのクライアント*を参照してください[UMDF 2 ドライバーでカーネル モードのクライアントをサポートしている](supporting-kernel-mode-clients-in-umdf-drivers.md)します。

KMDF および UMDF 間の類似性の向上、結果としてただし、ほとんどの場合は必要ドライバーを分割します。

##  <a name="which-framework-should-i-start-with"></a>は、どのフレームワークを開始すべきでしょうか。


かどうかは記載あまり一般的な機能のいずれかのドライバーが必要です[KMDF に UMDF 2 機能を比較する](comparing-umdf-2-0-functionality-to-kmdf.md)KMDF を使用する必要があります。 その他のすべてのドライバーでは、最初の選択肢には、UMDF にしてください。

UMDF で開始し、後で KMDF に移行すること、すれば、最小限の労力で」の説明に従って[KMDF ドライバーを 2 の UMDF ドライバー (およびその逆) に変換する方法について](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)します。

## <a name="how-do-user-mode-drivers-handle-security"></a>ユーザー モード ドライバーは、セキュリティをどのように処理するのでしょうか。


UMDF ドライバーは、LocalService アカウントのセキュリティ資格情報で実行される、ホスト プロセス自体が Windows サービスではないドライバー ホスト プロセスで実行します。 そのため、ユーザー モード ドライバーは、他のユーザー モード サービスとしてセキュリティで保護します。 UMDF ドライバー問題 I/O 要求時に、必要に応じて、クライアント プロセスを偽装できます。 権限借用は、システムは、ドライバーのホスト プロセスではなく、クライアントの id に対してアクセス チェックを実行できるように、クライアントのセキュリティ コンテキストで実行するドライバーのスレッドを使用できます。

ユーザー モード ドライバーでは、I/O の要求に対してのみ、プラグ アンド プレイまたはその他のシステム メッセージではなく、クライアント プロセスを偽装できます。

ドライバーのインストールでは、INF ファイルは、ドライバーの最大の偽装レベルを設定します。 権限借用は、「特権が昇格される」攻撃を防ぐために、最も低いレベルで設定してください。 クライアント アプリケーションを呼び出すと、 **CreateFile**関数、偽装レベルを指定します。 ドライバーは、このレベルの個々 の I/O 要求ごとに偽装を要求します。

## <a name="will-a-user-mode-driver-be-fast-enough"></a>ユーザー モード ドライバーは十分に高速されますか。


パフォーマンスは、UMDF の開発に優先度の高いです。 待機時間と CPU 使用率が若干向上、バスの容量、UMDF でサポートされるデバイスの種類のプライマリ ゲーティング要素です。

## <a name="what-is-the-difference-between-a-user-mode-driver-and-an-application"></a>ユーザー モード ドライバーとアプリケーションの違いは何ですか。


ユーザー モード ドライバーでは、ドライバー マネージャーによって開始され、ドライバーのホスト プロセスで実行されます。 ドライバーの 1 つのインスタンスには、複数のアプリケーションからの同時要求を処理できます。 ドライバーとの通信には、アプリケーションは、Win32 API を使用して、ドライバーのデバイスに I/O 要求を発行します。 ユーザー モード ドライバーの主なエントリ ポイントは、 [ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)インターフェイス (UMDF 1.11 およびそれ以前) または[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)ルーチン (UMDF 2.0 以降) ではなく**main()** 関数。

ドライバーには、I/O 要求とプラグ アンド プレイと電源の通知への応答で、追加のインターフェイスまたは呼び出されるコールバックも含まれます。 UMDF ドライバーによって管理されているデバイスは、システムに統合し、プラグ アンド プレイし、電源管理に参加します。

## <a name="how-do-i-debug-a-umdf-driver"></a>UMDF ドライバーをデバッグする方法は?


UMDF ドライバーは、ユーザー モード デバッガーまたはカーネル モードのデバッガーを使用してデバッグできます。 詳細については、次を参照してください。[デバッグ WDF ドライバー](debugging-a-wdf-driver.md)します。

UMDF バージョン 2.0 以降、ことができますを使用する多くのコマンドで、 *Wdfkd.dll* UMDF ドライバーをデバッグするデバッガー拡張機能ライブラリ。 コマンドの一覧は、次を参照してください。[デバッガー拡張機能](debugger-extensions-for-kmdf-drivers.md)します。 UMDF が UMDF トレース ログを格納するさらに、(または UMDF *IFR*) 非ページ メモリのカーネルにします。 詳細、IFR については、次を参照してください。[フレームワークのイベントのロガーを使用して](using-the-framework-s-event-logger.md)します。

## <a name="is-there-a-newsgroup-for-umdf"></a>UMDF のニュースグループはありますか。


次のフォーラムでの Windows ドライバーのすべての側面のディスカッションをご覧ください。

-   マイクロソフトは、 [Windows ハードウェア WDK とドライバーの開発](http://social.msdn.microsoft.com/Forums/windowsdesktop/home?forum=wdk)フォーラム。

-   システム リソース (OSR) に保ちますを開き、 [OSR オンライン:NTDEV 一覧](http://www.osronline.com/showlists.cfm?list=ntdev)フォーラム。

 

 






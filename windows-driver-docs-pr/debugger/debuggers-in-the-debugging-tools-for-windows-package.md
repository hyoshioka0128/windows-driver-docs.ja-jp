---
title: デバッグ環境
description: Windows Driver Kit (WDK) 8.0 を開始するには、ドライバーの開発環境と Windows デバッガーは Microsoft Visual Studio に統合します。
ms.assetid: 13F9D82A-4C04-425A-A063-B349DB5C8E08
keywords:
- WinDbg
- KD
- CDB
- NTSD
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc765998bf763ac189ab9ddd3618c2b64f30a22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552459"
---
# <a name="debugging-environments"></a>デバッグ環境


Windows Driver Kit (WDK) 8.0 を開始するには、ドライバーの開発環境と Windows デバッガーは Microsoft Visual Studio に統合します。

Visual Studio と WDK をインストールした後は、使用可能な 6 つのデバッグ環境があります。

-   Visual Studio と統合された Windows デバッガー
-   Microsoft Windows デバッガー (WinDbg)
-   マイクロソフト カーネル デバッガー (KD)
-   NTKD
-   Microsoft コンソール デバッガー (CDB)
-   Microsoft NT シンボリック デバッガー (NTSD)

次のセクションでは、デバッグ環境について説明します。

### <a name="span-idvisualstudiowithintegratedwindowsdebuggerspanspan-idvisualstudiowithintegratedwindowsdebuggerspanspan-idvisualstudiowithintegratedwindowsdebuggerspanvisual-studio-with-integrated-windows-debugger"></a><span id="Visual_Studio_with_integrated_Windows_debugger"></span><span id="visual_studio_with_integrated_windows_debugger"></span><span id="VISUAL_STUDIO_WITH_INTEGRATED_WINDOWS_DEBUGGER"></span>Visual Studio と統合された Windows デバッガー

WDK 8.0 以降、ドライバーの開発環境と Windows デバッガーが Visual Studio に統合します。 この統合された環境でのコーディング、構築、する必要があるツールのほとんどをパッケージ化、テスト、デバッグ、およびドライバーの展開がで使用できます、Visual Studio ユーザー インターフェイス。

通常カーネル モードのデバッグには、2 台のコンピューターが必要です。 デバッガーを実行する、*ホスト コンピューター*での実行をデバッグ対象のコードと、*ターゲット コンピューター*します。 Windows デバッガーを Visual Studio に統合して、さまざまなホスト コンピューターから、次の一覧に表示されるものも含め、タスクのデバッグを行うことができます。

-   デバッグのターゲット コンピュータのセットを構成します。
-   ターゲット コンピュータ群にデバッグ接続を構成します。
-   カーネル モードのデバッグ セッションを使用して、ホスト コンピューターと対象コンピューターを起動します。
-   ホスト コンピューター上のユーザー モード プロセスをデバッグします。
-   ターゲット コンピューター上のユーザー モード プロセスをデバッグします。
-   リモート デバッグ セッションに接続します。
-   アセンブリ コードとソース コードを表示します。
-   表示して、ローカル変数、パラメーター、およびその他の記号を操作します。
-   表示し、メモリを操作します。
-   呼び出し履歴を移動します。
-   ブレークポイントを設定します。
-   デバッガー コマンドを実行します。

ドライバーをビルド、ドライバーを展開、および Visual Studio のユーザー インターフェイスからドライバーのテストを実行もできます。 行った場合の Visual Studio の統合を使用して WDK とツールを Windows のデバッグの両方で行うことができますほぼすべてのドライバーの開発、パッケージ化、配置、テスト、およびホスト コンピューター上の Visual Studio 内からタスクをデバッグします。 Visual Studio 統合 WDK の機能の一部を示します。

-   一連のドライバーをテストするためのターゲット コンピューターを構成します。
-   作成し、ドライバー パッケージに署名します。
-   ターゲット コンピューターにドライバー パッケージを展開します。
-   インストールし、ターゲット コンピューター上のドライバーをロードします。
-   ターゲット コンピューター上のドライバーをテストします。

### <a name="span-idwindbgspanspan-idwindbgspanspan-idwindbgspanwindbg"></a><span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>WinDbg

Microsoft Windows デバッガー (WinDbg) は、Windows ベースの強力なデバッガーのユーザー モードとカーネル モードのデバッグの両方に対応しています。 WinDbg では、Windows のカーネル、カーネル モード ドライバー、およびシステムのサービスだけでなくユーザー モード アプリケーションとドライバーのデバッグを提供します。

WinDbg は Visual Studio では、ソース レベルのデバッグのシンボルの書式をデバッグします。 PDB シンボル ファイルがあるモジュールから任意のシンボルまたは変数にアクセスできるし、COFF シンボル ファイル (Windows .dbg ファイルなど) でコンパイルされたモジュールによって公開されるすべてのパブリック関数名にアクセスできます。

WinDbg は、ソース コード、ブレークポイントの設定を表示できます (C++ オブジェクトを含む) の変数、スタック トレース、およびメモリを表示します。 デバッガー コマンド ウィンドウは、さまざまなコマンドを発行するユーザーを使用できます。

カーネル モード デバッグは、WinDbg では、2 台のコンピューター (ホスト コンピューターとターゲット コンピューター) が通常必要です。 WinDbg では、ユーザー モードおよびカーネル モードの両方のターゲットのリモート デバッグのさまざまなオプションもサポートします。

WinDbg では、グラフィカル インターフェイス対応 CDB/NTSD して KD/NTKD です。

### <a name="span-idkdspanspan-idkdspankd"></a><span id="KD"></span><span id="kd"></span>KD

Microsoft Kernel Debugger (KD) とは、NT ベースのすべてのオペレーティング システムのカーネル モードのアクティビティの詳細な分析できるようにする、文字ベースのコンソール プログラムです。 KD がカーネル モード コンポーネントとドライバーをデバッグするか、オペレーティング システム自体の動作の監視に使用できます。 KD では、マルチプロセッサ デバッグもサポートしています。

通常、KD は、デバッグ中のコンピューターでは実行されません。 2 台のコンピューターを作成する必要があります (、*ホスト コンピューター*と*ターゲット コンピューター*) のカーネル モードのデバッグします。

### <a name="span-idntkdspanspan-idntkdspanntkd"></a><span id="NTKD"></span><span id="ntkd"></span>NTKD

という名前の NTKD KD デバッガーのバリエーションがあります。 これは、方法は、点が異なりますが発生する新しいテキスト ウィンドウが起動したら KD が呼び出されたコマンド プロンプト ウィンドウを継承する一方、すべての方法で KD と同じです。

### <a name="span-idcdbspanspan-idcdbspancdb"></a><span id="CDB"></span><span id="cdb"></span>CDB

Microsoft Console Debugger (CDB) とは、低レベルの分析の Windows ユーザー モードのメモリおよび構成体をできるようにする、文字ベースのコンソール プログラムです。 名前*コンソール デバッガー*をという事実を示すために CDB がコンソール アプリケーションとして分類されます。 対象のアプリケーションはコンソール アプリケーションである必要がありますを意味しません。 実際、CDB はコンソール アプリケーションとグラフィカルな Windows プログラムの両方のデバッグの完全な機能です。

CDB が現在実行中またはプログラムをデバッグするために非常に強力な最近のクラッシュ (ライブ分析)、まだセットアップが簡単です。 作業アプリケーションの動作を調査するために使用します。 障害が発生したアプリケーションの場合は、スタック トレースを取得するか、罪のパラメーターを参照する CDB が使用できます。 文字ベースは (リモート アクセス サーバーを使用)、ネットワーク上でも動作します。

Cdb、する表示しプログラム コードを実行、ブレークポイントを設定および確認および変更できますメモリ内の値。 CDB では、それを逆アセンブルし、アセンブリ命令を表示するバイナリ コードを分析できます。 ソース コードは、直接それも分析できます。

CDB が、アドレスまたはグローバル シンボルでメモリの場所にアクセスできるため、参照できますデータと指示するアドレスではなく名前で簡単に検索を特定のセクションのコードをデバッグすること。 CDB では、複数のスレッドとプロセスのデバッグをサポートします。 拡張可能なとできる読み取り/書き込み両方ページ メモリと非ページ メモリ。

ターゲット アプリケーションがコンソール アプリケーションの場合、ターゲットは CDB でコンソール ウィンドウを共有します。 ターゲットのコンソール アプリケーションの個別のコンソール ウィンドウを起動するには、使用、 *-2*コマンド ライン オプション。

### <a name="span-idntsdspanspan-idntsdspanntsd"></a><span id="NTSD"></span><span id="ntsd"></span>NTSD

Microsoft NT ・ Symbolic Debugger (NTSD) という名前の CDB デバッガーのバリエーションがあります。 これは、方法が発生する新しいテキスト ウィンドウ開始されると、一方、CDB が呼び出されたコマンド プロンプト ウィンドウを継承する点を除いて、すべての方法で CDB と同じです。

以降、**開始**コマンドが、新しいコンソール ウィンドウを起動することもでき、次の 2 つの構造は同じ結果になります。

```console
start cdb parameters 
ntsd parameters
```

(Visual Studio や、WinDbg、KD) は、カーネル デバッガーから制御できるように、入力と NTSD (または CDB) からの出力をリダイレクトすることになります。 この手法を使用した場合、NTSD コンソール ウィンドウがない表示されます。 カーネル デバッガーから NTSD を制御するは、非常に軽量なデバッガー、対象のアプリケーションを格納しているコンピューターでほとんどない負担を配置するためにそのため特に役立ちます。 この組み合わせは、システム プロセス、シャット ダウン、および起動の後のステージのデバッグに使用できます。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Windows デバッグ](index.md)

 

 







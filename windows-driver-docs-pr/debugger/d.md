---
title: D (Windows デバッガー用語集)
description: 用語集のページ-D
ms.assetid: e4d53375-c82e-493b-9ccb-444c211fbc79
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75bb2fb885dc151e16a3cca53b646fb4dc356323
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387083"
---
# <a name="d"></a>D


<span id="data_breakpoint"></span><span id="DATA_BREAKPOINT"></span>**データブレークポイント**  
「プロセッサのブレークポイント」を参照してください。

<span id="dbgeng_extension"></span><span id="DBGENG_EXTENSION"></span>**DbgEng 拡張機能**  
Dbgeng .h ヘッダーファイル内のプロトタイプに基づくデバッガー拡張機能。 これらの拡張機能は、デバッガーエンジン API を使用してデバッガーエンジンと通信します。

<span id="debug_build"></span><span id="DEBUG_BUILD"></span>**デバッグビルド**  
確認済みビルドを参照してください。

<span id="debuggee"></span><span id="DEBUGGEE"></span>**デバッガー**  
「ターゲット」を参照してください。

<span id="debugger"></span><span id="DEBUGGER"></span>**デバッガー**  
デバッガーエンジンのすべての機能を使用するデバッガーエンジンアプリケーション。 たとえば、WinDbg、CDB、NTSD、および KD は、デバッガーです。

<span id="debugger_console"></span><span id="DEBUGGER_CONSOLE"></span>**デバッガーコンソール**  
デバッガーエンジン入力のソースと出力の出力先を表す架空のエンティティ。 実際、デバッガーエンジンでは、入力と出力のコールバックのみが使用され、実装に使用されているものの概念はありません。

通常、入力はデバッガーから受信されコマンドウィンドウ、出力は同じウィンドウに送信されます。 ただし、入力と出力のコールバックでは、出力用に他の多くの入力と宛先のソースを提供できます。たとえば、リモート接続、スクリプトファイル、ログファイルなどです。

<span id="debugger_engine"></span><span id="DEBUGGER_ENGINE"></span>**デバッガーエンジン**  
デバッグターゲットを操作するためのライブラリ。 そのインターフェイスは、dbgeng .h ファイルのプロトタイプに基づいています。 これは、デバッガー、拡張機能、およびデバッガーエンジンアプリケーションによって使用されます。

<span id="debugger_engine_api"></span><span id="DEBUGGER_ENGINE_API"></span>**デバッガーエンジン API**  
デバッガーエンジンの動作を制御するための強力なインターフェイス。 これは、デバッガー、DbgEng 拡張機能、およびデバッガーエンジンアプリケーションによって使用される場合があります。 このインターフェイスのプロトタイプは、dbgeng .h ヘッダーファイルにあります。

<span id="debugger_engine_application"></span><span id="DEBUGGER_ENGINE_APPLICATION"></span>**デバッガーエンジンアプリケーション**  
デバッガーエンジン API を使用してデバッガーエンジンを制御するスタンドアロンアプリケーション。

<span id="debugger_extension"></span><span id="DEBUGGER_EXTENSION"></span>**デバッガー拡張機能**  
デバッガー内で実行できる外部関数。 各拡張機能は、デバッガー拡張 DLL と呼ばれるモジュールからエクスポートされます。 デバッガーエンジンは、DLL 内のコードを呼び出すことによって、デバッガー拡張機能を呼び出します。 デバッガー拡張機能には、Windows 用のデバッグツールが付属しています。 独自の拡張機能を作成して、任意の数のデバッガー機能を自動化したり、デバッガーからアクセスできる情報の出力をカスタマイズしたりすることができます。

またはとも呼ばれます。

<span id="debugger_extension_dll"></span><span id="DEBUGGER_EXTENSION_DLL"></span>**デバッガー拡張 DLL**  
デバッガー拡張機能を含む DLL。 デバッガーエンジンによって DLL が読み込まれると、これらの拡張機能はデバッガー内で使用できるようになります。

<span id="debugger_extension_library"></span><span id="DEBUGGER_EXTENSION_LIBRARY"></span>**デバッガー拡張機能ライブラリ**  
「デバッガー拡張 DLL」を参照してください。

<span id="debugging_client"></span><span id="DEBUGGING_CLIENT"></span>**クライアントのデバッグ**  
プロキシとして機能するデバッガーエンジンのインスタンス。デバッガーのコマンドと i/o をデバッグサーバーに送信します。

<span id="debugging_server"></span><span id="DEBUGGING_SERVER"></span>**デバッグサーバー**  
ホストとして動作するデバッガーエンジンのインスタンス。デバッグクライアントからの接続をリッスンします。

<span id="debugging_session"></span><span id="DEBUGGING_SESSION"></span>**デバッグセッション**  
デバッグセッションは、WinDbg、KD、CDB などのソフトウェアデバッグプログラムを実行して、ソフトウェアコンポーネント、システムサービス、アプリケーション、またはオペレーティングシステムをデバッグする実際の動作です。 デバッグセッションは、分析のためにメモリダンプファイルに対して実行することもできます。

がを取得し、すべてのターゲットが破棄されるまで継続すると、デバッグセッションが開始します。

<span id="default_exception_filter"></span><span id="DEFAULT_EXCEPTION_FILTER"></span>**既定の例外フィルター**  
他の例外フィルターと一致しない例外イベントに適用されるイベントフィルター。 既定の例外フィルターは、特定の例外フィルターです。

<span id="dormant_mode"></span><span id="DORMANT_MODE"></span>**休止モード**  
デバッガープログラムが実行されている状態ですが、ターゲットまたはアクティブセッションがありません。

<span id="downstream_store"></span><span id="DOWNSTREAM_STORE"></span>**ダウンストリームストア**  
シンボルサーバーによって作成されたシンボルのキャッシュ。 通常、このキャッシュはローカルコンピューター上にあり、シンボルストアはリモートに配置されます。 シンボルサーバーのチェーンがある場合、ダウンストリームストアは、シンボルストアから下流にある任意のコンピューターに配置できます。

<span id="dump_file"></span><span id="DUMP_FILE"></span>**ダンプファイル**  
「クラッシュダンプファイル」を参照してください。

<span id="dump_target"></span><span id="DUMP_TARGET"></span>**ダンプターゲット**  
デバッグ中のクラッシュダンプファイル。

 

 






---
title: D (Windows デバッガーの用語集)
description: 用語集ページ - D
Robots: noindex, nofollow
ms.assetid: e4d53375-c82e-493b-9ccb-444c211fbc79
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5b5f500adcae7bb675393b346f5d1b777943497
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581884"
---
# <a name="d"></a>D


<span id="data_breakpoint"></span><span id="DATA_BREAKPOINT"></span>**データ ブレークポイント**  
プロセッサのブレークポイントを参照してください。

<span id="dbgeng_extension"></span><span id="DBGENG_EXTENSION"></span>**DbgEng 拡張機能**  
Dbgeng.h ヘッダー ファイルでのプロトタイプに基づいてデバッガー拡張機能。 これらの拡張機能では、デバッガー エンジン API を使用して、デバッガー エンジンと通信します。

<span id="debug_build"></span><span id="DEBUG_BUILD"></span>**デバッグ ビルド**  
チェック ビルドを参照してください。

<span id="debuggee"></span><span id="DEBUGGEE"></span>**デバッグ対象**  
ターゲットを参照してください。

<span id="debugger"></span><span id="DEBUGGER"></span>**デバッガー**  
デバッガー エンジンのすべての機能を使用するデバッガー エンジン アプリケーション。 たとえば、WinDbg、CDB、NTSD、KD、デバッガーとは。

<span id="debugger_console"></span><span id="DEBUGGER_CONSOLE"></span>**デバッガーのコンソール**  
デバッガー エンジンが入力のソースと出力の変換先を表す架空のエンティティ。 実際には、デバッガー エンジンのみ入力を使用してコールバックを出力し、その実装に使用されるものの概念がありません。

通常、デバッガー コマンド ウィンドウから入力を受信し、出力は、同じウィンドウに送信します。 ただし、入力と出力のコールバックでは、入力と出力では、リモート接続、スクリプト ファイル、およびログ ファイルの変換先の他の多くのソースを提供できます。

<span id="debugger_engine"></span><span id="DEBUGGER_ENGINE"></span>**デバッガー エンジン**  
デバッグ ターゲットを操作するためのライブラリです。 そのインターフェイスは、dbgeng.h ファイルでのプロトタイプに基づいています。 使用してデバッガー、拡張機能、およびデバッガー エンジン アプリケーション。

<span id="debugger_engine_api"></span><span id="DEBUGGER_ENGINE_API"></span>**デバッガーのエンジンの API**  
デバッガー エンジンの動作を制御する強力なインターフェイスです。 使用できる、デバッガー、DbgEng 拡張機能、およびデバッガー エンジン アプリケーション。 このインターフェイスのプロトタイプは dbgeng.h ヘッダー ファイル内にあります。

<span id="debugger_engine_application"></span><span id="DEBUGGER_ENGINE_APPLICATION"></span>**デバッガー エンジン アプリケーション**  
デバッガー エンジンを制御するデバッガー エンジン API を使用するスタンドアロン アプリケーションです。

<span id="debugger_extension"></span><span id="DEBUGGER_EXTENSION"></span>**デバッガーの拡張機能**  
デバッガー内部で実行できる外部関数。 各拡張機能は、デバッガーの拡張 DLL として知られるモジュールからエクスポートされます。 デバッガー エンジンは、DLL 内でそのコードを呼び出すことによって、デバッガーの拡張機能を呼び出します。 一部のデバッガー拡張機能は、Windows のツールをデバッグで出荷されます。 任意の数のデバッガー機能を自動化する、またはデバッガーにアクセスできる情報の出力をカスタマイズするには、独自の拡張機能を記述することができます。

別名、または単にします。

<span id="debugger_extension_dll"></span><span id="DEBUGGER_EXTENSION_DLL"></span>**デバッガーの拡張 DLL**  
デバッガーの拡張機能を含む DLL です。 デバッガー エンジン DLL の読み込み時に、デバッガー内で使用可能になるこれらの拡張機能を使用します。

<span id="debugger_extension_library"></span><span id="DEBUGGER_EXTENSION_LIBRARY"></span>**デバッガーの拡張機能ライブラリ**  
デバッガーの拡張 DLL を参照してください。

<span id="debugging_client"></span><span id="DEBUGGING_CLIENT"></span>**クライアントのデバッグ**  
デバッグ サーバーにデバッガー コマンドと I/O を送信し、プロキシとして機能するデバッガー エンジンのインスタンス。

<span id="debugging_server"></span><span id="DEBUGGING_SERVER"></span>**サーバーのデバッグ**  
デバッグ クライアントからの接続をリッスンしている、ホストとして機能するデバッガー エンジンのインスタンス。

<span id="debugging_session"></span><span id="DEBUGGING_SESSION"></span>**デバッグ セッション**  
デバッグ セッションは、実際の操作など WinDbg、KD、CDB、ソフトウェア コンポーネント、システム サービス、アプリケーション、またはオペレーティング システムをデバッグするプログラムをデバッグ ソフトウェアを実行しているのです。 デバッグ セッションは、分析のためのメモリ ダンプ ファイルに対しても実行できます。

デバッグ セッションは、取得、し、すべてのターゲットが破棄されたまで続きます。

<span id="default_exception_filter"></span><span id="DEFAULT_EXCEPTION_FILTER"></span>**既定の例外フィルター**  
その他の例外のフィルターと一致しない例外イベントに適用されるイベント フィルターです。 既定の例外フィルターは、特定の例外フィルターです。

<span id="dormant_mode"></span><span id="DORMANT_MODE"></span>**休止モード**  
ターゲットまたはアクティブなセッションをせずに、デバッガーのプログラムが実行されている状態。

<span id="downstream_store"></span><span id="DOWNSTREAM_STORE"></span>**ダウン ストリームのストア**  
シンボル サーバーによって作成されるシンボルのキャッシュです。 通常このキャッシュは、シンボル ストアがリモートに配置中に、ローカル コンピューターには。 シンボル サーバーのチェーンがある場合は場合、は、シンボル ストアから下流にあるコンピューターで、ダウン ストリームのストアを配置することができます。

<span id="dump_file"></span><span id="DUMP_FILE"></span>**ダンプ ファイル**  
クラッシュ ダンプ ファイルを参照してください。

<span id="dump_target"></span><span id="DUMP_TARGET"></span>**ダンプ ターゲットについて**  
デバッグ中にあるクラッシュ ダンプ ファイル。

 

 






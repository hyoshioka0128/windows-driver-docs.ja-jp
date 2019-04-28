---
title: デバッガー エンジンの基本
description: デバッガー エンジンの基本
ms.assetid: fa52a1f0-9397-48a5-acbd-ce5347c0baef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 885969afbd5699e9f3652d33076d89b9aa4ebdd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367224"
---
# <a name="debugger-engine-introduction"></a>デバッガー エンジンの基本

このドキュメントでは、WinDbg、KD、CDB、NTSD で実行される拡張機能を記述する方法と、デバッガー エンジンを使用する方法について説明します。 ユーザー モードまたはカーネル モードの Microsoft Windows のデバッグを実行するときに、これらのデバッガー拡張機能を使用できます。

### <a name="span-iddebugger-enginespandebugger-engine"></a><span id="debugger-engine"></span>デバッガー エンジン

デバッガー エンジンでは、調べることと、ユーザー モードと Microsoft Windows のカーネル モードでデバッグ ターゲットを操作するためのインターフェイスを提供します。

デバッガー エンジンできますターゲットを取得、ブレークポイントを設定、イベントを監視、シンボルにクエリを実行、読み取りおよび書き込みメモリ、およびコントロールのスレッドとプロセスをターゲットにします。

デバッガー エンジンを使用して、デバッガーの拡張機能ライブラリとスタンドアロン アプリケーションの両方を記述することができます。 このようなアプリケーションは*エンジン アプリケーションのデバッガー*します。 デバッガー エンジンのすべての機能を使用するデバッガー エンジン アプリケーションは、*デバッガー*します。 たとえば、WinDbg、CDB、NTSD、および KD はデバッガーです。デバッガー エンジンは、その機能のコアを提供します。

デバッガー エンジン API は、ヘッダー ファイルの dbgeng.h でプロトタイプによって指定されます。

### <a name="incomplete-documentation"></a>不完全なドキュメント

これは、ドキュメントは暫定版と、完全ではありません。

ここでまだ記載されていないのデバッガーとデバッガー エンジンに関連する多く概念の参照、[のデバッグ技術](debugging-techniques.md)このドキュメントの「します。

デバッガー エンジン API の現在文書化されていない機能の一部を取得するには、使用、 [ **Execute** ](https://msdn.microsoft.com/library/windows/hardware/ff543208)個々 のデバッガー コマンドを実行するメソッド。

### <a name="span-idextensionsspanspan-idextensionsspanextensions"></a><span id="extensions"></span><span id="EXTENSIONS"></span>拡張機能

拡張 DLL のビルドを作成して、独自のデバッグ コマンドを作成できます。 たとえば、複雑なデータ構造を表示する、拡張機能コマンド記述する可能性があります。

デバッガーの拡張 Dll の 3 つの異なる種類があります。

-   *DbgEng 拡張 Dll*します。 これらは、dbgeng.h ヘッダー ファイルでのプロトタイプに基づいています。 この型の各 DLL には、DbgEng 拡張機能のコマンドをエクスポートできます。 これらの拡張機能コマンドでは、デバッガー エンジン API を使用し、WdbgExts API を使用することもできます。

-   *EngExtCpp 拡張 Dll*します。 これらは、engextcpp.h と dbgeng.h ヘッダー ファイルでのプロトタイプに基づいています。 この型の各 DLL には、DbgEng 拡張機能のコマンドをエクスポートできます。 これらの拡張機能コマンドでは、デバッガー エンジン API と、EngExtCpp 拡張フレームワークの両方を使用し、WdbgExts API を使用することもできます。

-   *WdbgExts 拡張 Dll*します。 これらは、wdbgexts.h ヘッダー ファイルでのプロトタイプに基づいています。 この型の各 DLL は、1 つまたは複数の WdbgExts 拡張機能のコマンドをエクスポートします。 これらの拡張機能コマンドでは、排他的 WdbgExts API を使用します。

拡張機能またはスタンドアロンのアプリケーションを作成する DbgEng API を使用できます。 WdbgExts API では、デバッガー エンジン API の機能のサブセットが含まれており、拡張機能でのみ使用できます。

すべてのデバッガー拡張機能はコンパイルされ、ビルド ユーティリティを使用して構築する必要があります。 ビルド ユーティリティは、Windows Driver Kit (WDK) で含まれています。

カスタム インストールを実行し、選択した場合、Windows のツールをデバッグ パッケージの一部として拡張機能のコード サンプルがインストールされて、 **SDK**コンポーネントとそのすべてのサブコンポーネントです。 Sdk で見つかります\\サンプルの Windows 内のデバッグ ツールのインストール ディレクトリのサブディレクトリ。

デバッガーの新しい拡張機能を記述する最も簡単な方法では、サンプル拡張機能を学習します。 各拡張機能サンプルにはメイクファイルが含まれていて、ビルド ユーティリティでのソース ファイルを使用します。 サンプルでは、両方の種類の拡張機能が表されます。

## <a name="span-idwritingcustomanalysisdebuggerextensionsspanspan-idwritingcustomanalysisdebuggerextensionsspanspan-idwritingcustomanalysisdebuggerextensionsspanwriting-custom-analysis-debugger-extensions"></a><span id="Writing_Custom_Analysis_Debugger_Extensions"></span><span id="writing_custom_analysis_debugger_extensions"></span><span id="WRITING_CUSTOM_ANALYSIS_DEBUGGER_EXTENSIONS"></span>カスタム分析デバッガー拡張機能の作成


機能を拡張することができます、 [ **! 分析**](-analyze.md)分析の拡張機能プラグインを記述することでデバッガー コマンド。 分析の拡張機能プラグインを提供するには、によっては、バグ チェックや、独自のコンポーネントまたはアプリケーションに固有の方法での例外の解析に参加できます。 分析の拡張機能プラグインを記述するときに、呼び出されるプラグインの対象となる状況を説明するメタデータ ファイルを記述します。 ときに **! 分析**実行されると、検索、読み込み、および適切な分析の拡張機能プラグインを実行します。 詳細については、次を参照してください[カスタム分析デバッガー拡張機能の作成。](writing-custom-analysis-debugger-extensions.md)

## <a name="span-idcustomizingdebuggeroutputusingdmlspanspan-idcustomizingdebuggeroutputusingdmlspanspan-idcustomizingdebuggeroutputusingdmlspancustomizing-debugger-output-using-dml"></a><span id="Customizing_Debugger_Output_Using_DML"></span><span id="customizing_debugger_output_using_dml"></span><span id="CUSTOMIZING_DEBUGGER_OUTPUT_USING_DML"></span>DML を使用して出力をデバッガーのカスタマイズ


DML を使用して出力をデバッガーをカスタマイズすることができます。 詳細については、次を参照してください。 [DML を使用してデバッガーの出力のカスタマイズ](customizing-debugger-output-using-dml.md)します。

## <a name="span-idjavascriptspanspan-idjavascriptspanspan-idjavascriptspanusing-javascript-to-extend-the-capabilities-of-the-debugger"></a><span id="JavaScript"></span><span id="javascript"></span><span id="JAVASCRIPT"></span>JavaScript を使用して、デバッガーの機能を拡張するには


デバッガー オブジェクトについて理解し、拡張、およびデバッガーの機能をカスタマイズするスクリプトを作成するのにには、JavaScript を使用します。 JavaScript のプロバイダーは、デバッガーの内部オブジェクト モデルへのスクリプト言語をブリッジします。 プロバイダー、スクリプト、JavaScript デバッガーを使うと、デバッガーでの JavaScript の使用。 詳細については、次を参照してください。 [JavaScript デバッガー Scripting](javascript-debugger-scripting.md)します。

 

 






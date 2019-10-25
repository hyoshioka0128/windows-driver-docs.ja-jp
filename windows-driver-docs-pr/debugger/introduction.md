---
title: デバッガー エンジンの基本
description: デバッガー エンジンの基本
ms.assetid: fa52a1f0-9397-48a5-acbd-ce5347c0baef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8f9de13e52cd6f5d717ccf9ad814df259eac7a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826370"
---
# <a name="debugger-engine-introduction"></a>デバッガー エンジンの基本

このドキュメントでは、デバッガーエンジンを使用する方法と、WinDbg、KD、CDB、NTSD で実行される拡張機能を記述する方法について説明します。 これらのデバッガー拡張機能は、Microsoft Windows でユーザーモードまたはカーネルモードのデバッグを実行するときに使用できます。

### <a name="span-iddebugger-enginespandebugger-engine"></a><span id="debugger-engine"></span>デバッガーエンジン

デバッガーエンジンには、Microsoft Windows のユーザーモードとカーネルモードでデバッグ対象を調べて操作するためのインターフェイスが用意されています。

デバッガーエンジンでは、ターゲットの取得、ブレークポイントの設定、イベントの監視、シンボルの照会、メモリの読み取りと書き込み、およびターゲットのスレッドとプロセスの制御を行うことができます。

デバッガーエンジンを使用して、デバッガー拡張ライブラリとスタンドアロンアプリケーションの両方を記述できます。 このようなアプリケーションは、*デバッガーエンジンアプリケーション*です。 デバッガーエンジンのすべての機能を使用するデバッガーエンジンアプリケーションは、*デバッガー*です。 たとえば、WinDbg、CDB、NTSD、および KD は、デバッガーです。デバッガーエンジンには、その機能の中核となる機能が用意されています。

デバッガーエンジン API は、ヘッダーファイル dbgeng. h 内のプロトタイプによって指定されます。

### <a name="incomplete-documentation"></a>不完全なドキュメント

このドキュメントは暫定版であり、現在は不完全です。

ここでまだ説明されていないデバッガーとデバッガーエンジンに関連する多くの概念については、このドキュメントの「[デバッグ技術](debugging-techniques.md)」セクションを参照してください。

デバッガーエンジン API の現在ドキュメントに記載されていない機能の一部を取得するには、 [**execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute)メソッドを使用して個々のデバッガーコマンドを実行します。

### <a name="span-idextensionsspanspan-idextensionsspanextensions"></a><span id="extensions"></span><span id="EXTENSIONS"></span>補助

拡張 DLL を作成してビルドすることによって、独自のデバッグコマンドを作成できます。 たとえば、複雑なデータ構造を表示する拡張コマンドを記述することができます。

デバッガー拡張 Dll には、次の3種類があります。

-   *Dbgeng 拡張 dll*。 これらは、dbgeng .h ヘッダーファイル内のプロトタイプに基づいています。 この型の各 DLL は、DbgEng 拡張コマンドをエクスポートできます。 これらの拡張コマンドでは、デバッガーエンジン API を使用します。また、WdbgExts API を使用することもできます。

-   *EngExtCpp 拡張 dll*。 これらは、engextcpp ヘッダーファイルと dbgeng .h ヘッダーファイル内のプロトタイプに基づいています。 この型の各 DLL は、DbgEng 拡張コマンドをエクスポートできます。 これらの拡張コマンドでは、デバッガーエンジン API と EngExtCpp extension フレームワークの両方を使用します。また、WdbgExts API を使用することもできます。

-   *Wdbgexts 拡張 dll*。 これらは、wdbgexts ヘッダーファイル内のプロトタイプに基づいています。 この型の各 DLL は、1つ以上の WdbgExts 拡張コマンドをエクスポートします。 これらの拡張コマンドでは、WdbgExts API のみを使用します。

DbgEng API を使用して、拡張機能またはスタンドアロンアプリケーションを作成できます。 WdbgExts API には、デバッガーエンジン API の機能のサブセットが含まれており、拡張機能でのみ使用できます。

すべてのデバッガー拡張機能は、ビルドユーティリティを使用してコンパイルおよびビルドする必要があります。 ビルドユーティリティは、Windows Driver Kit (WDK) に含まれています。

カスタムインストールを実行し、 **SDK**コンポーネントとそのすべてのサブコンポーネントを選択した場合、拡張コードサンプルは Windows パッケージのデバッグツールの一部としてインストールされます。 これらは、Windows 用デバッグツールのインストールディレクトリの sdk\\samples サブディレクトリにあります。

新しいデバッガー拡張機能を記述する最も簡単な方法は、サンプルの拡張機能を調べることです。 各サンプル拡張機能には、ビルドユーティリティで使用するメイクファイルとソースファイルが含まれています。 両方の種類の拡張機能は、サンプルで表現されています。

## <a name="span-idwriting_custom_analysis_debugger_extensionsspanspan-idwriting_custom_analysis_debugger_extensionsspanspan-idwriting_custom_analysis_debugger_extensionsspanwriting-custom-analysis-debugger-extensions"></a><span id="Writing_Custom_Analysis_Debugger_Extensions"></span><span id="writing_custom_analysis_debugger_extensions"></span><span id="WRITING_CUSTOM_ANALYSIS_DEBUGGER_EXTENSIONS"></span>カスタム分析デバッガー拡張機能の作成


Analysis extension プラグインを記述することで、 [ **! analyze**](-analyze.md)デバッガーコマンドの機能を拡張できます。 分析拡張機能プラグインを提供することにより、独自のコンポーネントまたはアプリケーションに固有の方法で、バグチェックまたは例外の分析に参加できます。 分析拡張機能プラグインを記述するときは、プラグインを呼び出す状況を記述したメタデータファイルも記述します。 **! Analyze**を実行すると、適切な分析拡張機能プラグインが検索、読み込み、および実行されます。 詳細については、「[カスタム分析デバッガー拡張機能の記述](writing-custom-analysis-debugger-extensions.md)」を参照してください。

## <a name="span-idcustomizing_debugger_output_using_dmlspanspan-idcustomizing_debugger_output_using_dmlspanspan-idcustomizing_debugger_output_using_dmlspancustomizing-debugger-output-using-dml"></a><span id="Customizing_Debugger_Output_Using_DML"></span><span id="customizing_debugger_output_using_dml"></span><span id="CUSTOMIZING_DEBUGGER_OUTPUT_USING_DML"></span>DML を使用したデバッガー出力のカスタマイズ


DML を使用して、デバッガーの出力をカスタマイズできます。 詳細については、「 [DML を使用したデバッガー出力のカスタマイズ](customizing-debugger-output-using-dml.md)」を参照してください。

## <a name="span-idjavascriptspanspan-idjavascriptspanspan-idjavascriptspanusing-javascript-to-extend-the-capabilities-of-the-debugger"></a><span id="JavaScript"></span><span id="javascript"></span><span id="JAVASCRIPT"></span>JavaScript を使用したデバッガーの機能の拡張


JavaScript を使用して、デバッガーオブジェクトを理解し、デバッガーの機能を拡張およびカスタマイズするスクリプトを作成します。 JavaScript プロバイダーは、スクリプト言語をデバッガーの内部オブジェクトモデルにブリッジします。 JavaScript デバッガースクリプトプロバイダーは、デバッガーで JavaScript を使用できるようにします。 詳細については、「 [JavaScript デバッガースクリプト](javascript-debugger-scripting.md)」を参照してください。

 

 






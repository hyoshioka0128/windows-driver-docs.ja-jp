---
title: DoTraceMessage をカスタマイズできますか。
description: DoTraceMessage をカスタマイズできますか。
ms.assetid: 4c5c4990-6095-4ab8-a20b-7597b3169f52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98de0b66328d05b42d22e86ad61d8209fc9c5fc8
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769444"
---
# <a name="can-i-customize-dotracemessage"></a>DoTraceMessage をカスタマイズできますか?


はい、独自のバージョンの[**DoTraceMessage**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロを作成することができます。 DoTraceMessage は、トレースメッセージを生成します。

[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)サンプルドライバーは、このトピックで説明されているメソッドの例を示しています。 [Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

### <a name="span-iddotracemessage__default_versionspanspan-iddotracemessage__default_versionspandotracemessage-default-version"></a><span id="dotracemessage__default_version"></span><span id="DOTRACEMESSAGE__DEFAULT_VERSION"></span>DoTraceMessage: 既定のバージョン

既定では、DoTraceMessage マクロの形式は次のとおりです。

```
DoTraceMessage(Flag,"Message",MessageVariables...);
```

この既定のバージョンでは、*フラグ*は[トレースフラグ](trace-flags.md)を表します。これは、メッセージが生成される条件です。 *MessageVariables*には、ドライバーが定義し、トレースメッセージに表示される変数のコンマ区切りリストが含まれています。 *MessageVariables*変数は、 **printf**要素を使用して書式設定されます。 WPP プリプロセッサは、DoTraceMessage マクロからコンパイラディレクティブを作成します。 このマクロは、[トレースプロバイダー](trace-provider.md)用に生成された PDB ファイル (カーネルモードドライバーやユーザーモードアプリケーションなど) に、メッセージ定義情報と書式情報を追加します。

DoTraceMessage マクロは、論理的には次のように展開されます。

```
PRE macro // If defined
If (WPP_CHECK_INIT && Flag is enabled) {
 ....Call WmiTraceMessage;
}
POST macro // If defined
```

次のコード例について考えます。

```
DoTraceMessage(ERROR, "IOCTL = %d", ControlCode);
```

この呼び出しは、エラーフラグが有効になっている場合にトレースメッセージを生成します。 メッセージは "IOCTL =% d" で、 *MessageVariables*は*controlcode*の値です。

ログ前とログ後のマクロが定義されている場合は、それらも展開されます。 PRE マクロと POST マクロは、Microsoft Windows 2000 以降のオペレーティングシステムでサポートされています。 マクロを使用するには、WDK を使用してドライバーをビルドする必要があります。 以前のバージョンの Windows Driver Development Kit (DDK) を使用してドライバーをビルドする場合、PRE および POST 機能は使用できず、マクロはトレースステートメントの一部として実行されません。 以前のバージョンの Windows DDK を使用してドライバーをビルドすると、ビルドの中断が発生しない可能性がありますが、コードは想定どおりに動作しません。

### <a name="span-iddotracemessage__general_formatspanspan-iddotracemessage__general_formatspandotracemessage-general-format"></a><span id="dotracemessage__general_format"></span><span id="DOTRACEMESSAGE__GENERAL_FORMAT"></span>DoTraceMessage: 一般形式

有効なトレースメッセージ関数の一般的な形式を次に示します。

```
FunctionName(Conditions...,"Message",MessageVariables...);
```

メッセージの前に表示されるパラメーターは、条件として解釈されます。 メッセージの後に表示されるパラメーターは、メッセージ変数として解釈されます。

*条件*は、コンマで区切られた値の一覧です。 トレースメッセージは、すべての条件が true の場合にのみ生成されます。 コードでサポートされている任意の条件を指定できます。

### <a name="span-idexample__mytracespanspan-idexample__mytracespanexample-mytrace"></a><span id="example__mytrace"></span><span id="EXAMPLE__MYTRACE"></span>例: MyTrace

トレース関数の例を次に示します。 この例では、トレースメッセージを生成しているプロバイダーのトレースレベルおよびサブコンポーネントの条件を追加します。

```
MyDoTrace(Level, Flag, Subcomponent,"Message",MessageVariables...);
```

次に例を示します。

```
MyDoTrace(TRACE_LEVEL_ERROR, VERBOSE, Network,"IOCTL = %d", ControlCode);
```

トレースレベルは、Evntrace で定義されている標準レベルです。これは、WDK の Include サブディレクトリにあるパブリックヘッダーファイルです。

```
#define TRACE_LEVEL_NONE        0   // Tracing is not on
#define TRACE_LEVEL_FATAL       1   // Abnormal exit or termination
#define TRACE_LEVEL_ERROR       2   // Severe errors that need logging
#define TRACE_LEVEL_WARNING     3   // Warnings such as allocation failure
#define TRACE_LEVEL_INFORMATION 4   // Includes non-error cases(for example, Entry-Exit)
#define TRACE_LEVEL_VERBOSE     5   // Detailed traces from intermediate steps
#define TRACE_LEVEL_RESERVED6   6
#define TRACE_LEVEL_RESERVED7   7
#define TRACE_LEVEL_RESERVED8   8
#define TRACE_LEVEL_RESERVED9   9
```

### <a name="span-idhow_to_create_a_custom_tracing_functionspanspan-idhow_to_create_a_custom_tracing_functionspanhow-to-create-a-custom-tracing-function"></a><span id="how_to_create_a_custom_tracing_function"></span><span id="HOW_TO_CREATE_A_CUSTOM_TRACING_FUNCTION"></span>カスタムトレース関数を作成する方法

カスタムトレース関数を作成するには、次の手順を実行します。

-   DoTraceMessage マクロをサポートする別のバージョンのマクロを記述します。

-   WPP プリプロセッサを呼び出す RUN WPP ステートメントに **-func**パラメーターを追加し \_ ます。

### <a name="span-idwrite_custom_macrosspanspan-idwrite_custom_macrosspanwrite-custom-macros"></a><span id="write_custom_macros"></span><span id="WRITE_CUSTOM_MACROS"></span>カスタムマクロを記述する

トレースメッセージの条件 (メッセージの前に表示されるパラメーター) を変更するカスタムトレース関数を作成するには、のトレース関数、 **wpp \_ レベル \_ ENABLED** 、および**wpp \_ レベル \_ ロガー**をサポートする別のバージョンのマクロを記述する必要があります。

-   **WPP \_レベル \_ enabled (*Flags*)** は、指定されたフラグ値を使用してログ記録を有効にするかどうかを決定します。 **TRUE**または**FALSE**が返されます。

-   **WPP \_LEVEL \_ LOGGER (*Flags*)** は、プロバイダーが有効になっているトレースセッションを検索し、トレースセッションへのハンドルを返します。

たとえば、トレースレベルをフラグだけでなく条件として含める場合は、 \_ トレースレベルを含む新しい WPP レベル有効マクロを定義し \_ ます。 次のコード例に示すように、既定のマクロで新しいマクロの定義を基にすることができます。

```
#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >=lvl
```

通常、WPP \_ レベルの \_ LOGGER マクロは影響を受けません。 このような場合は、新しいマクロを既定のマクロとして定義できます。 次に例を示します。

```
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) WPP_LEVEL_LOGGER(flags)
```

ただし、場合によっては、LOGGER マクロを変更する必要があります。 たとえば、フラグではなくトレースレベルのみに依存するトレース関数を記述することができます。

次のコード例では、マクロの flags 値がダミーの値に置き換えられています。 コントロールの GUID 定義を宣言するときに、フラグが定義されていません。

```
#define WPP_CONTROL_GUIDS \
   WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(DUMMY))
```

```
#define WPP_LEVEL_LOGGER(lvl) (WPP_CONTROL(WPP_BIT_ ## DUMMY).Logger)
```

### <a name="span-idadd_the_function_to_wppspanspan-idadd_the_function_to_wppspanadd-the-function-to-wpp"></a><span id="add_the_function_to_wpp"></span><span id="ADD_THE_FUNCTION_TO_WPP"></span>WPP に関数を追加する

カスタムトレース関数を WPP に追加するには、次のコード例に示すように、関数の宣言を使用して **-func**パラメーターを RUN wpp ステートメントに追加し \_ ます。

```
RUN_WPP=$(SOURCES) -km -func:DoTraceLevelMessage(LEVEL,FLAGS,MSG,...)
```

**メモ** **-km** \_ ユーザーモードアプリケーションまたはダイナミックリンクライブラリ (dll) の場合は、実行 WPP ディレクティブで-km スイッチを指定しないでください。



実行 wpp のオプションパラメーターの完全な一覧につい \_ ては、「 [Wpp プリプロセッサ](wpp-preprocessor.md)」を参照してください。










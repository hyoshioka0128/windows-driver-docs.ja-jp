---
title: DoTraceMessage をカスタマイズできます。
description: DoTraceMessage をカスタマイズできます。
ms.assetid: 4c5c4990-6095-4ab8-a20b-7597b3169f52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63dbeae90a2de439ad3f26d58ef95bc0e6dfe139
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371626"
---
# <a name="can-i-customize-dotracemessage"></a>DoTraceMessage をカスタマイズできますか?


はい、独自のバージョンを書き込むことができます、 [ **DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))マクロ。 DoTraceMessage では、トレース メッセージを生成します。

[TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)サンプル ドライバーは、このトピックで説明されているメソッドの例を示します。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)で使用できるは、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

### <a name="span-iddotracemessagedefaultversionspanspan-iddotracemessagedefaultversionspandotracemessage-default-version"></a><span id="dotracemessage__default_version"></span><span id="DOTRACEMESSAGE__DEFAULT_VERSION"></span>DoTraceMessage:既定のバージョン

既定では、DoTraceMessage マクロは、次の形式があります。

```
DoTraceMessage(Flag,"Message",MessageVariables...);
```

この既定のバージョンで*フラグ*を表す、[トレース フラグ](trace-flags.md)、これは、メッセージを生成する条件。 *MessageVariables*ドライバーを定義し、トレース メッセージに表示される変数のコンマ区切りの一覧が含まれています。 *MessageVariables*変数を使用して書式設定、 **printf**要素。 プリプロセッサ WPP DoTraceMessage マクロからコンパイラ ディレクティブを作成します。 このマクロが生成された PDB ファイルにメッセージ定義の情報と書式設定情報を追加、[トレース プロバイダー](trace-provider.md)、カーネル モード ドライバーまたはユーザー モード アプリケーションなどです。

DoTraceMessage マクロを展開すると論理的には、次のようにします。

```
PRE macro // If defined
If (WPP_CHECK_INIT && Flag is enabled) {
 ....Call WmiTraceMessage;
}
POST macro // If defined
```

次のコード例を検討してください。

```
DoTraceMessage(ERROR, "IOCTL = %d", ControlCode);
```

この呼び出しは、エラー フラグが有効にすると、トレース メッセージを生成します。 メッセージが"IOCTL = %d"および*MessageVariables*の値である*ControlCode*します。

前のログ記録と後のログ記録のマクロが定義されている場合も展開されます。 前のマクロと POST のマクロは、Microsoft Windows 2000 以降のオペレーティング システムでサポートされます。 マクロを使用するには、WDK を使用して、ドライバーをビルドする必要があります。 以前のバージョンの Windows ドライバー開発キット (DDK) を使用してドライバーをビルドする場合は、事前/事後の機能が使用できないと、トレース ステートメントの一部として、マクロは実行されません。 以前のバージョンの Windows DDK を使用して、ドライバーをビルドしても、ビルド ブレーク可能性がありますされませんが、コードは、期待どおりに機能しません。

### <a name="span-iddotracemessagegeneralformatspanspan-iddotracemessagegeneralformatspandotracemessage-general-format"></a><span id="dotracemessage__general_format"></span><span id="DOTRACEMESSAGE__GENERAL_FORMAT"></span>DoTraceMessage:一般的な形式

有効なトレース メッセージの関数の一般的な形式を次に示します。

```
FunctionName(Conditions...,"Message",MessageVariables...);
```

メッセージの前に表示されるパラメーターは、条件として解釈されます。 メッセージの後に表示されるパラメーターは、メッセージ変数として解釈されます。

*条件*値のコンマ区切りの一覧です。 すべての条件に該当する場合にのみ、トレース メッセージが生成されます。 コードでサポートされている任意の条件を指定することができます。

### <a name="span-idexamplemytracespanspan-idexamplemytracespanexample-mytrace"></a><span id="example__mytrace"></span><span id="EXAMPLE__MYTRACE"></span>例: MyTrace

トレース機能のサンプルを次に示します。 この例では、トレース レベルおよびトレース メッセージが生成されているプロバイダーのサブコンポーネントの条件を追加します。

```
MyDoTrace(Level, Flag, Subcomponent,"Message",MessageVariables...);
```

例:

```
MyDoTrace(TRACE_LEVEL_ERROR, VERBOSE, Network,"IOCTL = %d", ControlCode);
```

トレース レベルは、Evntrace.h、WDK のインクルードのサブディレクトリ内にあるパブリック ヘッダー ファイルで定義されている標準的なレベルです。

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

### <a name="span-idhowtocreateacustomtracingfunctionspanspan-idhowtocreateacustomtracingfunctionspanhow-to-create-a-custom-tracing-function"></a><span id="how_to_create_a_custom_tracing_function"></span><span id="HOW_TO_CREATE_A_CUSTOM_TRACING_FUNCTION"></span>カスタム関数のトレースを作成する方法

カスタム トレース関数を作成するには、次の手順を実行します。

-   別のバージョンの DoTraceMessage マクロをサポートするマクロを記述します。

-   追加、 **- func** 、実行するようにパラメーター\_WPP プリプロセッサを呼び出す WPP ステートメント。

### <a name="span-idwritecustommacrosspanspan-idwritecustommacrosspanwrite-custom-macros"></a><span id="write_custom_macros"></span><span id="WRITE_CUSTOM_MACROS"></span>カスタムのマクロを作成します。

トレース メッセージ (メッセージの前に表示されるパラメーター) の条件を変更するカスタム トレース関数を作成するには、トレース機能をサポートするマクロの代替バージョンを記述する必要があります**WPP\_レベル\_有効になっている**と**WPP\_レベル\_ロガー**します。

-   **WPP\_レベル\_有効 (*フラグ*)** 指定したフラグ値でログ記録が有効になっているかどうかを決定します。 返します**TRUE**または**FALSE**します。

-   **WPP\_レベル\_ロガー (*フラグ*)** 検索トレース セッションをプロバイダーが有効になり、トレース セッション ハンドルを返します。

たとえば、トレース レベル、フラグ、だけでなく、条件として追加する場合は、定義新しい WPP\_レベル\_トレース レベルを含むマクロを有効にします。 次のコード例に示すように既定の macro 新しいマクロの定義を作成できます。

```
#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >=lvl
```

通常、WPP\_レベル\_ロガー マクロが影響を受けません。 このような場合は、既定のマクロを使用する新しいマクロを定義できます。 次に、例を示します。

```
#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) WPP_LEVEL_LOGGER(flags)
```

ただし、場合によっては、ロガーのマクロを変更する必要があります。 たとえば、フラグではなくトレース レベルにのみ依存するトレース関数を記述する可能性があります。

次のコード例で、マクロ内のフラグの値は、ダミーの値に置換されます。 コントロールの GUID 定義を宣言するときに、フラグは定義されていません。

```
#define WPP_CONTROL_GUIDS \
   WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(DUMMY))
```

```
#define WPP_LEVEL_LOGGER(lvl) (WPP_CONTROL(WPP_BIT_ ## DUMMY).Logger)
```

### <a name="span-idaddthefunctiontowppspanspan-idaddthefunctiontowppspanadd-the-function-to-wpp"></a><span id="add_the_function_to_wpp"></span><span id="ADD_THE_FUNCTION_TO_WPP"></span>WPP に関数を追加します。

WPP には、カスタム トレース機能を追加するには、追加、 **- func** 、実行するようにパラメーター\_WPP ステートメントは、次のコード例として、関数の宣言を示しています。

```
RUN_WPP=$(SOURCES) -km -func:DoTraceLevelMessage(LEVEL,FLAGS,MSG,...)
```

**注**するを指定する必要があります、 **km**実行の切り替え\_WPP ディレクティブのユーザー モード アプリケーションまたはダイナミック リンク ライブラリ (Dll)。



実行の省略可能なパラメーターの完全な一覧については\_WPP を参照してください[WPP プリプロセッサ](wpp-preprocessor.md)します。










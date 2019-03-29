---
title: 追加する方法はプレフィックスとサフィックスにトレース メッセージ
description: 追加する方法はプレフィックスとサフィックスにトレース メッセージ
ms.assetid: d8cd0a90-d020-4b1e-bec1-7d920964169e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e6c99def3fd22b8a4f8ef2733a6785022c11491
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580777"
---
# <a name="how-do-i-add-a-prefix-and-suffix-to-a-trace-message"></a>トレース メッセージにプレフィックスとサフィックスを追加する方法


使用することができます、 [WPP プリプロセッサ](wpp-preprocessor.md)データ トレース メッセージを追加する構成ブロック。

によって、WPP 構成ブロックが定義されている、**開始\_wpp config**と**エンド\_wpp**ソース コード内に配置するステートメント。

**//begin\_wpp config**

...

*構成ブロック*

...

**//end\_wpp**

ヘッダー ファイルで構成データを配置する場合は、プロジェクトのプロパティ、ヘッダー ファイルの名前を指定 (の**WPP トレース**)。 [**ファイル オプション**プロパティ] ページで、指定、**スキャンの構成ファイル**します。 参照してください[WPP プリプロセッサ](wpp-preprocessor.md)詳細についてはします。

### <a name="span-idconfigurationblocksyntaxspanspan-idconfigurationblocksyntaxspanconfiguration-block-syntax"></a><span id="configuration_block_syntax"></span><span id="CONFIGURATION_BLOCK_SYNTAX"></span>構成ブロックの構文

<span id="__USEPREFIX__Function_Name___Format_string___"></span><span id="__useprefix__function_name___format_string___"></span><span id="__USEPREFIX__FUNCTION_NAME___FORMAT_STRING___"></span>**USEPREFIX (**<em>関数\_名前</em>**、"**<em>書式指定文字列</em>**");**  
イベントが記録されたときに使用する形式の文字列のプレフィックスを定義します。 最初のパラメーターは、このプレフィックスを適用する関数の名前です。 2 番目のパラメーターは、使用する書式指定文字列です。 既定値を使用するには、% を指定します。STDPREFIX です。 既定のトレース メッセージのプレフィックスは、CPU の数、プロセス ID、スレッド ID、世界協定時刻 (UTC) 形式のタイムスタンプ、およびコントロールの GUID のフレンドリ名を指定します。

```
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
```

<span id="__FUNC_Function_Name_args__EXP__"></span><span id="__func_function_name_args__exp__"></span><span id="__FUNC_FUNCTION_NAME_ARGS__EXP__"></span>**FUNC** *関数\_名前*{*args*} (EXP)**;**  
名前とトレース関数のシグネチャを定義します。 中かっこ **{}** 関数の値の設定の定義に使用します。 次の例では、関数を受け取り、1 つの引数なしの書式指定文字列と、レベルがエラーに設定します。

```
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
```

<span id="__USESUFFIX__Function_Name___Format_string___"></span><span id="__usesuffix__function_name___format_string___"></span><span id="__USESUFFIX__FUNCTION_NAME___FORMAT_STRING___"></span>**USESUFFIX (**<em>関数\_名前</em>**、"**<em>書式指定文字列</em>**");**  
イベントが記録されたときに使用する形式の文字列のサフィックスを定義します。 最初のパラメーターは、このサフィックスを適用する関数の名前です。 2 番目のパラメーターは、使用する書式指定文字列です。 変数の名前は、コードで使用できます。

```
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
```

### <a name="span-idexampleconfigurationblockspanspan-idexampleconfigurationblockspanexample-configuration-block"></a><span id="example_configuration_block"></span><span id="EXAMPLE_CONFIGURATION_BLOCK"></span>構成ブロックの例

次の例では、書式文字列のプレフィックスとサフィックスを使用するトレース マクロを定義します。 トレース マクロを定義する場合、ロガーを選択して、イベントが記録するかどうかを確認するマクロを定義する必要もあります。

```
//MACRO: TRACE_RETURN
//
//begin_wpp config
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
//end_wpp

//
// The next two macros are for checking if the event should be logged, and for
// choosing the logger handle to use when calling the ETW trace API
//
#define WPP_LEVEL_EXP_ENABLED(LEVEL, HR) WPP_FLAG_ENABLED(LEVEL)
#define WPP_LEVEL_EXP_LOGGER(LEVEL, HR) WPP_FLAG_LOGGER(LEVEL)
```

### <a name="span-idexampletraceresultsspanspan-idexampletraceresultsspanexample-trace-results"></a><span id="example_trace_results"></span><span id="EXAMPLE_TRACE_RESULTS"></span>トレース結果の例

```
[0]0F78.0460::06/24/2006-15:54:54.880 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
```

 

 






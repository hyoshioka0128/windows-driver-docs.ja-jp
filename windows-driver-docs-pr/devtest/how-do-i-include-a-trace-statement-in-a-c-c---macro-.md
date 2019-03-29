---
title: C と C++ マクロにトレース ステートメントを含める方法
description: C と C++ マクロにトレース ステートメントを含める方法
ms.assetid: 1ab7f87e-7dbc-49a1-b3a2-24e4d525dc8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ed0afac0f86b5de4aee95003c3008175522e2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580772"
---
# <a name="how-do-i-include-a-trace-statement-in-a-cc-macro"></a>C/C++ マクロにトレース ステートメントを含める方法


厳密に言えば、WPP プリプロセッサは C プリプロセッサの前に実行されるので、マクロ内のトレース ステートメントを含めることはできません。 1 つのソリューションは、C プリプロセッサを 2 回実行するが、さらに簡単なソリューションは、: トレース マクロに省略可能な事前/事後ステップを定義します。

たとえば、「で終了に失敗しました」のマクロをなどにすることがあります。

```
If (FAILED(HR)) {
     DoTraceMessage(ERROR,"We failed!");
     Goto done ;
} 
```

この場合、マクロの事前/事後のフォームを使用してこれを実現します。

### <a name="span-iddefinethefunctionspanspan-iddefinethefunctionspandefine-the-function"></a><span id="define_the_function"></span><span id="DEFINE_THE_FUNCTION"></span>関数を定義します

ソース ファイルでは、たとえば、関数を定義します。

```
FUNC:_EXIT_IF_EXP_FAILED{LEVEL=WSM_ERROR}(_EXIT_IF_EXP_FAILED_EXP,MSG,...)
```

### <a name="span-iddefinethemacrosspanspan-iddefinethemacrosspandefine-the-macros"></a><span id="define_the_macros"></span><span id="DEFINE_THE_MACROS"></span>マクロを定義します。

ヘッダー ファイルでは、次の定義ディレクティブを追加します。 WPP 後に置く\_コントロール\_GUID 定義する前に、 **\#含める**のステートメント、[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)。

```
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_PRE(LEVEL, HR) {HRESULT hr=S_OK ; if(FAILED(hr = HR)) {
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_POST(LEVEL, HR) ; goto done; } }
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_ENABLED(LEVEL, HR) WPP_LEVEL_ENABLED(LEVEL)
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(WSM_ERROR)
```

### <a name="span-idaddformattingspanspan-idaddformattingspanadd-formatting"></a><span id="add_formatting"></span><span id="ADD_FORMATTING"></span>書式設定を追加します。

トレース メッセージをヘッダー ファイル内のデータを書式設定を含めることで読みやすくすることができます。 この手順は省略可能です。

```
// MACRO: _EXIT_IF_EXP_FAILED
//
// begin_wpp config
// USEPREFIX (_EXIT_IF_EXP_FAILED,"%!STDPREFIX!");
// FUNC _EXIT_IF_EXP_FAILED{LEVEL=WSM_ERROR}(_EXIT_IF_EXP_FAILED_EXP,MSG,...);
// USESUFFIX (_EXIT_IF_EXP_FAILED," hr= %!HRESULT!", hr);
// end_wpp
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_PRE(LEVEL, HR) {HRESULT hr=S_OK ; if(FAILED(hr = HR)) {
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_POST(LEVEL, HR) ; goto done; } }
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_ENABLED(TRACELEVEL, HR) WPP_LEVEL_ENABLED(TRACELEVEL)
#define WPP_LEVEL__EXIT_IF_EXP_FAILED_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(WSM_ERROR)
```

この例で、**開始\_wpp config**と**エンド\_wpp**ステートメントは、WPP のヘッダー ファイルで構成データを識別します。

また、ヘッダー ファイルで構成データがある WPP に通知を追加、 **-スキャン**、実行するようにパラメーター\_WPP マクロは、WPP プリプロセッサを呼び出します。 以下に例を示します。

```
RUN_WPP -scan:trace.h
```

実行の省略可能なパラメーターの完全な一覧については\_WPP を参照してください[WPP プリプロセッサ](wpp-preprocessor.md)します。

### <a name="span-idusethemacrosspanspan-idusethemacrosspanuse-the-macros"></a><span id="use_the_macros"></span><span id="USE_THE_MACROS"></span>マクロを使用します。

ソース コードで、次の呼び出しでなど、マクロを使用します。

```
_EXIT_IF_EXP_FAILED(hr,"it failed");
```

 

 






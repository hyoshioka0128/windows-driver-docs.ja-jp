---
title: トレースの方法は、式が使用されている場合
description: トレースの方法は、式が使用されている場合
ms.assetid: 05fc8225-ba4e-4718-a5e1-c9e49ec931b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b68ac23817724130314ed08d04950621e896f75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552107"
---
# <a name="how-are-trace-if-expressions-used"></a>トレースの方法は、式が使用されている場合ですか?


理解に役立つトレースする方法-式を使用している場合、使用方法について説明するこのような式の例と構文の提供"開始\_wpp config"ステートメント。 この例では、関数のトレース\_返すには、FAILED(HR) 式が true の場合、イベント ログに記録します。

FAILED(HR) が true の場合は、ULONG の状態を含むソース ファイルがあるし、トレースを呼び出すことによって、イベントがログに記録することを想定しています。\_RETURN(Status) します。
```
//MACRO: TRACE_RETURN
//
//begin_wpp config
//USEPREFIX (TRACE_RETURN, "%!STDPREFIX!");
//FUNC TRACE_RETURN{LEVEL=ERROR}(EXP);
//USESUFFIX (TRACE_RETURN, "Function Return=%!HRESULT!",EXP);
//end_wpp

#define WPP_LEVEL_EXP_PRE(LEVEL, HR) {if (FAILED(HR)) {
#define WPP_LEVEL_EXP_POST(LEVEL, HR) ;}}
#define WPP_LEVEL_EXP_ENABLED(LEVEL, HR) WPP_LEVEL_ENABLED(LEVEL)
#define WPP_LEVEL_EXP_LOGGER(LEVEL, HR) WPP_LEVEL_LOGGER(ERROR)
```

前の例では、ことに注意して、トレース\_開始の間で戻り値が定義されている\_wpp 構成と終了\_wpp 行。 この定義の後は、前/マクロと有効にし、ロガーの定義を投稿します。

Begin\_wpp 構成と終了\_wpp 区切り記号はプリプロセッサによって解析される構成ブロックを定義します。 構成ブロックの定義を含むファイルは、WPP でスキャンする必要があります。 このファイルは scan:file.extension パラメーターで指定します。

**注**について **-スキャン**およびその他の**実行\_WPP**オプションを参照してください[WPP プリプロセッサ](wpp-preprocessor.md)。



次の一覧では、例の構成ブロック内の各ステートメントについて詳しく説明します。

<span id="USEPREFIX"></span><span id="useprefix"></span>**USEPREFIX**  
イベントが記録されたときに使用されるプレフィックスの書式指定文字列を定義します。 例では、STDPREFIX が使用されます。 STDPREFIX で使用可能な値では、次を参照してください。[すべてトレースの行にプレフィックスの出力を変更する方法でしょうか。](how-do-i-change-the-prefix-output-on-every-trace-line-.md)

<span id="USESUFFIX"></span><span id="usesuffix"></span>**USESUFFIX**  
イベントが記録されたときに使用されるサフィックスの書式指定文字列を定義します。

<span id="FUNC"></span><span id="func"></span>**FUNC**  
トレースの関数のシグネチャと名前を定義します。 例では、この関数は、1 つのパラメーターとしない書式指定文字列を受け取ります。

トレースの別の例の場合は、式を参照してください、 [C/C++ マクロにトレース ステートメントを含める方法でしょうか。](how-do-i-include-a-trace-statement-in-a-c-c---macro-.md)セクション。










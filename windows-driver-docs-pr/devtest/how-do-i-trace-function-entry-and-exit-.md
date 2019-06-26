---
title: どの関数のトレース エントリの操作し、終了
description: どの関数のトレース エントリの操作し、終了
ms.assetid: 08b0cf86-0f19-4972-8ae1-44ffdc968c16
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92c4d0d26f42991c79d9564a41b85fe4656defd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358281"
---
# <a name="how-do-i-trace-function-entry-and-exit"></a>関数の出入りをトレースする方法


次のサンプル コードでは、関数のエントリをトレースし、呼び出しを終了する方法を示します。 このコードは、Windows 2000 以降のバージョンの Windows で動作します。

定義を最初に、追加、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))ソースまたはヘッダー ファイル マクロ。 定義するときに、[トレース フラグ](trace-flags.md)、次の例に示すように、関数のトレース フラグを定義します。

```
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(CtlGuid,(a044090f,3d9d,48cf,b7ee,9fb114702dc1),  \
        WPP_DEFINE_BIT(ERROR)                \
        WPP_DEFINE_BIT(Unusual)              \
        WPP_DEFINE_BIT(Noise)                \
 WPP_DEFINE_BIT(FuncTrace) )
```

次に、同じファイルでは、トレース メッセージの構成データを追加します。 使用して構成データの開始、**開始\_wpp config**ステートメントでは、末尾にでは、**エンド\_wpp**ステートメント。 FuncTrace をサポートするマクロの定義を次に追加します。

```
// begin_wpp config
// FUNC FuncEntry();
// FUNC FuncExit();
// USESUFFIX(FuncEntry, " Entry to %!FUNC!");
// USESUFFIX(FuncExit, " Exit from %!FUNC!");
// end_wpp

// Map the null flags used by Entry/Exit to a function called FuncTrace
#define WPP__ENABLED() WPP_LEVEL_ENABLED(FuncTrace)
#define WPP__LOGGER() WPP_LEVEL_LOGGER(FuncTrace)
```

ソース ファイルでの関数コードを囲む**FuncEntry()** と**FuncExit()** 呼び出し。

```
#include "mytrace.h"
#include "entryexit.tmh"
void examplesub(int x)
{
    FuncEntry();
    // function code
    FuncExit();
}
```

例:

```
#include "mytrace.h"
#include "entryexit.tmh"
void examplesub(int x)
{
    FuncEntry();
       DoTraceMessage(Noise, "Value is %d",x);
    FuncExit();
}
```

ヘッダー ファイルで構成データを配置する場合は、使用、 **-スキャン**パラメーターを指定したファイルで構成データを検索する WPP します。 この例では、構成データは mytrace.h ファイルです。

```
RUN_WPP=$(SOURCES) -km -scan:mytrace.h
```

**注**するを指定する必要があります、 **km**実行の切り替え\_WPP ディレクティブのユーザー モード アプリケーションまたはダイナミック リンク ライブラリ (Dll)。



実行の省略可能なパラメーターの完全な一覧については\_WPP を参照してください[WPP プリプロセッサ](wpp-preprocessor.md)します。










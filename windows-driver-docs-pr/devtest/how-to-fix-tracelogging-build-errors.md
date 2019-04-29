---
title: TraceLogging のビルド エラーの修正方法
description: このトピックでは、一般的なビルド エラーとその解決方法について説明します。
ms.assetid: E0C7ACA5-68C9-40FF-8D6E-4A65CEB0A851
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3dab8293ffad7098dc400309a84c0d163786052
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329936"
---
# <a name="how-to-fix-tracelogging-build-errors"></a>TraceLogging のビルド エラーの修正方法


このトピックでは、一般的なビルド エラーとその解決方法について説明します。

## <a name="span-idcase1declspecsafebufferserrorsspanspan-idcase1declspecsafebufferserrorsspanspan-idcase1declspecsafebufferserrorsspancase-1-declspecsafebuffers-errors"></a><span id="Case_1___DECLSPEC_SAFEBUFFERS__errors"></span><span id="case_1___declspec_safebuffers__errors"></span><span id="CASE_1___DECLSPEC_SAFEBUFFERS__ERRORS"></span>ケース 1: ' DECLSPEC\_SAFEBUFFERS のエラー


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>ビルド エラー (スニペット)。  
```
1>traceloggingprovider.h(1592): error C2146: syntax error : missing ';' before identifier 'TLG_STATUS'
1>traceloggingprovider.h(1592): error C2433: 'DECLSPEC_SAFEBUFFERS' : 'inline' not permitted on data declarations
1>traceloggingprovider.h(1592): error C4430: missing type specifier - int assumed. Note: C++ does not support default-int
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>修正:  
ソース ファイルで TraceLoggingProvider.h をインクルードする前に windows.h が含まれます。

## <a name="span-idcase2tracelogginginmoderncappsspanspan-idcase2tracelogginginmoderncappsspanspan-idcase2tracelogginginmoderncappsspancase-2-tracelogging-in-modern-c-apps"></a><span id="Case_2__TraceLogging_in_Modern_C___Apps"></span><span id="case_2__tracelogging_in_modern_c___apps"></span><span id="CASE_2__TRACELOGGING_IN_MODERN_C___APPS"></span>ケース 2: 最新の C++ アプリで TraceLogging


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>ビルド エラー (スニペット)。  
後に、ビルド環境に TraceLogging ヘッダー ファイルをコピーし、この行を追加します。

```
TraceLoggingRegisterByGuid(g_3DBuilderTraceProvider, &s_3DBuilderTraceProviderGuid);
```

このリンカー エラーを入手できました。

```
Error 2 error LNK2001: unresolved external symbol __imp__EventSetInformation@20 
        E:\TFS\Main\PrintPreviewR5\Viewers\PrintPreview\App.xaml.obj    PrintPreview
Error 3 error LNK2001: unresolved external symbol __imp__EventRegister@16       
        E:\TFS\Main\PrintPreviewR5\Viewers\PrintPreview\App.xaml.obj    PrintPreview
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>修正:  
UWP アプリでは、この参照の問題を解決するのには advapi32.lib とリンクする必要があります。

## <a name="span-idcase3phonebuildsspanspan-idcase3phonebuildsspanspan-idcase3phonebuildsspancase-3-phone-builds"></a><span id="Case_3__Phone_Builds"></span><span id="case_3__phone_builds"></span><span id="CASE_3__PHONE_BUILDS"></span>ケース 3: 電話のビルド


<span id="Build_Error__snippet__"></span><span id="build_error__snippet__"></span><span id="BUILD_ERROR__SNIPPET__"></span>ビルド エラー (スニペット)。  
ファイル dictationuimodel.cpp をコンパイルするときにエラーが発生しました。

```
traceloggingprovider.h(1592) : error C2146: syntax error : missing ';' before identifier 'TLG_STATUS'
traceloggingprovider.h(1592) : error C2433: 'DECLSPEC_SAFEBUFFERS' : 'inline' not permitted on data declarations
```

<span id="Fix_"></span><span id="fix_"></span><span id="FIX_"></span>修正:  
ケースを参照してください。\#1。 SDK が、マクロを定義していない可能性があります**DECLSPEC\_SAFEBUFFERS**します。 最新の Sdk では、このマクロの定義があります。 SDK がこのマクロを定義していない場合は、独自の定義を指定する必要があります。 **DECLSPEC\_SAFEBUFFERS** windows.h で含める必要がある、winnt.h で定義されます。 また、Windows 10 SDK のパブリック リリースまでする必要がありますを定義、*テレメトリ*キーワード。

```
#ifndef WINEVENT_KEYWORD_TELEMETRY 
#define WINEVENT_KEYWORD_TELEMETRY  0x2000000000000
#endif
```

 

 






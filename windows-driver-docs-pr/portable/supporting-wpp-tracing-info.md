---
Description: WPP トレースのサポート
title: WPP トレースのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c36d291a72128499c915f2dd58815b1ae3cf986
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380842"
---
# <a name="supporting-wpp-tracing"></a>WPP トレースのサポート


Windows ソフトウェア トレース プリプロセッサ (WPP) は、イベントをリアルタイムで効率的なログ機構を提供します。 WPP は、WPD ドライバーでトレースとエラー メッセージをログに推奨される方法です。

WPP トレースは、システムのタイムスタンプを含めるし、関数呼び出しまでの経過時間を測定することにより、たとえば、パフォーマンスを測定するために使用できます。

## <a name="span-idsampledriversthatsupportwpptracingspanspan-idsampledriversthatsupportwpptracingspanspan-idsampledriversthatsupportwpptracingspansample-drivers-that-support-wpp-tracing"></a><span id="Sample_Drivers_that_Support_WPP_Tracing"></span><span id="sample_drivers_that_support_wpp_tracing"></span><span id="SAMPLE_DRIVERS_THAT_SUPPORT_WPP_TRACING"></span>WPP トレースをサポートしているサンプル ドライバー


次のサンプル ドライバーでは、WPP トレースを使用する方法を示します。

-   WpdBasicHardwareDriver
-   WpdServiceSampleDriver

## <a name="span-idtransitioningfromoutputdebugstringtowppspanspan-idtransitioningfromoutputdebugstringtowppspanspan-idtransitioningfromoutputdebugstringtowppspantransitioning-from-outputdebugstring-to-wpp"></a><span id="Transitioning_from_OutputDebugString_to_WPP"></span><span id="transitioning_from_outputdebugstring_to_wpp"></span><span id="TRANSITIONING_FROM_OUTPUTDEBUGSTRING_TO_WPP"></span>OutputDebugString から WPP への移行


チェックを使用して、エラー メッセージが記録、WpdHelloWorldDriver、WpdWudfSampleDriver、および、WpdMultiTransportDriver\_HR 関数をラップする、 **OutputDebugString**メソッド。 開発時にこのメソッドは使いやすいが、トレースを表示するには、アクティブなデバッガーの接続が必要です。 OutputDebugString メソッド使用してください最小最終的なコードでのリリース。 WPP トレースより軽量な柔軟、そしてさまざまなトレースのアプリケーションのことをお勧めします。 たとえば開発中は、コードが実行をトレースのエラーを診断するためのエラーのログ記録します。

使用してドライバーを移行するために**OutputDebugString** WPP を使用するには、次の手順を完了します。

1.  元のチェックを削除\_HR() 関数の定義 (で見つかる*WpdHelloWorldDriver.cpp*または*WpdWudfSampleDriver.cpp* WPD のサンプル)での宣言と*Stdafx.h*します。
2.  更新プログラム、 *Stdafx.h* WPP マクロは、このトピックで後で説明されているファイル。
3.  追加の実行を\_WPP ディレクティブには、ドライバーのソース ファイルにします。
4.  DllMain メソッドには、ドライバーには、WPP 初期化とクリーンアップ ルーチンを追加します。
5.  各ドライバーのソース ファイルを追加、 *\#含める&lt;ファイル名&gt;.tmh*既存のステートメントを含めた後。
6.  ドライバーを再構築します。 チェックを置換した\_HR 関数と同じ WPP マクロ、同じシグネチャを持つ場合は、変更は必要ありませんチェックを使用するコードの\_HR。

WPP プリプロセッサ プロセス*Stdafx.h*トレース マクロは、各トレース メッセージのヘッダー (tmh) ファイルを生成します。Obj フォルダーの CPP ファイルです。

各プリプロセッサの出力を検査します。 場合、CPP ファイルのチェックを呼び出す\_HR (make を使用して生成された*WpdBaseDriver.pp*)、すべてのチェックがわかります\_HR トレース ステートメントは、トレース テキスト関数と WPP 関数の中に、WPP 関数呼び出しでラッピングされています。定義された*WpdBaseDriver.tmh*します。

最も一般的な WPP に関連するコンパイル エラーが発生することができますが (たとえば、余分な引数に一致しない %d が、書式指定文字列に含まれている場合) パラメーターや、WPP で不足しているエントリが一致しない形式の識別子のため、\_コントロール\_GUID マクロ。

## <a name="span-idupdatingthestdafxhfilespanspan-idupdatingthestdafxhfilespanupdating-the-stdafxh-file"></a><span id="updating_the_stdafx.h_file"></span><span id="UPDATING_THE_STDAFX.H_FILE"></span>Stdafx.h ファイルの更新


次のコード例にする更新プログラムが含まれています*Stdafx.h* 、ドライバーは現在サポートしている場合**OutputDebugString**します。

```ManagedCPlusPlus
#define MYDRIVER_TRACING_ID      L"Microsoft\\WPD\\ServiceSampleDriver"

#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(ServiceSampleDriverCtlGuid,(f0cc34b3,a482,4dc0,b978,b5cf42aec4fd), \
        WPP_DEFINE_BIT(TRACE_FLAG_ALL)                                      \
        WPP_DEFINE_BIT(TRACE_FLAG_DEVICE)                                   \
        WPP_DEFINE_BIT(TRACE_FLAG_DRIVER)                                   \
        WPP_DEFINE_BIT(TRACE_FLAG_QUEUE)                                    \
        )

#define WPP_LEVEL_FLAGS_LOGGER(lvl,flags) \
           WPP_LEVEL_LOGGER(flags)

#define WPP_LEVEL_FLAGS_ENABLED(lvl, flags) \
           (WPP_LEVEL_ENABLED(flags) && WPP_CONTROL(WPP_BIT_ ## flags).Level >= lvl)

//
// This comment block is scanned by the trace preprocessor to define our
// TraceEvents function.
//
// begin_wpp config
// FUNC Trace{FLAG=TRACE_FLAG_ALL}(LEVEL, MSG, ...);
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// end_wpp

//
// This comment block is scanned by the trace preprocessor to define our
// CHECK_HR function.
//
//
// begin_wpp config
// USEPREFIX (CHECK_HR,"%!STDPREFIX!");
// FUNC CHECK_HR{FLAG=TRACE_FLAG_ALL}(hrCheck, MSG, ...);
// USESUFFIX (CHECK_HR, " hr= %!HRESULT!", hrCheck);
// end_wpp

//
// PRE macro: The name of the macro includes the condition arguments FLAGS and EXP
//            define in FUNC above
//
#define WPP_FLAG_hrCheck_PRE(FLAGS, hrCheck) {if(hrCheck != S_OK) {

//
// POST macro
// The name of the macro includes the condition arguments FLAGS and EXP
//            define in FUNC above
#define WPP_FLAG_hrCheck_POST(FLAGS, hrCheck) ; } }

//
// The two macros below are for checking if the event should be logged and for
// choosing the logger handle to use when calling the ETW trace API
//
#define WPP_FLAG_hrCheck_ENABLED(FLAGS, hrCheck) WPP_FLAG_ENABLED(FLAGS)
#define WPP_FLAG_hrCheck_LOGGER(FLAGS, hrCheck) WPP_FLAG_LOGGER(FLAGS)
```

## <a name="span-idaddingthewppinitializationandcleanuproutinestodllmainspanspan-idaddingthewppinitializationandcleanuproutinestodllmainspanspan-idaddingthewppinitializationandcleanuproutinestodllmainspanadding-the-wpp-initialization-and-cleanup-routines-to-dllmain"></a><span id="Adding_the_WPP_Initialization_and_Cleanup_Routines_to_DllMain"></span><span id="adding_the_wpp_initialization_and_cleanup_routines_to_dllmain"></span><span id="ADDING_THE_WPP_INITIALIZATION_AND_CLEANUP_ROUTINES_TO_DLLMAIN"></span>DllMain に WPP 初期化とクリーンアップ ルーチンを追加します。


更新した後、*ソース*ファイルで次のコード例に示すように、ドライバーの場合、DllMain ルーチンを更新します。

```ManagedCPlusPlus
// DLL Entry Point
extern "C" BOOL WINAPI DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID lpReserved)
{    
if(DLL_PROCESS_ATTACH == dwReason)    
{        
g_hInstance = hInstance;              
//        
// Initialize tracing.        
//        
WPP_INIT_TRACING(MYDRIVER_TRACING_ID);    
}    
else if (DLL_PROCESS_DETACH == dwReason)    
{        
//        
// Cleanup tracing.        
//        
WPP_CLEANUP();    
}    
return _AtlModule.DllMain(dwReason, lpReserved);
}
```

## <a name="span-idincludingthetracemessageheaderfilesspanspan-idincludingthetracemessageheaderfilesspanspan-idincludingthetracemessageheaderfilesspanincluding-the-trace-message-header-files"></a><span id="Including_the_Trace_Message_Header_files"></span><span id="including_the_trace_message_header_files"></span><span id="INCLUDING_THE_TRACE_MESSAGE_HEADER_FILES"></span>トレース メッセージのヘッダー ファイルを含む


DllMain ルーチンを更新した後は、それぞれを更新します。CPP は、ソース ファイルと、対応するトレース メッセージのヘッダー ファイルをインクルードします。 次のコード例を含めることを示しています、 *WpdBaseDriver.tmh*ファイル*WpdBaseDriver.cpp*します。

```ManagedCPlusPlus
//
// WpdBaseDriver.cpp
//#include "stdafx.h"
#include "WpdBaseDriver.h"
// Include the WPP generated Trace Message Header (tmh) file for this .cpp
#include "WpdBaseDriver.tmh"
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WDK と Visual Studio のビルド環境](https://msdn.microsoft.com/library/windows/hardware/hh454286)

 

 






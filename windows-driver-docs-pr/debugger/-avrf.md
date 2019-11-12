---
title: avrf
description: avrf 拡張機能では、Application Verifier の設定を制御し、さまざまなアプリケーション検証ツールによって生成される出力を表示します。
ms.assetid: e9313954-a1fa-45a9-bc1a-78be2451f5aa
keywords:
- Windows デバッグ avrf
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- avrf
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7f91dfda25c6fca1eb854d66efce5e75a15baaf
ms.sourcegitcommit: a70dcf63a439d278ae0194733d9fa2adfe496c89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66813563"
---
# <a name="avrf"></a>!avrf


**!avrf** 拡張機能は[アプリケーション検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/application-verifier)の設定を制御し、アプリケーション検証ツールによって生成されるさまざまな出力を表示します。

```dbgcmd
    !avrf
    !avrf -vs { Length | -a Address }
    !avrf -hp { Length | -a Address }
    !avrf -cs { Length | -a Address }
    !avrf -dlls [ Length ]
    !avrf -trm
    !avrf -ex [ Length ] 
    !avrf -threads [ ThreadID ]
    !avrf -tp [ ThreadID ]
    !avrf -srw  [ Address | Address Length ] [ -stats ]
    !avrf -leak  [ -m ModuleName] [ -r ResourceType] [ -a Address ] [ -t ]
    !avrf -trace TraceIndex 
    !avrf -cnt
    !avrf -brk [BreakEventType]  
    !avrf -flt [EventType Probability] 
    !avrf -flt break EventType 
    !avrf -flt stacks Length 
    !avrf -trg [ Start End | dll Module | all ] 
    !avrf -settings 
    !avrf -skp [ Start End | dll Module | all | Time ] 
```

## <a name="span-idddk__avrf_dbgspanspan-idddk__avrf_dbgspanparameters"></a><span id="ddk__avrf_dbg"></span><span id="DDK__AVRF_DBG"></span>パラメーター


<span id="-vs___Length___-a_Address__"></span><span id="-vs___length___-a_address__"></span><span id="-VS___LENGTH___-A_ADDRESS__"></span> **-vs {** *Length* **| -a** *Address* **}**  

仮想空間操作ログを表示します。*Length* は、最新のものから順に表示するレコードの数を指定します。*Address* は、仮想アドレスを指定します。この仮想アドレスを含む仮想操作のレコードが表示されます。


<span id="-hp___Length___-a_Address__"></span><span id="-hp___length___-a_address__"></span><span id="-HP___LENGTH___-A_ADDRESS__"></span> **-hp {** *Length* **|-** *Address* **}**  
ヒープ操作ログを表示します。 *Address*ヒープのアドレスを指定します。 このヒープ アドレスが含まれているヒープ操作のレコードが表示されます。


<span id="-cs___Length___-a_Address__"></span><span id="-cs___length___-a_address__"></span><span id="-CS___LENGTH___-A_ADDRESS__"></span> **-cs {** *Length* **|-** *Address* **}**  
クリティカル セクションの削除ログを表示します。*Length* は、最新のものから順に、表示するレコードの数を指定します。*Address* は、クリティカル セクションのアドレスを指定します。*Address* を指定すると、特定のクリティカル セクションのレコードが表示されます。

<span id="-dlls___Length__"></span><span id="-dlls___length__"></span><span id="-DLLS___LENGTH__"></span> **-dll \[**  *Length* **\]**  
DLL のロード/アンロード ログを表示します。*Length* は、最新のものから順に、表示するレコードの数を指定します。


<span id="-trm"></span><span id="-TRM"></span> **-trm**  
すべての終了および中断されたスレッドのログを表示します。

<span id="-ex___Length__"></span><span id="-ex___length__"></span><span id="-EX___LENGTH__"></span> **-ex \[**  *Length* **\]**  
例外のログを表示します。 Application Verifier は、アプリケーション内のすべての例外を追跡します。

<span id="-threads___ThreadID__"></span><span id="-threads___threadid__"></span><span id="-THREADS___THREADID__"></span> **-threads \[**  *ThreadID* **\]**  
ターゲット プロセスのスレッドに関する情報を表示します。 子のスレッドでスタック サイズと**CreateThread**も、親で指定されたフラグが表示されます。 スレッド ID を指定すると、そのスレッドのみの情報が表示されます。

<span id="-tp___ThreadID___"></span><span id="-tp___threadid___"></span><span id="-TP___THREADID___"></span> **-tp \[**  *ThreadID* **\]**    
Threadpool のログを表示します。 このログには、スレッドの優先順位、スレッドにメッセージを投稿、およびスレッド プール コールバック内からの初期化中または初期化解除 COM を変更するスレッドの関係マスクを変更するなどのさまざまな操作のスタック トレースが含まれています。 スレッド ID を指定すると、そのスレッドの情報のみが表示されます。

<span id="-srw____Address___Address_Length_____-stats___"></span><span id="-srw____address___address_length_____-stats___"></span><span id="-SRW____ADDRESS___ADDRESS_LENGTH_____-STATS___"></span> **-srw \[** *Address* **|** *Address Length* **\] \[ -stats \]**    
Slim Reader/Writer (SRW) ログを表示します。*Address* を指定すると、そのアドレスにおける SRW ロックのレコードが表示されます。*Address* と *Length* を指定すると、そのアドレス範囲内の SRW ロックのレコードが表示されます。**-stats** オプションを含めると、SRW ロックの統計情報が表示されます。

<span id="-leak___-m_ModuleName____-r_ResourceType____-a_Address_____-t___"></span><span id="-leak___-m_modulename____-r_resourcetype____-a_address_____-t___"></span><span id="-LEAK___-M_MODULENAME____-R_RESOURCETYPE____-A_ADDRESS_____-T___"></span> **-leak \[-m** <em>ModuleName</em>  **\] \[ -r** <em>ResourceType</em>  **\] \[ -a** *Address*  **\] \[ -t \]**    
リソースの未処理のログを表示します。 これらのリソースは、特定の時点のリークができない可能性があります。 指定した場合*Modulename* (拡張機能を含む)、指定したモジュール内のすべての未処理リソースが表示されます。 指定した場合*ResourceType*、そのリソースの種類のすべての優れたリソースが表示されます。 指定した場合*アドレス*、そのアドレスを持つ未解決のリソースのレコードが表示されます。 *ResourceType*次のいずれかを指定できます。

ヒープ:ヒープの Win32 Api を使用して、ヒープ割り当てを表示します。

地元の：ローカル/グローバル割り当てを表示します。

CRT:CRT の Api を使用して表示割り当て

仮想。仮想の予約を表示します。

BSTR。BSTR の割り当てを表示します

レジストリ:レジストリ キーの表示を開きます

電源。電源通知オブジェクトを表示します

ハンドル:スレッドの表示、ファイル、およびイベント処理の割り当て

<span id="-trace_TraceIndex"></span><span id="-trace_traceindex"></span><span id="-TRACE_TRACEINDEX"></span> **-trace** *TraceIndex* 指定したトレース インデックスのスタック トレースが表示されます。一部の構造は、スタック トレースを識別するために、この 16 ビットのインデックス番号を使用します。このインデックスは、スタック トレース データベースの特定の場所を指します。

<span id="-cnt"></span><span id="-CNT"></span> **-cnt**グローバル カウンターの一覧を表示します。

<span id="-brk___BreakEventType__"></span><span id="-brk___breakeventtype__"></span><span id="-BRK___BREAKEVENTTYPE__"></span> **-brk \[** *BreakEventType* **\]** ブレーク イベントを指定します。*BreakEventType* はブレーク イベントの型番です。使用可能な型と現在のブレーク イベントの設定の一覧については、**!avrf brk** を入力してください。

<span id="-flt___EventType_Probability__"></span><span id="-flt___eventtype_probability__"></span><span id="-FLT___EVENTTYPE_PROBABILITY__"></span> **-flt \[** *EventType Probability* **\]** フォールト挿入を指定します。*EventType* はイベントの型番です。*Probability* はイベントが失敗する頻度です。0 ～ 1,000,000 (0xF4240) の整数を指定できます。追加のパラメーターなしで **!avrf flt** を入力した場合は、現在のフォールト挿入の設定が表示されます。

<span id="-flt_break_EventType"></span><span id="-flt_break_eventtype"></span><span id="-FLT_BREAK_EVENTTYPE"></span>**-flt break** *EventType* *EventType* によって指定されたエラーが挿入されるたびにアプリケーション検証ツールがデバッガーで中断されるようになります。

<span id="-flt_stacks_Length"></span><span id="-flt_stacks_length"></span><span id="-FLT_STACKS_LENGTH"></span>**-flt stacks* *Length* 最新のフォールト挿入操作に対するスタック トレースの *Length* 数が表示されます。

<span id="-trg___Start_End___dll_Module___all____"></span><span id="-trg___start_end___dll_module___all____"></span><span id="-TRG___START_END___DLL_MODULE___ALL____"></span> **-trg \[** *Start End* **| dll** *Module* **| all\]** 対象範囲を指定します。*Start* は対象範囲の開始アドレスです。*End* は対象範囲の終了アドレスです。*Module* は対象となるモジュールの名前 (.exe または .dll 拡張子を含むが、パスは含まない) を指定します。**-trg all** を入力した場合、すべての対象範囲がリセットされます。**- trg** を追加のパラメーターなしで入力した場合、現在の対象範囲が表示されます。

<span id="-skp___Start_End___dll_Module___all___Time____"></span><span id="-skp___start_end___dll_module___all___time____"></span><span id="-SKP___START_END___DLL_MODULE___ALL___TIME____"></span> **-skp \[** *Start End* **| dll** *Module* **| all |** **Time* **\]** 除外範囲を指定します。*Start* は除外範囲の開始アドレスです。*End* は除外範囲の終了アドレスです。モジュールは対象とするまたは除外するモジュールの名前を指定します。*Module* は除外するモジュールの名前 (.exe または .dll 拡張子を含むが、パスは含まない) を指定します。**-skp all** を入力すると、すべての対象範囲または除外範囲がリセットされます。*Time* 値を入力した場合、すべての障害が実行の再開後 *Time* ミリ秒抑制されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

exts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アプリケーション検証ツールとドキュメント、ダウンロードしてインストールする方法については、次を参照してください。 [Application Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/application-verifier)します。

<a name="remarks"></a>注釈
-------

**!avrf** 拡張機能がパラメーターなしで使用されると、現在のアプリケーション検証ツールのオプションが表示されます。**[Full page heap]** または **[Fast fill heap]** オプションが有効な場合、アクティブなページ ヒープに関する情報も表示されます。いくつかの例については、アプリケーション検証ツール ドキュメントの「ヒープ操作ログ」を参照してください。

アプリケーション検証ツールの停止が発生した場合、パラメーターなしの **!avrf** 拡張機能が停止の性質とその結果を示します。いくつかの例については、アプリケーション検証ツール ドキュメントの「アプリケーション検証ツールのデバッグの停止」を参照してください。

ntdll.dll と verifier.dll 用のシンボルが不足している場合、**!avrf** 拡張機能はエラー メッセージを生成します。この問題に対処する方法については、アプリケーション検証ツール ドキュメントの「アプリケーション検証ツールのデバッガーの設定」を参照してください。

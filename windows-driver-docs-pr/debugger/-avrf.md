---
title: avrf
description: Avrf 拡張機能では、Application Verifier の設定を制御し、さまざまなアプリケーション検証ツールによって生成される出力を表示します。
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
ms.openlocfilehash: eb452ca2be00cdeca72cc168c28585d617d31069
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551281"
---
# <a name="avrf"></a>! avrf


**! Avrf**拡張機能の設定を制御する[Application Verifier](application-verifier.md)し、さまざまなアプリケーション検証ツールによって生成される出力を表示します。

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

## <a name="span-idddkavrfdbgspanspan-idddkavrfdbgspanparameters"></a><span id="ddk__avrf_dbg"></span><span id="DDK__AVRF_DBG"></span>パラメーター


<span id="-vs___Length___-a_Address__"></span><span id="-vs___length___-a_address__"></span><span id="-VS___LENGTH___-A_ADDRESS__"></span>**-vs {** *Length* **| -a** *Address* **}**  
仮想空間操作ログを表示します。 *長さ*以降、最新では、表示するレコードの数を指定します。 *アドレス*仮想のアドレスを指定します。 この仮想アドレスを含む仮想操作のレコードが表示されます。

<span id="-hp___Length___-a_Address__"></span><span id="-hp___length___-a_address__"></span><span id="-HP___LENGTH___-A_ADDRESS__"></span>**-hp {** *長さ* **|-** *アドレス* **}**  
ヒープ操作ログを表示します。 *アドレス*ヒープのアドレスを指定します。 このヒープ アドレスが含まれているヒープ操作のレコードが表示されます。

<span id="-cs___Length___-a_Address__"></span><span id="-cs___length___-a_address__"></span><span id="-CS___LENGTH___-A_ADDRESS__"></span>**-cs {** *長さ* **|-** *アドレス* **}**  
クリティカル セクションの削除ログを表示します。 *長さ*以降、最新では、表示するレコードの数を指定します。 *アドレス*クリティカル セクションのアドレスを指定します。 特定のクリティカル セクションのレコードが表示されるとき*アドレス*を指定します。

<span id="-dlls___Length__"></span><span id="-dlls___length__"></span><span id="-DLLS___LENGTH__"></span>**-dll \[**  *長さ* **\]**  
DLL の読み込み/アンロード ログを表示します。 *長さ*以降、最新では、表示するレコードの数を指定します。

<span id="-trm"></span><span id="-TRM"></span>**-trm**  
すべての終了および中断されたスレッドのログを表示します。

<span id="-ex___Length__"></span><span id="-ex___length__"></span><span id="-EX___LENGTH__"></span>**-ex \[**  *長さ* **\]**  
例外のログを表示します。 Application Verifier は、アプリケーション内のすべての例外を追跡します。

<span id="-threads___ThreadID__"></span><span id="-threads___threadid__"></span><span id="-THREADS___THREADID__"></span>**-スレッド\[**  *ThreadID* **\]**  
ターゲット プロセスのスレッドに関する情報を表示します。 子のスレッドでスタック サイズと**CreateThread**も、親で指定されたフラグが表示されます。 スレッド ID を指定すると、そのスレッドのみの情報が表示されます。

<span id="-tp___ThreadID___"></span><span id="-tp___threadid___"></span><span id="-TP___THREADID___"></span>**-tp \[**  *ThreadID* **\]**   
Threadpool のログを表示します。 このログには、スレッドの優先順位、スレッドにメッセージを投稿、およびスレッド プール コールバック内からの初期化中または初期化解除 COM を変更するスレッドの関係マスクを変更するなどのさまざまな操作のスタック トレースが含まれています。 スレッド ID を指定すると、そのスレッドの情報のみが表示されます。

<span id="-srw____Address___Address_Length_____-stats___"></span><span id="-srw____address___address_length_____-stats___"></span><span id="-SRW____ADDRESS___ADDRESS_LENGTH_____-STATS___"></span>**-srw \[**  *アドレス* **|** *アドレス長*  **\] \[ -stats \]**   
Slim Reader/writer (SRW) ログを表示します。 指定した場合*アドレス*、SRW ロックがそのアドレスでレコードが表示されます。 指定した場合*アドレス*と*長さ*、レコードは、SRW ロックで、そのアドレス範囲が表示されます。 含める場合は、 **-stats**オプション、SRW ロックの統計情報が表示されます。

<span id="-leak___-m_ModuleName____-r_ResourceType____-a_Address_____-t___"></span><span id="-leak___-m_modulename____-r_resourcetype____-a_address_____-t___"></span><span id="-LEAK___-M_MODULENAME____-R_RESOURCETYPE____-A_ADDRESS_____-T___"></span>**-リーク\[-m** <em>ModuleName</em>  **\] \[ -r** <em>ResourceType</em>  **\] \[ -a** *アドレス*  **\] \[ -t \]**   
リソースの未処理のログを表示します。 これらのリソースは、特定の時点のリークができない可能性があります。 指定した場合*Modulename* (拡張機能を含む)、指定したモジュール内のすべての未処理リソースが表示されます。 指定した場合*ResourceType*、そのリソースの種類のすべての優れたリソースが表示されます。 指定した場合*アドレス*、そのアドレスを持つ未解決のリソースのレコードが表示されます。 *ResourceType*次のいずれかを指定できます。

ヒープ:ヒープの Win32 Api を使用して、ヒープ割り当てを表示します。

地元の：ローカル/グローバル割り当てを表示します。

CRT:CRT の Api を使用して表示割り当て

仮想。仮想の予約を表示します。

BSTR。BSTR の割り当てを表示します

レジストリ:レジストリ キーの表示を開きます

電源。電源通知オブジェクトを表示します

ハンドル:スレッドの表示、ファイル、およびイベント処理の割り当て

<span id="-trace_TraceIndex"></span><span id="-trace_traceindex"></span><span id="-TRACE_TRACEINDEX"></span>**-トレース** *TraceIndex*トレースの指定したインデックスのスタック トレースが表示されます。 一部の構造は、スタック トレースを識別するために、この 16 ビットのインデックス番号を使用します。 このインデックスは、スタック トレースのデータベース内の場所を指します。

<span id="-cnt"></span><span id="-CNT"></span>**-cnt**グローバル カウンターの一覧を表示します。

<span id="-brk___BreakEventType__"></span><span id="-brk___breakeventtype__"></span><span id="-BRK___BREAKEVENTTYPE__"></span>**-brk \[**  *BreakEventType* **\]** 中断イベントを指定します。 *BreakEventType*は中断イベントの型の数です。 使用可能な型は、の一覧と、現在の中断イベントの設定の一覧は、次のように入力します。 **! avrf brk**します。

<span id="-flt___EventType_Probability__"></span><span id="-flt___eventtype_probability__"></span><span id="-FLT___EVENTTYPE_PROBABILITY__"></span>**-flt \[**  *EventType 確率* **\]** フォールト インジェクションを指定します。 *EventType*は型のイベント数です。 *確率*イベントが失敗する頻度です。 0 ~ 1,000,000 (0xF4240) 整数を指定できます。 入力した場合 **! avrf flt**追加パラメーターには、現在のフォールト インジェクション設定が表示されます。

<span id="-flt_break_EventType"></span><span id="-flt_break_eventtype"></span><span id="-FLT_BREAK_EVENTTYPE"></span>-**flt break** *EventType* Application Verifier をそれぞれのデバッガーを中断すると、時間で指定された、このエラー *EventType*、挿入されます。

<span id="-flt_stacks_Length"></span><span id="-flt_stacks_length"></span><span id="-FLT_STACKS_LENGTH"></span>**-flt スタック***長さ*表示*長さ*最新フォールト挿入操作のスタック トレースの数。

<span id="-trg___Start_End___dll_Module___all____"></span><span id="-trg___start_end___dll_module___all____"></span><span id="-TRG___START_END___DLL_MODULE___ALL____"></span>**-trg \[**  *開始終了* **| dll** *モジュール* **| すべて\]** ターゲット範囲を指定します。 *開始*は対象範囲の先頭アドレスです。 *終了*は対象範囲の終了アドレスです。 *モジュール*(.exe または .dll 拡張子を含むが、パスは含まれません) の名前を指定の対象とするモジュール。 入力した場合 **- trg すべて**、すべての対象範囲がリセットされます。 入力した場合 **- trg**追加パラメーターなしに、現在の対象範囲が表示されます。

<span id="-skp___Start_End___dll_Module___all___Time____"></span><span id="-skp___start_end___dll_module___all___time____"></span><span id="-SKP___START_END___DLL_MODULE___ALL___TIME____"></span>**-skp \[**  *開始終了* **| dll** *モジュール* **| すべて |***時間* **\]** 除外範囲を指定します。 *開始*除外範囲の先頭アドレスです。 *終了*除外範囲の終了アドレスです。 モジュールには、対象となるまたは除外するモジュールの名前を指定します。 *モジュール*(.exe または .dll 拡張子を含むが、パスは含まれません) の名前を指定すると、除外するモジュールの。 入力した場合 **- skp すべて**、すべての対象範囲または除外範囲をリセットします。 入力した場合、*時間*値のすべてのエラーが抑制されます*時間*実行再開までのミリ秒。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アプリケーション検証ツールとドキュメント、ダウンロードしてインストールする方法については、[Application Verifier](application-verifier.md)を参照してください。

<a name="remarks"></a>注釈
-------

ときに、 **! avrf**パラメーターなしで拡張機能を使うと、現在 Application Verifier のオプションが表示されます。 場合、**完全ページ ヒープ**または**高速の塗りつぶしヒープ**オプションが有効になって、アクティブなページに関する情報は、ヒープにも表示されます。 いくつかの例については、Application Verifier のドキュメントで「ヒープ操作ログ」を参照してください。

アプリケーションの検証機能停止が発生した場合、 **! avrf**パラメーターなしで拡張機能が停止し、その原因の性質によって示されます。 いくつかの例については、Application Verifier ドキュメント「アプリケーション検証ツールが停止のデバッグ」を参照してください。

Ntdll.dll と verifier.dll 用のシンボルは、不足している場合、 **! avrf**拡張機能には、エラー メッセージが生成されます。 この問題に対処する方法については、Application Verifier のドキュメントで"設定をデバッガーの Application Verifier"を参照してください。

 

 






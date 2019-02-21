---
title: スタックが作成され、ログのダンプ
description: スタックが作成され、ログのダンプ
ms.assetid: 5FE6AA76-5299-4d5d-9154-6DB34D93EECB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58aeb88821a8ea4ba02dab7f41906a6fc84eeecb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557811"
---
# <a name="stack-and-dump-logging"></a>スタックが作成され、ログのダンプ


## <a name="span-idusingstacktraceonerrorandminidumponerrorswitchesspanspan-idusingstacktraceonerrorandminidumponerrorswitchesspanspan-idusingstacktraceonerrorandminidumponerrorswitchesspanusing-stacktraceonerror-and-minidumponerror-switches"></a><span id="Using__stacktraceonerror_and__minidumponerror_switches"></span><span id="using__stacktraceonerror_and__minidumponerror_switches"></span><span id="USING__STACKTRACEONERROR_AND__MINIDUMPONERROR_SWITCHES"></span>スイッチの/stacktraceonerror と/minidumponerror を使用します。


スタック トレースをキャプチャする 2 つの方法がありますが、ミニ ダンプは、テストから。 'Onerror' モードは、最も簡単なのです。 テストを実行するときは、te を指定します。 '/stacktraceonerror' や '/minidumponerror' スイッチ。 次に、エラーが発生した場合ロガーはキャプチャ、スタック トレースやミニ ダンプが既定の形式で。

スタック トレースとミニ ダンプをキャプチャするその他のメソッドでは、後で説明する Api を使用します。

## <a name="span-idusingwexdebughfunctionalitytocapturestacktracesandminidumpsspanspan-idusingwexdebughfunctionalitytocapturestacktracesandminidumpsspanusing-wexdebugh-functionality-to-capture-stack-traces-and-mini-dumps"></a><span id="using_wexdebug.h_functionality_to_capture_stack_traces_and_mini_dumps"></span><span id="USING_WEXDEBUG.H_FUNCTIONALITY_TO_CAPTURE_STACK_TRACES_AND_MINI_DUMPS"></span>スタック トレースとミニ ダンプをキャプチャする WexDebug.h 機能を使用します。


WexDebug.h 呼び出しスタック トレースをキャプチャするための Api を提供して、ミニ ダンプします。

### <a name="span-idcallsavedumpapitosaveaminidumpspanspan-idcallsavedumpapitosaveaminidumpspanspan-idcallsavedumpapitosaveaminidumpspancall-savedump-api-to-save-a-mini-dump"></a><span id="Call_SaveDump_API_to_save_a_mini_dump."></span><span id="call_savedump_api_to_save_a_mini_dump."></span><span id="CALL_SAVEDUMP_API_TO_SAVE_A_MINI_DUMP."></span>ミニ ダンプを保存する SaveDump API を呼び出します。

この API は、省略可能な DWORD パラメーター (これは、ダンプ フラグを入力またはフラグの組み合わせ) と文字列の参照をその戻り、保存されたダンプ ファイルへのパスとファイルの名前を含む文字列。 ファイル名では、API によって自動的に生成され、現在の日付と時刻に基づきます。

ダンプの省略可能な型のパラメーターは、実行のミニ ダンプに含める必要がありますを指定します。 これもかを指定するかどうか、ダンプ、dmp に保存されますまたは cab ファイルの場合は、cab ファイル、シンボルは、ダンプと共に保存されます。 省略可能なパラメーターを省略した場合は、既定の設定が使用されます。

例 (その pdb と共に cab にダンプ) 保存:

```cpp
NoThrowString savedDumpFilePath;
HRESULT hr = Debug::SaveDump(MiniDumpFormat::WriteCab | MiniDumpFormat::WriteCabSecondaryFiles, savedDumpFilePath);
```

メモ、cab ファイルにダンプを保存する通常のダンプを保存するよりも時間がかかるさらに時間がかかりますシンボル ファイルを添付します。

### <a name="span-idcallgetstackapitoobtainacallstacktracespanspan-idcallgetstackapitoobtainacallstacktracespanspan-idcallgetstackapitoobtainacallstacktracespancall-getstack-api-to-obtain-a-call-stack-trace"></a><span id="Call_GetStack_API_to_obtain_a_call_stack_trace."></span><span id="call_getstack_api_to_obtain_a_call_stack_trace."></span><span id="CALL_GETSTACK_API_TO_OBTAIN_A_CALL_STACK_TRACE."></span>呼び出し履歴のトレースを取得する GetStack API を呼び出します。

この API は、省略可能な DWORD パラメーター (これは、型フラグを設定またはフラグの組み合わせ) とで文字列を返しますが、現在のコンテキストのコール スタック トレースを格納している文字列参照。

オプションのスタックの型パラメーターでは、スタック トレースに含める必要がありますを指定します。 省略可能なパラメーターを省略した場合は、既定の設定が使用されます。

以下に例を示します。

```cpp
NoThrowString stackText;
HRESULT hr = Debug::GetStack(CallStackFormat::ColumnNames | CallStackFormat::FrameAddress |
                             CallStackFormat::SourceLine, stackText);
```

スタックのオプションの相関関係は、デバッガー コマンドをするフラグします。 デバッガーの windbg ファミリを使用する場合、次のおおよその相関関係の一覧が役に立つ。


| デバッガーの構文 |          対応するフラグ          |
|-----------------|---------------------------------------|
|        k        |     CallStackFormat::ColumnNames      |
|       kv        |   k + CallStackFormat::FunctionInfo   |
|     kp/kP     |    k + CallStackFormat::Parameters    |
|       kn        |   k + CallStackFormat::FrameNumbers   |
|       kf        | k + CallStackFormat::FrameMemoryUsage |

## <a name="span-idtechnicalreferencespanspan-idtechnicalreferencespanspan-idtechnicalreferencespantechnical-reference"></a><span id="Technical_Reference"></span><span id="technical_reference"></span><span id="TECHNICAL_REFERENCE"></span>テクニカル リファレンス


ダンプとスタックの省略可能なパラメーターについての詳細について関心がある場合に付属のマニュアルを参照してください[ツールを Windows のデバッグ](https://go.microsoft.com/fwlink/p/?linkid=8708)します。 'ダンプ フラグ' 参照に関するドキュメントについては、[デバッグ\_形式\_XXX ドキュメント](https://msdn.microsoft.com/library/cc267446.aspx)します。 ドキュメントに 'スタック フラグ' を参照してください、 ['OutputStackTrace' メソッドのドキュメント](https://msdn.microsoft.com/library/cc266034.aspx)します。










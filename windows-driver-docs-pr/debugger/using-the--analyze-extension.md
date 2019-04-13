---
title: 分析の拡張機能を使用
description: 分析の拡張機能を使用
ms.assetid: 0aa74153-e992-4d1c-b734-ccc60cff452c
keywords:
- 拡張機能の例を分析します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24547e89ed4a3a7c09fb8c43e0645fddd34dac6c
ms.sourcegitcommit: c340d6058fa3ea6407d0041de80482b88f623a90
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "59534158"
---
# <a name="using-the-analyze-extension"></a>!analyze 拡張機能の使用


## <span id="ddk_using_the_analyze_extension_dbg"></span><span id="DDK_USING_THE_ANALYZE_EXTENSION_DBG"></span>


クラッシュした対象のコンピューターまたはアプリケーションのデバッグの最初の手順は、使用する、 [ **! 分析**](-analyze.md)拡張機能コマンド。

この拡張機能は、膨大な自動分析を実行します。 この分析の結果は、デバッガー コマンド ウィンドウに表示されます。

使用する必要があります、 **-v**データの完全な詳細の表示のオプション。 その他のオプションについて詳しくは、次を参照してください。、 [ **! 分析**](-analyze.md)リファレンス ページです。

このトピックの内容は次のとおりです。

- ユーザー モードです-v 例の分析。
- カーネル モード-v 例の分析。
- フォロー アップ フィールドと triage.ini ファイル
- 追加! 手法の分析

### <a name="span-idddkausermodeanalyzevexampledbgspanspan-idddkausermodeanalyzevexampledbgspana-user-mode-analyze--v-example"></a><span id="ddk_a_user_mode_analyze_v_example_dbg"></span><span id="DDK_A_USER_MODE_ANALYZE_V_EXAMPLE_DBG"></span>ユーザー モードです-v 例の分析。

この例では、デバッガーは例外が発生したユーザー モード アプリケーションにアタッチされます。

```dbgcmd
0:000> !analyze -v
*******************************************************************************
*                                                                             *
*                        Exception Analysis                                   *
*                                                                             *
*******************************************************************************

Debugger SolutionDb Connection::Open failed 80004005
```

インターネットに接続している場合、デバッガーは Microsoft によって管理されるクラッシュ ソリューションのデータベースにアクセスしようとします。 ここでは、コンピューターでインターネットにアクセスできなかったか、または web サイトが機能しないことを示す、エラー メッセージが表示されます。

```dbgcmd
FAULTING_IP: 
ntdll!PropertyLengthAsVariant+73
77f97704 cc               int     3
```

FAULTING\_IP フィールドには、障害の時点で、命令ポインターが表示されます。

```dbgcmd
EXCEPTION_RECORD:  ffffffff -- (.exr ffffffffffffffff)
ExceptionAddress: 77f97704 (ntdll!PropertyLengthAsVariant+0x00000073)
   ExceptionCode: 80000003 (Break instruction exception)
  ExceptionFlags: 00000000
NumberParameters: 3
   Parameter[0]: 00000000
   Parameter[1]: 00010101
   Parameter[2]: ffffffff
```

例外\_レコード フィールドには、このクラッシュ例外レコードが表示されます。 この情報を使用しても表示できます、 [ **.exr (例外レコードの表示)** ](-exr--display-exception-record-.md)コマンド。

```dbgcmd
BUGCHECK_STR:  80000003
```

バグチェック\_STR フィールドには、例外コードが表示されます。 名前は、名称: 用語*バグ チェック*実際には、カーネル モードのクラッシュを示します。 ユーザー モードのデバッグ、例外コードを表示する: この場合、0x80000003 します。

```dbgcmd
DEFAULT_BUCKET_ID:  APPLICATION_FAULT
```

既定の\_バケット\_ID フィールドには、このエラーが属しているエラーの一般的なカテゴリが表示されます。

```dbgcmd
PROCESS_NAME:  MyApp.exe
```

プロセス\_名フィールドは、例外が発生したプロセスの名前を指定します。

```dbgcmd
LAST_CONTROL_TRANSFER:  from 01050963 to 77f97704
```

最後の\_コントロール\_転送フィールドには、スタック上の最後の呼び出しが表示されます。 この場合、アドレス 0x01050963 にコードでは、0x77F97704 で関数が呼び出されます。 これらのアドレスを使用することができます、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)コマンドでこれらのアドレスが存在するどのようなモジュールと関数の決定をします。

```dbgcmd
STACK_TEXT:  
0006b9dc 01050963 00000000 0006ba04 000603fd ntdll!PropertyLengthAsVariant+0x73
0006b9f0 010509af 00000002 0006ba04 77e1a449 MyApp!FatalErrorBox+0x55 [D:\source_files\MyApp\util.c @ 541]
0006da04 01029f4e 01069850 0000034f 01069828 MyApp!ShowAssert+0x47 [D:\source_files\MyApp\util.c @ 579]
0006db6c 010590c3 000e01ea 0006fee4 0006feec MyApp!SelectColor+0x103 [D:\source_files\MyApp\colors.c @ 849]
0006fe04 77e11d0a 000e01ea 00000111 0000413c MyApp!MainWndProc+0x1322 [D:\source_files\MyApp\MyApp.c @ 1031]
0006fe24 77e11bc8 01057da1 000e01ea 00000111 USER32!UserCallWinProc+0x18
0006feb0 77e172b4 0006fee4 00000001 010518bf USER32!DispatchMessageWorker+0x2d0
0006febc 010518bf 0006fee4 00000000 01057c5d USER32!DispatchMessageA+0xb
0006fec8 01057c5d 0006fee4 77f82b95 77f83920 MyApp!ProcessQCQPMessage+0x3b [D:\source_files\MyApp\util.c @ 2212]
0006ff70 01062cbf 00000001 00683ed8 00682b88 MyApp!main+0x1e6 [D:\source_files\MyApp\MyApp.c @ 263]
0006ffc0 77e9ca90 77f82b95 77f83920 7ffdf000 MyApp!mainCRTStartup+0xff [D:\source_files\MyApp\crtexe.c @ 338]
0006fff0 00000000 01062bc0 00000000 000000c8 KERNEL32!BaseProcessStart+0x3d
```

スタック\_テキスト フィールドには、エラーが発生したコンポーネントのスタック トレースが表示されます。

```dbgcmd
FOLLOWUP_IP: 
MyApp!FatalErrorBox+55
01050963 5e               pop     esi

FOLLOWUP_NAME:  dbg

SYMBOL_NAME:  MyApp!FatalErrorBox+55

MODULE_NAME:  MyApp

IMAGE_NAME:  MyApp.exe

DEBUG_FLR_IMAGE_TIMESTAMP:  383490a9
```

ときに[ **! 分析**](-analyze.md) 、エラーの原因となった可能性がありますが、命令を判断します、フォロー アップの表示、\_IP フィールド。 シンボル\_名、モジュール\_名前、イメージ\_名、およびデバッグ\_FLR\_イメージ\_タイムスタンプ フィールドを表示、シンボル、モジュール、イメージ名、およびこれに対応するイメージのタイムスタンプ命令。

```dbgcmd
STACK_COMMAND:  .ecxr ; kb
```

スタック\_コマンド フィールドには、スタックを取得するために使用されたコマンドが表示されます。\_テキスト。 このコマンドを使用してこのスタック トレースの表示を繰り返すまたはスタックの関連情報を取得するように変更できます。

```dbgcmd
BUCKET_ID:  80000003_MyApp!FatalErrorBox+55
```

バケット\_ID フィールドには、現在のエラーが属しているエラーの特定のカテゴリが表示されます。 このカテゴリでは、デバッガーで分析の出力に表示するその他の情報を確認するのに役立ちます。

```dbgcmd
Followup: dbg
---------
```

については、フォロー アップ\_名と、フォロー アップ フィールドは、フォロー アップ フィールドと triage.ini ファイルを参照してください。

さまざまな表示されるその他のフィールドがあります。

-   コントロールが FAULTING し、無効なアドレスに転送されたかどうか\_IP フィールドには、この無効なアドレスにが含まれます。 フォロー アップではなく\_IP フィールドに、失敗\_命令\_アドレス フィールドは、この逆アセンブリが意味のない可能性がありますが、このアドレスからの逆アセンブルしたコードに表示されます。 この場合、シンボル\_名、モジュール\_名前、イメージ\_名、およびデバッグ\_FLR\_イメージ\_タイムスタンプ フィールドはこの命令の呼び出し元を参照してください。

-   1 つが生じる場合は、プロセッサが misfires\_ビット\_エラー、2 つ\_ビット\_エラー、または実行可能な\_無効な\_コントロール\_転送フィールド。

-   メモリの破損は、CHKIMG、発生したかどうかは\_拡張フィールドを指定、 [ **! chkimg** ](-chkimg.md)拡張機能コマンドで調査するために使用する必要があります。

### <a name="span-idddkakernelmodeanalyzevexampledbgspanspan-idddkakernelmodeanalyzevexampledbgspana-kernel-mode-analyze--v-example"></a><span id="ddk_a_kernel_mode_analyze_v_example_dbg"></span><span id="DDK_A_KERNEL_MODE_ANALYZE_V_EXAMPLE_DBG"></span>カーネル モード-v 例の分析。

この例では、デバッガーはだけがクラッシュしたコンピューターにアタッチされます。

```dbgcmd
kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DRIVER_IRQL_NOT_LESS_OR_EQUAL (d1)
An attempt was made to access a pagable (or completely invalid) address at an
interrupt request level (IRQL) that is too high.  This is usually
caused by drivers using improper addresses.
If kernel debugger is available get stack backtrace.
```

表示の最初の要素は、確認コードとこの種類のバグ チェックについて、バグを示します。 表示されるテキストの一部は、この特定のインスタンスには適用されません可能性があります。 各バグ チェックの詳細については、次を参照してください。、[バグ チェック コード参照](bug-check-code-reference2.md)セクション。

```dbgcmd
Arguments:
Arg1: 00000004, memory referenced
Arg2: 00000002, IRQL
Arg3: 00000001, value 0 = read operation, 1 = write operation
Arg4: f832035c, address which referenced memory
```

バグ チェック パラメーターは、次に表示されます。 これらはそれぞれ後に説明します。 たとえば、3 番目のパラメーターが 1、およびそれに続くコメントは、書き込み操作が失敗したことを示すこのことについて説明します。

```dbgcmd
## Debugging Details:


WRITE_ADDRESS:  00000004 Nonpaged pool

CURRENT_IRQL:  2
```

次のほとんどのフィールドは、クラッシュの性質によって異なりません。 この場合、書き込みがわかります\_アドレスと現在\_IRQL フィールド。 バグの検査パラメーターに表示される情報の書き換えこれらは単純にします。 ステートメント"非ページ プール"を「ユーザーがページング可能な (または完全に無効な) アドレスにアクセスしようとするいるとしました」というバグ チェックのテキストを比較すると、アドレスが有効でないことがわかります。 無効なアドレスは、ここで 0x00000004 をしました。

```dbgcmd
FAULTING_IP: 
USBPORT!USBPORT_BadRequestFlush+7c
f832035c 894204           mov     [edx+0x4],eax
```

FAULTING\_IP フィールドには、障害の時点で、命令ポインターが表示されます。

```dbgcmd
DEFAULT_BUCKET_ID:  DRIVER_FAULT
```

既定の\_バケット\_ID フィールドには、このエラーが属しているエラーの一般的なカテゴリが表示されます。

```dbgcmd
BUGCHECK_STR:  0xD1
```

バグチェック\_STR フィールドは、既に見たバグ チェック コードを示します。 場合によっては、追加のトリアージ情報が追加されます。

```dbgcmd
TRAP_FRAME:  f8950dfc -- (.trap fffffffff8950dfc)
.trap fffffffff8950dfc
ErrCode = 00000002
eax=81cc86dc ebx=81cc80e0 ecx=81e55688 edx=00000000 esi=81cc8028 edi=8052cf3c
eip=f832035c esp=f8950e70 ebp=f8950e90 iopl=0         nv up ei pl nz ac po nc
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00010216
USBPORT!USBPORT_BadRequestFlush+7c:
f832035c 894204           mov     [edx+0x4],eax     ds:0023:00000004=????????
.trap
Resetting default context
```

トラップ\_フレーム フィールドには、このクラッシュのトラップ フレームが表示されます。 この情報を使用しても表示できます、 [ **.trap (表示トラップ フレーム)** ](-trap--display-trap-frame-.md)コマンド。

```dbgcmd
LAST_CONTROL_TRANSFER:  from f83206e0 to f832035c
```

最後の\_コントロール\_転送フィールドには、スタック上の最後の呼び出しが表示されます。 この場合、アドレス 0xF83206E0 にコードでは、0xF832035C で関数が呼び出されます。 使用することができます、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)コマンドでこれらのアドレスが存在するどのようなモジュールと関数の決定をします。

```dbgcmd
STACK_TEXT:  
f8950e90 f83206e0 024c7262 00000000 f8950edc USBPORT!USBPORT_BadRequestFlush+0x7c
f8950eb0 804f5561 81cc8644 81cc8028 6d9a2f30 USBPORT!USBPORT_DM_TimerDpc+0x10c
f8950fb4 804f5644 6e4be98e 00000000 ffdff000 nt!KiTimerListExpire+0xf3
f8950fe0 8052c47c 8053cf20 00000000 00002e42 nt!KiTimerExpiration+0xb0
f8950ff4 8052c16a efdefd44 00000000 00000000 nt!KiRetireDpcList+0x31
```

スタック\_テキスト フィールドには、エラーが発生したコンポーネントのスタック トレースが表示されます。

```dbgcmd
FOLLOWUP_IP: 
USBPORT!USBPORT_BadRequestFlush+7c
f832035c 894204           mov     [edx+0x4],eax
```

フォロー アップ\_IP フィールドには、エラーの原因となった可能性がありますが、命令の逆アセンブリが表示されます。

```dbgcmd
FOLLOWUP_NAME:  usbtri

SYMBOL_NAME:  USBPORT!USBPORT_BadRequestFlush+7c

MODULE_NAME:  USBPORT

IMAGE_NAME:  USBPORT.SYS

DEBUG_FLR_IMAGE_TIMESTAMP:  3b7d868b
```

シンボル\_名、モジュール\_名前、イメージ\_名、および DBG\_FLR\_イメージ\_タイムスタンプ フィールドを表示、シンボル、モジュール、イメージ、およびこの命令に対応するイメージのタイムスタンプ(これが有効である)、または (がない) 場合は、この命令の呼び出し元にします。

```dbgcmd
STACK_COMMAND:  .trap fffffffff8950dfc ; kb
```

スタック\_コマンド フィールドには、スタックを取得するために使用されたコマンドが表示されます。\_テキスト。 このコマンドを使用してこのスタック トレースの表示を繰り返すまたはスタックの関連情報を取得するように変更できます。

```dbgcmd
BUCKET_ID:  0xD1_W_USBPORT!USBPORT_BadRequestFlush+7c
```

バケット\_ID フィールドには、現在のエラーが属しているエラーの特定のカテゴリが表示されます。 このカテゴリでは、デバッガーで分析の出力に表示するその他の情報を確認するのに役立ちます。

```dbgcmd
INTERNAL_SOLUTION_TEXT:  https://oca.microsoft.com/resredir.asp?sid=62&State=1
```

インターネットに接続している場合、デバッガーは Microsoft によって管理されるクラッシュ ソリューションのデータベースにアクセスしようとします。 このデータベースには、非常に多くの既知のバグに関する情報が Web ページへのリンクが含まれています。 問題、内部の一致が見つかったかどうか\_ソリューション\_テキスト フィールドが表示されます、URL の詳細については、アクセスできることです。

```dbgcmd
Followup: usbtri
---------

      This problem has a known fix.
      Please connect to the following URL for details:
      ------------------------------------------------
      https://oca.microsoft.com/resredir.asp?sid=62&State=1
```

については、フォロー アップ\_名前と、フォロー アップ フィールドと triage.ini ファイルを参照してください、フォロー アップ フィールド。

さまざまな表示されるその他のフィールドがあります。

-   コントロールが FAULTING し、無効なアドレスに転送されたかどうか\_IP フィールドには、この無効なアドレスにが含まれます。 フォロー アップではなく\_IP フィールドに、失敗\_命令\_アドレス フィールドは、この逆アセンブリが意味のない可能性がありますが、このアドレスからの逆アセンブルしたコードに表示されます。 この場合、シンボル\_名、モジュール\_名前、イメージ\_名、および DBG\_FLR\_イメージ\_タイムスタンプ フィールドはこの命令の呼び出し元を参照してください。

-   1 つが生じる場合は、プロセッサが misfires\_ビット\_エラー、2 つ\_ビット\_エラー、または実行可能な\_無効な\_コントロール\_転送フィールド。

-   メモリの破損は、CHKIMG、発生したかどうかは\_拡張フィールドを指定、 [ **! chkimg** ](-chkimg.md)拡張機能コマンドで調査するために使用する必要があります。

-   その名前をバグチェックに表示される可能性のバグ チェックがデバイス ドライバーのコード内で発生した場合\_ドライバー フィールド。

### <a name="span-idddkthefollowupfieldandthetriageinifiledbgspanspan-idddkthefollowupfieldandthetriageinifiledbgspanthe-followup-field-and-the-triageini-file"></a><span id="ddk_the_followup_field_and_the_triage_ini_file_dbg"></span><span id="DDK_THE_FOLLOWUP_FIELD_AND_THE_TRIAGE_INI_FILE_DBG"></span>フォロー アップ フィールドと triage.ini ファイル

ユーザー モードおよびカーネル モードのどちらも、表示のフォロー アップ フィールドはこれを判断する場合に、現在のスタック フレームの所有者に関する情報を表示します。 この情報は、次のように決定されます。

1.  ときに、 [ **! 分析**](-analyze.md)拡張機能を使用すると、デバッガーは、スタックの最上位のフレームで始まるし、エラーの原因があるかどうかを決定します。 いない場合は、次のフレームが分析されます。 このプロセスは、エラーになる可能性があるフレームが見つかるまで続きます。

2.  デバッガーは、このフレームの関数、モジュールの所有者を特定しようとします。 所有者を特定できる場合、このフレームが障害であると見なされます。

3.  所有者を特定できない場合、所有者が決定されます (または、スタックを完全に検査) までに、次のスタック フレームと、デバッガーを渡します。 所有者がこの検索で見つかった最初のフレームは、エラーであると見なされます。 情報を検索するせず、スタックがなくなった場合は、フォロー アップのフィールドは表示されません。

4.  エラー時のフレームの所有者は、フォロー アップのフィールドに表示されます。 場合 **! 分析-v**は、フォロー アップを使用します\_IP、シンボル\_名、モジュール\_名前、イメージ\_名、および DBG\_FLR\_イメージ\_。このフレームのタイムスタンプ フィールドが参照してください。

フォロー アップ フィールドで役に立つ情報を表示するには、まずモジュールおよび関数の所有者の名前を含む Triage.ini ファイルを作成する必要があります。

Triage.ini ファイルには、エラーの可能性がありますすべてのモジュールの所有者を識別する必要があります。 実際の所有者ではなく、情報の文字列を使用できますが、この文字列は、スペースを含めることはできません。 モジュールがエラーがない場合は、このモジュールを省略するか、スキップするかを示すことができます。 トリアージ プロセス、さらに細かい粒度を与える個々 の関数の所有者を指定することもできます。

Triage.ini ファイルの構文について詳しくは、次を参照してください。[モジュールを指定すると、関数の所有者](specifying-module-and-function-owners.md)します。

### <a name="span-idddkadditionalanalyzetechniquesdbgspanspan-idddkadditionalanalyzetechniquesdbgspanadditional-analyze-techniques"></a><span id="ddk_additional_analyze_techniques_dbg"></span><span id="DDK_ADDITIONAL_ANALYZE_TECHNIQUES_DBG"></span>追加! 手法の分析

信じがない場合、バケット\_ID が正しいこと、使用して、バケットの選択をオーバーライドする[ **! 分析**](-analyze.md)で、 **-d**パラメーター。

クラッシュまたは例外が発生しなかった場合[ **! 分析**](-analyze.md)ターゲットの現在の状態を提供する非常に短いテキストが表示されます。 特定の状況で、分析、クラッシュが発生しましたかのように実行を強制します。 使用 **!-f 分析**このタスクを実行します。

ユーザー モード、例外が発生しましたが、基になる問題は、スレッドがハングしたと思われる場合、現在のスレッドに設定し、使用して、調査しているスレッド **! analyze - ハング**します。 この拡張機能では、すべてのスレッドが他のスレッドをブロックしてかどうかを判断するスレッド スタック分析を実行します。

カーネル モードでバグ チェックが発生しましたが、基になると思われる場合、問題、ハングしたスレッドを使用して、 **! analyze - ハング**します。 この拡張機能は、システムによって保持されているロックを調査および DPC をスキャン キューのチェーンとハングのスレッドがないが表示されます。 問題は、カーネル モードのリソース デッドロックと確信できる場合、 [ **! デッドロック**](-deadlock.md)と共に拡張機能、**デッドロック検出**Driver Verifier のオプション。

既知の問題も自動的に無視できます。 これを行うには、まず、書式設定された既知の問題の一覧を含む XML ファイルを作成する必要があります。 使用して、**!-c 分析-読み込み * * * KnownIssuesFile*拡張機能をこのファイルを読み込めません。 例外または中断が発生するを使用して、 **!-c 分析**拡張機能。 例外には、既知の問題のいずれかが一致すると、ターゲットは実行を再開します。 ターゲットは、実行を再開しないかどうかを使用して **! 分析-v**問題の原因を特定します。 Sdk サンプルの XML ファイルが見つかりません\\サンプル\\分析\_デバッガーのインストール ディレクトリのサブディレクトリを続行します。

 

 






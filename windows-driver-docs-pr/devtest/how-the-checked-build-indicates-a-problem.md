---
title: チェック ビルドで問題が示される方法
description: チェック ビルドで問題が示される方法
ms.assetid: 373519e0-bca9-434e-8cc3-e11c2d4b42a4
keywords:
- チェック済みビルドの WDK、問題通知
- 通知 WDK チェックビルド
- WDK チェックビルドをアサートします
- ブレークポイント WDK
- デバッガーメッセージ WDK
- メッセージ WDK チェック済みビルド
- WDK チェックされたビルドのエラー
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3234192f15cbd2e365536918e73d5370d540df65
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999065"
---
# <a name="how-the-checked-build-indicates-a-problem"></a>チェック ビルドで問題が示される方法

## <span id="ddk_how_the_checked_build_indicates_a_problem_tools"></span><span id="DDK_HOW_THE_CHECKED_BUILD_INDICATES_A_PROBLEM_TOOLS"></span>

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

オペレーティングシステムのチェックされたビルドでは、さまざまな方法を使用して、検出された問題を通知します。 これらのメソッドには、アサートエラー、ブレークポイント、およびデバッガーメッセージが含まれます。 これらのメソッドはすべて、カーネルデバッガーからの出力になります。 そのため、有効にするには、カーネルモードのデバッガー (WinDbg、KD など) が接続されているチェックを実行する必要があります。

デバッグの詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

### <a name="span-idassert_failuresspanspan-idassert_failuresspanassert-failures"></a><span id="assert_failures"></span><span id="ASSERT_FAILURES"></span>アサートエラー

チェックを実行したビルドが実行するチェックのほとんどは、 [**ASSERT**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))ステートメントとして実装されます。 アサートされた式が**FALSE**と評価されると、次のものを含むメッセージがデバッガーによって表示されます。

-   失敗したコード式のテキスト

-   失敗したアサートルーチンのソースコードパス、ファイル名、および行番号

次の例は、i/o マネージャーでアサートが失敗したときにデバッガーによって表示される出力を示しています。

```
*** Assertion failed: Irp->IoStatus.Status != 0xffffffff
***   Source File: D:\nt\private\ntos\io\iosubs.c, line 3305

0:Break, Ignore, Terminate Process or Terminate Thread (bipt)? b
0:Execute '!cxr BD94B918' to dump context
Break instruction exception - code 80000003 (first chance)
ntkrnlmp!DbgBreakPoint:
804a3ce4 cc               int     3
```

デバッガーの出力に示されているように、ユーザーは "中断、無視、プロセスの終了、またはスレッドの終了" を求められます。 ユーザーは "b" を入力して応答しました。これにより、デバッガーはブレークポイントによるシステムの実行を停止します。 その結果、ユーザーは、検出された問題のデバッグを続行できるようになります。

失敗したアサートがシステムに与える影響は、さまざまな要因によって異なります。 Windows Vista より前のバージョンの Windows では、システムのスタートアッププロセス中にオペレーティングシステムに対してデバッグが有効にされている場合、システムはデバッガーを中断します (接続されている場合)。または、デバッガーが接続されるのを待機しています。 デバッグが有効になっていない場合、パラメーター1の値が0x80000003 で\_ある\_[**バグチェック 0x1e**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x1e--kmode-exception-not-handled) (kmode 例外は処理されません\_) でシステムがクラッシュします。 Windows Vista 以降では、デバッガーが接続されている場合にのみ、システムはデバッガーを中断します。 デバッグが有効になっていない場合、またはデバッグが有効になっていて、デバッガーが接続されていない場合は、失敗したアサーションは報告されません (ただし、アサーションチェックは実行されます)。 デバッグが有効になっていてもデバッガーが接続されていない場合に、ドライバーを開発しているときにデバッガーをランダムに中断する場合は、コード内で[**Dbgbreakpoint ポイント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)ステートメントを使用できます。

一部の[**アサート**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))エラーの前に、追加の[**dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)出力があります。 この種類のアサートの一般的な例の1つは、次のように ntddk と wdm で定義されている、チェックを行うドライバーのビルドで使用する、次の[**ページ\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロです。

```
#define PAGED_CODE() \
    if (KeGetCurrentIrql() > APC_LEVEL) { \
KdPrint(( "EX: Pageable code called at IRQL %d\n", KeGetCurrentIrql() )); \
        ASSERT(FALSE); \
        }
```

このマクロは、ページング可能な関数が適切な IRQLs でのみ呼び出されることを確認するために、オペレーティングシステム内で頻繁に使用されます。

通常、失敗したコード式のテキストを調べて、アサートが発生したときのドライバーのアクションや呼び出された関数など、アサートの原因を判断できます。 この分析には、 **KB (スタックトレースの表示)** デバッガーコマンドが不可欠です。

最も一般的なアサート呼び出しの一覧については、「 [Checked Build assert](checked-build-asserts.md)」を参照してください。

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>区切り

チェックされたビルドでは、ブレークポイントを使用して問題を示すこともできます。 多くの場合、ブレークポイントの前に[**Dbgprint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)ステートメントがあります。これにより、発生した問題に関する情報がデバッガーに表示されます。 ブレークポイントが発生したときにデバッガーがシステムに接続されていない場合、システムがクラッシュし、すべての説明メッセージが失われます。

チェックされたビルドのブレークポイントの前にあり、ドライバーライターによって検出された最も一般的なメッセージは、[チェックされた[ビルドブレークポイントとメッセージ](checked-build-breakpoints-and-messages.md)] に一覧表示されます。

次の例は、 **Dbgprint**呼び出しとブレークポイントがデバッガーにどのように表示されるかを示しています。

```
*** DPC routine > 1 sec --- This is not a break in KeUpdateSystemTime
Break instruction exception - code 80000003 (first chance)
NTOSKRNL!DbgBreakPoint:
804a3ce4 cc               int     3
```

この例では、1つの遅延プロシージャ呼び出し (DPC) が1秒以上実行されていたことを示すデバッガーメッセージと、チェックを行うビルドで実装されたチェックの種類を示します。 このブレークポイントは、ドライバーが DPC ルーチンで長い時間を費やしていることを意味します。これは、重大なドライバーの問題を示している可能性があります。 一方、このブレークポイントは、ドライバーが DPC ルーチンで大量のデバッグ出力を生成する場合にも発生します。これにより、DPC の実行に必要な時間が延長されます。 問題の根底にある原因を調べるには、DPC ルーチンが実行していることを確認し、ブレークポイントを1回または2回続けて続行します。

ブレークポイントが検出されてもメッセージが表示されないまれな状況では、( **KB**デバッガーコマンドを使用して) カーネルスタックトレースを調べて、ブレークポイントが検出された場所を判断することが重要です。 多くの場合、これにより、ブレークポイントの理由についての強力な手掛かりが得られます。

次の例は、多くの Windows ドライバー開発者がスタックトレースと共に見た共通のブレークポイントを示しています。

```
Break instruction exception - code 80000003 (first chance)
ntkrnlmp!SpinLockSpinningForTooLong:
8069aafd cc               int     3
1: kd> kb
ChildEBP RetAddr  Args to Child              
f9f77c4c 80103a6c f9f77c84 00000005 fa20e7df ntkrnlmp!SpinLockSpinningForTooLong
f9f77c58 fa20e7df 81b34930 e1558bd0 00180016 halmps!KfAcquireSpinLock+0x3c
f9f77c7c 80742683 000000ff 81ba6000 00000000 nothing+0x7df
f9f77d54 80742893 0000046c 81ba6000 f9f77d80 ntkrnlmp!IopLoadDriver+0x785
f9f77d78 805f8d2d 00000000 00000000 81fa88b8 ntkrnlmp!IopLoadUnloadDriver+0x75
f9f77dac 807cd14f f7d59ce8 00000000 00000000 ntkrnlmp!ExpWorkerThread+0x129
f9f77ddc 8069bece 805f8c04 00000001 00000000 ntkrnlmp!PspSystemThreadStartup+0x4d
00000000 00000000 00000000 00000000 00000000 ntkrnlmp!KiThreadStartup+0x16
```

このスタックトレースからわかるように、 **KfAcquireSpinLock**呼び出しの結果としてブレークポイントが取得されました。 Wdm を調べると、これが[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)としてドライバーによって参照される関数の実際の名前であることがわかります。 ブレークポイントの前にメッセージが表示されていない場合でも、スタックの一番上にあるブレークポイントの位置を確認できます (**ntkrnlmp!SpinLockSpinningForTooLong**)。 この場所は、ブレークポイントの理由を示しています。スピンロックは、異常に長い間、スピンロックがスピンしています。

### <a name="span-iddebugger_messagesspanspan-iddebugger_messagesspandebugger-messages"></a><span id="debugger_messages"></span><span id="DEBUGGER_MESSAGES"></span>デバッガーメッセージ

チェックを行ったビルドでは、デバッガーメッセージを使用して、発生したエラーに関する追加情報を識別したり、提供したりすることもできます。 デバッガーメッセージの最も一般的な原因は、カーネル以外のコンポーネントや HAL 以外のコンポーネントから発生したエラー、またはチェックされた (デバッグ) ユーザーモードのプログラムです。 出力の量は、各オペレーティングシステムのリリースによって異なります。

次の例は、完全にチェックされたビルドのインストールによって表示される可能性がある出力を示しています。 この出力は、Windows XP のプレリリース版によって生成されたものであるため、通常は完全にチェックされたビルドで見られるよりも多くの voluminous です。

```
0:Attempting to load winsock
0:Checking for presence of ws2_32
0:Looking in ws2_32 for getaddrinfo
0:AudioSrv: 1:CreateSessionUserSid: GetCurrentUserTokenW failed, LastError=1245
1:AudioSrv: RegOpenConsoleUser: no console sid
0:(s: 0 0xc4.d0 winlogon.exe) USRK-[Wrn=170] CloseDesktop: Desktop 0X81CEAF78 still in use by thread 0XE16F3EA0
0:GetWinStationUserToken: Error 1702 getting UserToken LogonId 0
1:AudioSrv: InitializeForNewConsoleUser: User SID S-1-5-21-329068152-1292428093-1547161642-500
1:(s: 0 0x240.3a8 spoolsv.exe) USRK-[Wrn=1400] ValidateHwnd: Invalid hwnd (0X0000FFFF)
0:(s: 0 0x240.3a8 spoolsv.exe) USRK-[Wrn=1400] ValidateHwnd: Invalid hwnd (0X0000FFFF)
0:bReadUserSystemEUDCRegistry():fail NtStatus - c0000000
0:GDI: GDISRV:Fail to read system wide eudc
0:
1:TERMSRV : Not Personal Workstation
0:(s: 0 0x260.3c4 Explorer.EXE) USER-[Wrn=1400] HMValidateHandle: Invalid:00000000 Type:0x1
0:(s: 0 0x260.3c4 Explorer.EXE) USER-[Wrn=1400] HMValidateHandle: Invalid:00000000 Type:0x1
0:(s: 0 0x260.3c4 Explorer.EXE) USER-[Wrn=1400] HMValidateHandle: Invalid:00000000 Type:0x1
```

ドライバーのデバッグ中にチェックされたビルドが表示できる最も一般的なメッセージのいくつかは、[[チェック済みビルドのブレークポイントとメッセージ](checked-build-breakpoints-and-messages.md)] に一覧表示されています。

さまざまなシステムコンポーネントで追加のトレースメッセージまたは情報メッセージを有効にすると、後続のブレークポイントやアサートエラーが発生することなくデバッガーメッセージが発生することもあります。

 

 






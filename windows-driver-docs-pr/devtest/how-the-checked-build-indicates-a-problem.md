---
title: チェック ビルドで問題が示される方法
description: チェック ビルドで問題が示される方法
ms.assetid: 373519e0-bca9-434e-8cc3-e11c2d4b42a4
keywords:
- チェック ビルド WDK、問題の通知
- 通知 WDK ビルドの確認
- WDK のチェック ビルドをアサートします。
- WDK のブレークポイント
- WDK のメッセージをデバッガーします。
- WDK のメッセージがビルドを確認
- WDK のエラー チェック ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0d1c435766b512fb6af883cf70bf416ef2e6d7e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372688"
---
# <a name="how-the-checked-build-indicates-a-problem"></a>チェック ビルドで問題が示される方法


## <span id="ddk_how_the_checked_build_indicates_a_problem_tools"></span><span id="DDK_HOW_THE_CHECKED_BUILD_INDICATES_A_PROBLEM_TOOLS"></span>


オペレーティング システムのチェック ビルドでは、さまざまな方法を使用して、見つけた問題の通知。 これらのメソッドには、アサート エラー、ブレークポイントおよびデバッガーのメッセージが含まれます。 これらのメソッドのすべては、カーネル デバッガーからの出力になります。 したがってに便利ですが、接続されているカーネル モード デバッガー (WinDbg、KD など) を使用してチェック ビルドを実行する必要があります。

デバッグの詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)します。

### <a name="span-idassertfailuresspanspan-idassertfailuresspanassert-failures"></a><span id="assert_failures"></span><span id="ASSERT_FAILURES"></span>アサート失敗

チェック ビルドが実行されるチェックの大部分として実装されて[ **ASSERT** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))ステートメント。 式がアサートされていると評価される場合**FALSE**デバッガーを含むメッセージが表示されます。

-   失敗したコード式のテキスト

-   ソース コードのパス、ファイル名、および失敗したアサートのルーチンの行番号

次の例では、デバッガーがアサートが I/O マネージャーが失敗したときに表示する出力を示します。

```
*** Assertion failed: Irp->IoStatus.Status != 0xffffffff
***   Source File: D:\nt\private\ntos\io\iosubs.c, line 3305

0:Break, Ignore, Terminate Process or Terminate Thread (bipt)? b
0:Execute '!cxr BD94B918' to dump context
Break instruction exception - code 80000003 (first chance)
ntkrnlmp!DbgBreakPoint:
804a3ce4 cc               int     3
```

ユーザーが「中断、無視、終了プロセスまたはスレッドの終了」によく寄せられる、デバッガーの出力に示すように、 デバッガーがブレークポイントが設定されたシステムの実行を停止の原因となった"b"を入力して回答があったユーザー。 結果として、ユーザーでは、検出された問題をデバッグを継続できますようになりました。

失敗したアサートがシステムに影響する方法は、さまざまな要因によって異なります。 Windows Vista より前の Windows のバージョンでは、オペレーティング システムのシステムの起動処理中のデバッグが有効な場合、システムを (接続されている) 場合、デバッガーを中断またはデバッガーに接続するを待つのハングします。 システムがクラッシュし、デバッグが有効でない場合[**バグ チェック 0x1E** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x1e--kmode-exception-not-handled) (KMODE\_例外\_いない\_処理済み) 0x80000003 のパラメーター 1 の値。 Windows Vista 以降では、システムは、デバッガーが接続されている場合にのみ、デバッガーが中断されます。 デバッグが有効でない場合、またはデバッグが有効になっているが、デバッガーが接続されていない場合は、失敗したアサーションは (ただし、アサーションによるチェックは実行されます) に報告されません。 ドライバーを開発し、確定的にデバッグが有効な場合にデバッガーにブレークするようには、デバッガーが接続されていない、使用することができますが、場合[ **DbgBreakPoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgbreakpoint)ステートメントをコードにします。

いくつか[ **ASSERT** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))エラーの追加前[**による DbgPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprint)出力します。 この種類の assert の 1 つの一般的な例は、次[**ページ\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロ、ntddk.h とドライバーのチェック ビルドで使用するための wdm.h で定義されています。

```
#define PAGED_CODE() \
    if (KeGetCurrentIrql() > APC_LEVEL) { \
KdPrint(( "EX: Pageable code called at IRQL %d\n", KeGetCurrentIrql() )); \
        ASSERT(FALSE); \
        }
```

このマクロは、適切な Irql でのみページング可能な関数が呼び出されることを確認するオペレーティング システム内でよく使用されます。

通常、失敗した場合、テキストを調べることができます、ドライバーのアクションのアサートが発生したときに呼び出された機能を含むアサーション エラーの原因を特定するための式のコードします。 **KB (スタック トレースの表示)** デバッガー コマンドがこの分析に重要です。

最も一般的なアサート呼び出しの一覧は、次を参照してください。[チェック ビルド アサート](checked-build-asserts.md)します。

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>ブレークポイント

チェック ビルドはブレークポイントを使用しても問題があります。 ブレークポイントは多くの場合、続く[**による DbgPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprint)ステートメントで、デバッガーが発生した問題に関する情報を表示します。 ブレークポイントが発生した場合、デバッガーでは、システムに接続されていない、システムがクラッシュし、説明のすべてのメッセージは失われます。

一部のチェックのビルドでのブレークポイントの前にして、ドライバーの作成者によってこれが発生した最も一般的なメッセージが記載されて[ビルド ブレークポイントのチェックとメッセージ](checked-build-breakpoints-and-messages.md)します。

次の例はどのように、**による DbgPrint**デバッガーに呼び出し、ブレークポイントが表示されます。

```
*** DPC routine > 1 sec --- This is not a break in KeUpdateSystemTime
Break instruction exception - code 80000003 (first chance)
NTOSKRNL!DbgBreakPoint:
804a3ce4 cc               int     3
```

この例は、1 つの遅延プロシージャ呼び出し (DPC) を示すメッセージが 1 秒より長く実行されているとチェック ビルドで実装されるチェックの種類を示しています。 デバッガーを示します。 このブレークポイントは、ドライバーがドライバーの重大な問題を示している可能性があります DPC ルーチンで時間を費やしたことを意味します。 その一方で、このブレークポイントはできるドライバーが必要な実行の DPC 時間の長さの拡張によって実現、DPC ルーチンで大量のデバッグ出力を生成する場合にも発生します。 問題の根本原因を検出するには、DPC ルーチンでを行うことを通知し、1 ~ 2 回、ブレークポイント以降を続行を確認します。

まれな状況では、ブレークポイントが、メッセージが表示されないことが重要です、カーネル スタック トレースを確認する (を使用して、 **KB**デバッガー コマンド) をブレークポイントが発生しました。 多くの場合、これのブレークポイントを理由に、強力な手掛かりが付与されます。

次の例は、スタック トレースと共に、多くの Windows ドライバー開発者は、発生する一般的なブレークポイントを示しています。

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

ブレークポイントが、呼び出しの結果として作成されたこのスタック トレースからわかる、 **KfAcquireSpinLock**します。 Wdm.h を調べると確認できますとしてドライバーによって参照される関数の実際の名前である[ **KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)します。 ブレークポイントの前にメッセージが表示されない、場合でも、スタックの一番上にあるブレークポイントの場所を確認できます (**ntkrnlmp!SpinLockSpinningForTooLong**)。 この場所は、ブレークポイントの理由を示します。保留中の異常に長いのため、取得、スピン ロックを回転されているがします。

### <a name="span-iddebuggermessagesspanspan-iddebuggermessagesspandebugger-messages"></a><span id="debugger_messages"></span><span id="DEBUGGER_MESSAGES"></span>デバッガーのメッセージ

チェック ビルドは特定するため、デバッガーのメッセージを使用したり、発生したエラーに関する追加情報を提供できます。 デバッガーのメッセージの最も一般的なソースは、ユーザー モードのプログラムのチェック (デバッグ) から、または非カーネルと HAL 以外のコンポーネントから発生するエラーです。 出力の量は、各オペレーティング システムのリリースによって異なります。

次の例では、完全なチェック ビルドのインストールによって表示される出力を示します。 この出力は、Windows XP では、プレリリース版によって生成された、完全チェック ビルドに通常表示されるよりもさらに膨大なは。

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

いくつかのチェック ビルドは、ドライバーのデバッグ中に表示できる最も一般的なメッセージが記載されて[ビルド ブレークポイントのチェックとメッセージ](checked-build-breakpoints-and-messages.md)します。

別のトレースまたは情報メッセージをさまざまなシステム コンポーネントを有効にすると、後続のブレークポイントまたはアサート失敗せずデバッガー メッセージこともあります。

 

 






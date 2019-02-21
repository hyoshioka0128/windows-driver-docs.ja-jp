---
title: バグ チェック時にドライバー検証機能を処理が有効になっています。
description: Driver Verifier は、実行時にドライバー関連のエラーを検出します。 検出され、ドライバー エラーに関する情報を表示、分析のデバッガー コマンドと共に Driver Verifier を使用できます。
ms.assetid: 4226B62B-0AA5-4D04-A32D-7DD22FD694E3
keywords:
- ドライバーの検証ツール
- 検証方法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a835eb71d0a959575ae04a7f55970b02d68a89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529600"
---
# <a name="handling-a-bug-check-when-driver-verifier-is-enabled"></a>バグ チェック時にドライバー検証機能を処理が有効になっています。


[Driver Verifier](https://go.microsoft.com/fwlink/p?LinkID=268663)実行時にドライバー関連のエラーを検出します。 Driver Verifier と共に使用することができます、 [ **! 分析**](-analyze.md)デバッガー コマンドが検出され、ドライバー エラーに関する情報を表示します。

Windows 8 で[Driver Verifier](https://go.microsoft.com/fwlink/p?LinkID=268663)などの新しい機能が強化されました[DDI 準拠の検査](https://go.microsoft.com/fwlink/p?LinkID=268676)します。 ここで DDI 準拠の確認を示す例を紹介しました。

設定するには、次の手順を使用します。

1.  ホストおよびターゲット コンピューターの間でカーネル モードのデバッグ セッションを確立します。
2.  ターゲット コンピューターに、ドライバーをインストールします。
3.  ターゲット コンピューターでは、コマンド プロンプト ウィンドウを開き、コマンドを入力して**verifier**します。 使用[ドライバー検証マネージャー](https://go.microsoft.com/fwlink/p?LinkID=268659)ドライバーをドライバーの検証を有効にします。
4.  ターゲット コンピューターを再起動します。

Driver Verifier は、エラーを検出すると、バグ チェックが生成されます。 Windows では、デバッガーを中断し、エラーの簡単な説明を表示します。 Driver Verifier がバグの確認を生成する例をここでは[**ドライバー\_VERIFIER\_検出\_違反 (C4)**](bug-check-0xc4--driver-verifier-detected-violation.md)します。

```dbgcmd
Driver Verifier: Extension abort with Error Code 0x20005
Error String ExAcquireFastMutex should only be called at IRQL <= APC_LEVEL.

*** Fatal System Error: 0x000000c4
                       (0x0000000000020005,0xFFFFF88000E16F50,0x0000000000000000,0x0000000000000000)

Break instruction exception - code 80000003 (first chance)

A fatal system error has occurred.
Debugger entered on first try; Bugcheck callbacks have not been invoked.

A fatal system error has occurred.

nt!DbgBreakPointWithStatus:
fffff802`a40ef930 cc              int     3
```

デバッガーで、次のように入力します。 [ **。-v を分析**](-analyze.md)エラーの詳細な説明を取得します。

```dbgcmd
0: kd> !analyze -v
Connected to Windows 8 9200 x64 target at (Thu Oct 11 13:48:31.270 2012 (UTC - 7:00)), ptr64 TRUE
Loading Kernel Symbols
...............................................................
................................................................
...................
Loading User Symbols
..................................................
Loading unloaded module list
............
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 0000000000020005, ID of the 'IrqlExApcLte1' rule that was violated.
Arg2: fffff88000e16f50, A pointer to the string describing the violated rule condition.
Arg3: 0000000000000000, An optional pointer to the rule state variable(s).
Arg4: 0000000000000000, Reserved (unused)

## Debugging Details:

...

DV_VIOLATED_CONDITION:  ExAcquireFastMutex should only be called at IRQL <= APC_LEVEL.

DV_MSDN_LINK: !url https://go.microsoft.com/fwlink/p/?linkid=216022

DV_RULE_INFO: !ruleinfo 0x20005

BUGCHECK_STR:  0xc4_IrqlExApcLte1_XDV

DEFAULT_BUCKET_ID:  WIN8_DRIVER_FAULT

PROCESS_NAME:  TiWorker.exe

CURRENT_IRQL:  9
```

上記の出力で、ルールの説明と名前を表示できます**IrqlExApcLte1**に違反していた、およびルールを説明するリファレンス ページへのリンクをクリックすることができます:<https://go.microsoft.com/fwlink/p/?linkid=216022>します。 デバッガー コマンド リンクをクリックすることもできます。 **! ruleinfo 0x20005**、ルールに関する情報を取得します。 この場合、ルールの状態を呼び出すことができません[ExAcquireFastMutex](https://go.microsoft.com/fwlink/p?LinkID=268628)割り込み要求レベル (IRQL) が APC より大きいかどうか\_レベル。 出力は、現在の IRQL は 9、および wdm.h で確認できますを示しています。 その APC\_レベルが 1 の値を持ちます。 Irql の詳細については、次を参照してください。[を管理するハードウェアの優先順位](https://go.microsoft.com/fwlink/p?LinkID=268625)します。

出力[ **! 分析-v** ](-analyze.md)はスタック トレースとエラーの原因となったコードに関する情報を使って続行されます。 次の出力を表示できます、 **OnInterrupt**と呼ばれる MyDriver.sys で日常的な[ExAcquireFastMutex](https://go.microsoft.com/fwlink/p?LinkID=268628)します。 **OnInterrupt** APC より大きい IRQL で実行される割り込みサービス ルーチンは、\_レベルに、このルーチンを呼び出すの違反が発生するように[ExAcquireFastMutex](https://go.microsoft.com/fwlink/p?LinkID=268628)します。

```dbgcmd
LAST_CONTROL_TRANSFER:  from fffff802a41f00ea to fffff802a40ef930

STACK_TEXT:  
... : nt!DbgBreakPointWithStatus ...
... : nt!KiBugCheckDebugBreak+0x12 ...
... : nt!KeBugCheck2+0x79f ...
... : nt!KeBugCheckEx+0x104 ...
... : VerifierExt!SLIC_abort+0x47 ...
... : VerifierExt!SLIC_ExAcquireFastMutex_entry_irqlexapclte1+0x25 ...
... : VerifierExt!ExAcquireFastMutex_wrapper+0x1a ...
... : nt!ViExAcquireFastMutexCommon+0x1d ...
... : nt!VerifierExAcquireFastMutex+0x1a ...
... : MyDriver!OnInterrupt+0x69 ...
... : nt!KiScanInterruptObjectList+0x6f ...
... : nt!KiChainedDispatch+0x19a ...
...

STACK_COMMAND:  kb

FOLLOWUP_IP: 
MyDriver!OnInterrupt+69 ...
fffff880`16306649 4c8d0510040000  lea     r8,[MyDriver! ?? ::FNODOBFM::`string' (fffff880`16306a60)]

FAULTING_SOURCE_LINE:  c:\MyDriverwdm03\cpp\MyDriver\pnp.c

FAULTING_SOURCE_FILE:  c:\MyDriverwdm03\cpp\MyDriver\pnp.c

FAULTING_SOURCE_LINE_NUMBER:  26

FAULTING_SOURCE_CODE:  
    22:    if(1 == interruptStatus)
    23:    {
    24:       ...
    25:       ExAcquireFastMutex( &(fdoExt->fastMutex) );
>   26:       ...
    27:       ExReleaseFastMutex( &(fdoExt->fastMutex) );
    28:       ...
    29:       return TRUE;
    30:    }
    31:    else


SYMBOL_STACK_INDEX:  9

SYMBOL_NAME:  MyDriver!OnInterrupt+69

FOLLOWUP_NAME:  ...

MODULE_NAME: MyDriver

IMAGE_NAME:  MyDriver.sys

DEBUG_FLR_IMAGE_TIMESTAMP:  50772f37

BUCKET_ID_FUNC_OFFSET:  69

FAILURE_BUCKET_ID:  0xc4_IrqlExApcLte1_XDV_VRF_MyDriver!OnInterrupt

BUCKET_ID:  0xc4_IrqlExApcLte1_XDV_VRF_MyDriver!OnInterrupt
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Static Driver Verifier](https://go.microsoft.com/fwlink/p?LinkID=268668)

 

 







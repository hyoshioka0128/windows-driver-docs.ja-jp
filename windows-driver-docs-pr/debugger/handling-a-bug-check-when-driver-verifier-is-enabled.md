---
title: ドライバーの検証ツールが有効な場合のバグ チェックの処理
description: ドライバーの検証ツールは、実行時にドライバーのエラーを検出します。 ドライバーの検証ツールと [デバッガーの分析] コマンドを使用すると、ドライバーのエラーに関する情報を検出して表示できます。
ms.assetid: 4226B62B-0AA5-4D04-A32D-7DD22FD694E3
keywords:
- ドライバーの検証ツール
- 検証方法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49951abcbd074a30aa1b492fc2aed30b8d8eab4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534353"
---
# <a name="handling-a-bug-check-when-driver-verifier-is-enabled"></a>ドライバーの検証ツールが有効な場合のバグ チェックの処理


[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)は、実行時にドライバーのエラーを検出します。 Driver Verifier と[**! analyze**](-analyze.md)デバッガーコマンドを使用すると、ドライバーのエラーに関する情報を検出して表示できます。

Windows 8 では、[ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)機能が、DDI の[コンプライアンスチェック](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)を含む新機能によって強化されています。 ここでは、DDI のコンプライアンスチェックの例を示します。

セットアップを行うには、次の手順に従います。

1.  ホストとターゲットコンピューターの間でカーネルモードのデバッグセッションを確立します。
2.  ターゲットコンピューターにドライバーをインストールします。
3.  ターゲットコンピューターでコマンドプロンプトウィンドウを開き、コマンド**検証ツール**を入力します。 ドライバー[検証マネージャー](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier-manager--windows-xp-and-later-)を使用して、ドライバーのドライバーの検証を有効にします。
4.  ターゲット コンピューターを再起動します。

ドライバーの検証ツールでエラーが検出されると、バグチェックが生成されます。 その後、Windows がデバッガーに分割され、エラーの簡単な説明が表示されます。 次に示すのは、ドライバーの検証ツールがバグチェック[**ドライバーの \_ 検証ツールの \_ 検出 \_ 違反 (C4)**](bug-check-0xc4--driver-verifier-detected-violation.md)を生成する例です。

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

デバッガーで、「 [**! analyze-v**](-analyze.md) 」と入力して、エラーの詳細な説明を取得します。

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

上記の出力には、規則の名前と説明 ( **IrqlExApcLte1**) が表示されます。また、規則について説明している参照ページへのリンクをクリックすることもできます。 <https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexapclte1> また、デバッガーのコマンドリンク [ **! ruleinfo 0x20005**] をクリックして、ルールに関する情報を取得することもできます。 この場合、割り込み要求レベル (IRQL) が APC レベルを超えると、 [ExAcquireFastMutex](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))を呼び出すことができないことがルールによって示され \_ ます。 出力は、現在の IRQL が9であることを示しています。また、wdm では、APC \_ レベルの値が1であることがわかります。 IRQLs の詳細については、「[ハードウェアの優先順位の管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)」を参照してください。

[**! Analyze-v**](-analyze.md)の出力は、スタックトレースと、エラーの原因となったコードに関する情報を使用して続行されます。 次の出力では、MyDriver. sys の**Oninterrupt**ルーチンが[ExAcquireFastMutex](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))という名前であることがわかります。 **Oninterrupt**は、APC レベルよりも大きい IRQL で実行される割り込みサービスルーチンです \_ 。そのため、このルーチンで[ExAcquireFastMutex](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))を呼び出すと、違反となります。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)

 

 







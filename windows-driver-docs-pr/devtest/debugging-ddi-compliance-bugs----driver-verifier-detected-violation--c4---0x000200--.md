---
title: デバッグ (C4) DRIVER_VERIFIER_DETECTED_VIOLATION 0x20002 - 0x20022
description: DDI 準拠の検査、選択したオプションがあるし、Driver Verifier DDI 準拠の規則のいずれかに違反するドライバー、Driver Verifier 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION のバグの確認を生成することを検出したときに (パラメーター 1 と等しく、ルールの識別子、特定の対応)。
ms.assetid: 9817AC4B-2BE8-44AC-8C9B-DED5EF0A7DD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca4dfeb4728968de0c7e2773afd6a53dbecbb15b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531512"
---
# <a name="debugging-ddi-compliance-bugs---driververifierdetectedviolation-c4-0x20002---0x20022"></a>DDI 準拠のバグのドライバーをデバッグ\_VERIFIER\_検出\_違反 (C4)。0x20002 - 0x20022


ある場合、 [DDI 準拠の検査](ddi-compliance-checking.md)オプションを選択し、Driver Verifier は、ドライバーが違反 DDI 準拠規則のいずれかを検出[Driver Verifier](driver-verifier.md)生成[ **バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (パラメーター 1 で特定のコンプライアンス規則の識別子に等しい)。

DDI 準拠規則では、ドライバーは、Windows オペレーティング システムのカーネルと正しく対話することを確認します。 たとえば、ルールには、ドライバーが、関数の適切な IRQL で関数呼び出しを行うこと、またはドライバーが正しく取得し、スピン ロックを解放することを確認します。 このセクションでは、これらの違反をデバッグするため、いくつかの戦略の例について説明します。

## <a name="debugging-ddi-compliance-checking-violations"></a>DDI 準拠のチェック違反をデバッグします。


-   [使用してバグ チェックに関する情報を表示するために分析。](#use-analyze-to-display-information-about-the-bug-check)
-   [使用して、! ruleinfo 拡張コマンド](#use-the-ruleinfo-extension-command)
-   [使用して、!、違反のソース コードの場所を識別するために、– v コマンドの分析](#use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code)
-   [DDI 準拠の違反の原因を修正](#fixing-the-cause-of-the-ddi-compliance-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用してバグ チェックに関する情報を表示するために分析。

デバッガーの制御をした後に発生するすべてのバグ チェックと同様、最適な最初の手順が実行するが、 [ **! 分析-v** ](https://msdn.microsoft.com/library/windows/hardware/ff562112)コマンド。

```
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
Arg1: 00020004, ID of the 'IrqlExAllocatePool' rule that was violated.
Arg2: 8481c118, A pointer to the string describing the violated rule condition.
Arg3: 00000000, Reserved (unused).
Arg4: 00000000, Reserved (unused).

## Debugging Details:


DV_VIOLATED_CONDITION:  ExAllocatePoolWithTagPriority should only be called at IRQL <= DISPATCH_LEVEL.

DV_MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=216021

DV_RULE_INFO: 0x20004
```

たびに[Driver Verifier](driver-verifier.md)キャッチ、 [DDI 準拠の検査](ddi-compliance-checking.md)違反、違反に関する情報が記載された、 [ **! 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)出力します。

この例で[ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)パラメーター 1 (Arg1) の 0x20004、ドライバーが違反したことを示す値、 [ **IrqlExAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff547747)コンプライアンス規則。

[ **! 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)出力には、次の情報が含まれています。

**DV\_VIOLATED\_条件。** このフィールドは、規則違反の原因の説明を示します。 この例で、条件に違反しましたを非常に高い IRQL レベルでのメモリを割り当てようとしたドライバーまたはディスパッチでページ プール メモリを割り当てられたしようとしています。\_レベル。 たとえば、このされた可能性がある呼び出しを試みるがドライバー [ **ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)割り込みサービス ルーチン (ISR)、またはページ プール メモリを割り当てようとしたドライバー中に、スピン ロックを保持します。

**DV\_MSDN\_LINK:** についての詳細を示す、MSDN のページを開きます、デバッガーがライブ リンク、WinDBG では、 [ **IrqlExAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff547747)ルール。

**DV\_ルール\_情報。**、WinDBG では、このルール使用可能なヘルプからについては、デバッガーで表示されるライブ リンクです。

### <a name="use-the-ruleinfo-extension-command"></a>使用して、! ruleinfo 拡張コマンド

**DV\_ルール\_情報:** のフィールド、 **! 分析**出力は、この規則違反に関する詳細情報を使用できるコマンドを示しています。 この例では、コマンドを使用することができます: **! ruleinfo 0x20004**

```
kd> !ruleinfo 0x20004

RULE_ID: 0x20004

RULE_NAME: IrqlExAllocatePool

RULE_DESCRIPTION:
The IrqlExAllocatePool rule specifies that the driver calls:
ExAllocatePool,
ExAllocatePoolWithTag,
ExAllocatePoolWithQuota,
ExAllocatePoolWithQuotaTag and
ExAllocatePoolWithTagPriority
only when it is executing at IRQL <= DISPATCH_LEVEL. A caller
executing at DISPATCH_LEVEL must specify a NonPagedXxx value
for PoolType. A caller executing at IRQL <= APC_LEVEL can
specify any POOL_TYPE value.

MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=216021
```

### <a name="use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code"></a>使用して、!、違反のソース コードの場所を識別するために分析 – v コマンド

Driver Verifier のバグはこの違反が検出されるとすぐに、システムを確認します。 **! 分析**出力が表示されます、現在の IRQL、現在のスタック メモリを割り当て、呼び出しが行われたとのソース コードが有効にした場合のポイント、 **! 分析 – v** (の詳細な) 出力は、ソースも表示されます割り当て要求が行われたファイルと行の数:

```
CURRENT_IRQL:  10

ANALYSIS_VERSION: 6.13.0016.1929 (debuggers(dbg).130725-1857) amd64fre

LAST_CONTROL_TRANSFER:  from 80ff159d to 80f751f4

STACK_TEXT:  
82f9eaa4 81dda59d 00000003 86fab4b0 00000065 nt!RtlpBreakWithStatusInstruction
82f9eaf8 81dda0b7 82fa0138 82f9eef8 82f9ef40 nt!KiBugCheckDebugBreak+0x1f
82f9eecc 81d5cdc6 000000c4 00020004 85435118 nt!KeBugCheck2+0x676
82f9eef0 81d5ccfd 000000c4 00020004 85435118 nt!KiBugCheck2+0xc6
82f9ef10 8542cb4e 000000c4 00020004 85435118 nt!KeBugCheckEx+0x19
82f9ef30 85425ded ffffffff 85425e0d 82f9ef60 VerifierExt!SLIC_abort+0x40
82f9ef38 85425e0d 82f9ef60 8210c19e 00000080 VerifierExt!SLIC_ExAllocatePoolWithTagPriority_internal_entry_IrqlExAllocatePool+0x6f
82f9ef40 8210c19e 00000080 00000000 00000000 VerifierExt!ExAllocatePoolWithTagPriority_internal_wrapper+0x19
82f9ef60 826c9e16 00000000 00000000 00000000 nt!VerifierExAllocatePoolWithTag+0x24
82f9efa8 81d0726c 833cba80 8a4b9480 00000000 MyDriver!HandleISR+0x146
82f9efbc 81d071c1 833cba80 8a4b9480 000000b8 nt!KiInterruptMessageDispatch+0x12
82f9efe4 81d71f29 00000001 525b61ea 00000224 nt!KiCallInterruptServiceRoutine+0x6d
82f9efe8 00000000 525b61ea 00000224 00000000 nt!KiInterruptDispatch+0x49

STACK_COMMAND:  kb

FOLLOWUP_IP: 
MyDriver!HandleISR+0x140
826c9e10 ff154440699b    call    dword ptr [IrqlExAllocatePool_ExAllocatePoolWithTag!_imp__ExAllocatePoolWithTag (9b694044)]

FAULTING_SOURCE_LINE:  d:\drvsrc\mydriver\isrhandler.c

FAULTING_SOURCE_FILE:  d:\drvsrc\mydriver\isrhandler.c

FAULTING_SOURCE_LINE_NUMBER:  206
```

### <a name="fixing-the-cause-of-the-ddi-compliance-violation"></a>DDI 準拠の違反の原因を修正

ドライバーが、対応するドキュメントで説明されている API と DDI 使用条件を満たしていることを確認は、一般に範囲 0x00020000 に 0x00020022 に Arg1 値を持つこれらのバグ チェックを修正して、します。

ISR でどのような種類のメモリ割り当てが設定 IRQL 規則に違反しようとしたここで使用した (0x20004) の例で、 [ **ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)ルーチン。

一般に、IRQL と適切な使用方法については、ルーチンに関するドキュメントを確認する必要があります。 特定のレビュー [DDI 準拠規則](https://msdn.microsoft.com/library/windows/hardware/ff552840)関数をテストします。 ルールは、この場合、 [ **IrqlExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff547747)します。

使用[Static Driver Verifier](static-driver-verifier.md)同じ規則を使用して、ドライバー ソース コードを分析します。 Static Driver Verifier は、Windows ドライバーのソース コードをスキャンし、さまざまなコード パスの実行をシミュレートすることで考えられる問題を報告するツールです。 Static Driver Verifier は、このような問題を識別するための優れた開発時ユーティリティです。

## <a name="related-topics"></a>関連トピック


[DDI 準拠の確認](ddi-compliance-checking.md)

[DDI 準拠の規則](https://msdn.microsoft.com/library/windows/hardware/ff552840)

[Static Driver Verifier](static-driver-verifier.md)

[**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)

 

 







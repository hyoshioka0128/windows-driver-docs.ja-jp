---
title: デバッグ DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x20002-0x20022
description: '[DDI 準拠の確認] オプションを選択した場合、ドライバーの検証ツールによって、いずれかの DDI コンプライアンス規則に違反していることが検出されると、ドライバーの検証ツールによってバグチェック 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION が生成されます (パラメーター1は特定のコンプライアンス規則の識別子。'
ms.assetid: 9817AC4B-2BE8-44AC-8C9B-DED5EF0A7DD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8f7bc380af1b3dc71e157a8e40c447e8d82310
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839571"
---
# <a name="debugging-ddi-compliance-bugs---driver_verifier_detected_violation-c4-0x20002---0x20022"></a>DDI 準拠のバグのデバッグ-DRIVER\_VERIFIER\_検出された\_違反 (C4): 0x20002-0x20022


[ [Ddi 準拠チェック](ddi-compliance-checking.md)] オプションを選択した場合、ドライバーの検証ツールによって、いずれかの ddi コンプライアンス規則に違反していることが検出されると、[ドライバーの検証ツール](driver-verifier.md)は[**バグチェック 0XC4: ドライバー\_検証\_検出されました\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(パラメーター1が特定のコンプライアンス規則の識別子と等しい)。

DDI コンプライアンス規則は、ドライバーが Windows オペレーティングシステムのカーネルと正しく通信するようにします。 たとえば、ルールによって、ドライバーが関数に対して必要な IRQL で関数呼び出しを行うかどうか、またはドライバーがスピンロックを正しく取得して解放することが確認されます。 ここでは、これらの違反をデバッグするための方法の例について説明します。

## <a name="debugging-ddi-compliance-checking-violations"></a>DDI 準拠チェックの違反のデバッグ


-   [! Analyze を使用して、バグチェックに関する情報を表示します](#use-analyze-to-display-information-about-the-bug-check)
-   [! Ruleinfo extension コマンドを使用します。](#use-the-ruleinfo-extension-command)
-   [! Analyze – v コマンドを使用して、ソースコード内の違反の場所を特定します。](#use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code)
-   [DDI 準拠違反の原因を修正する](#fixing-the-cause-of-the-ddi-compliance-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>! Analyze を使用して、バグチェックに関する情報を表示します

バグチェックが発生した場合と同様に、デバッガーを制御したら、最初に[ **! analyze-v**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)コマンドを実行します。

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

[Driver Verifier](driver-verifier.md)が DDI の[準拠チェック](ddi-compliance-checking.md)の違反をキャッチするたびに、 [ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)出力に違反に関する情報が提供されます。

この例では、[**バグチェック 0xC4: driver\_VERIFIER\_検出されました。\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)には、パラメーター 1 (Arg1) の値0x20004 が含まれています。これは、ドライバーが[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)のコンプライアンス規則に違反したことを示します。

[ **! Analyze**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)出力には、次の情報が含まれています。

**DV\_\_条件に違反**しました:このフィールドには、ルール違反の原因の説明が表示されます。 この例では、ドライバーが非常に高い IRQL レベルでメモリを割り当てようとしたか、またはディスパッチ\_レベルでページプールメモリを割り当てようとしたため、条件に違反しました。 たとえば、割り込みサービスルーチン (ISR) で[**Exallocatepoolwithtagpriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)を呼び出そうとしたドライバー、またはスピンロックを保持しながらページプールメモリを割り当てようとしたドライバーがある可能性があります。

**DV\_MSDN\_リンク:** WinDBG では、これはライブリンクです。これにより、デバッガーは[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)規則に関する詳細情報を示す MSDN ページを開きます。

**DV\_ルールの\_情報:** WinDBG では、これは、デバッガーで利用できるヘルプからこの規則に関する情報を表示するライブリンクです。

### <a name="use-the-ruleinfo-extension-command"></a>! Ruleinfo extension コマンドを使用します。

**! Analyze**出力の**DV\_RULE\_INFO:** フィールドは、この規則違反に関する詳細情報を検索するために使用できるコマンドを示しています。 この例では、 **! ruleinfo 0x20004**コマンドを使用できます。

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

### <a name="use-the-analyze-v-command-to-identify-the-location-of-the-violation-in-source-code"></a>! Analyze-v コマンドを使用して、ソースコード内の違反の場所を特定します。

この違反が検出されると、ドライバーの検証ツールによってシステムが即座にチェックされます。 **! Analyze**出力には、現在の IRQL、現在のスタック、メモリを割り当てるための呼び出しが行われたポイントが表示されます。また、ソースコードが **! analyze – v** (詳細) 出力を有効にした場合は、割り当てのソースファイルと行番号も表示されます。要求が行われました:

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

### <a name="fixing-the-cause-of-the-ddi-compliance-violation"></a>DDI 準拠違反の原因を修正する

これらのバグチェックを修正すると、範囲が0x00020000 から0x00020022 になります。一般に、ドライバーが、対応するドキュメントに記載されている API と DDI の使用状況の条件を満たしていることを確認します。

ここで使用した例 (0x20004) では、ISR における任意の並べ替えのメモリ割り当ては、 [**Exallocatepoolwithtagpriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)ルーチンに設定されている IRQL 規則に違反します。

一般に、IRQL と適切な使用法に関する情報については、ルーチンに関するドキュメントを参照してください。 関数をテストする特定の[DDI コンプライアンス規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を確認します。 この場合、ルールは[**IrqlExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlexallocatepool)です。

同じルールを使用して、ドライバーのソースコードを分析するには、[静的なドライバーの検証ツール](static-driver-verifier.md)を使用します。 静的ドライバー検証ツールは、Windows ドライバーのソースコードをスキャンし、さまざまなコードパスの使用をシミュレートすることによって発生する可能性のある問題を報告するツールです。 静的ドライバー検証ツールは、これらの種類の問題を特定するのに役立つ優れた開発時ユーティリティです。

## <a name="related-topics"></a>関連トピック


[DDI のコンプライアンスチェック](ddi-compliance-checking.md)

[DDI コンプライアンス規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[静的ドライバー検証ツール](static-driver-verifier.md)

[**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)

 

 







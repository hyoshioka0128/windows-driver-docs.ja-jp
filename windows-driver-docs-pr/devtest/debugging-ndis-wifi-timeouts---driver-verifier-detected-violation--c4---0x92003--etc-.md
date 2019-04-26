---
title: デバッグ DRIVER_VERIFIER_DETECTED_VIOLATION (C4)
description: Driver Verifier は、ドライバーには、NDIS/WiFi のタイムアウト ルールのいずれかに違反を検出します。
ms.assetid: 73D4B6DF-E667-4C71-B985-FCDC05837908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 556d04d6c369ab9c5efb8600eac68345845463a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344866"
---
# <a name="debugging-ndiswifi-time-out-errors---driververifierdetectedviolation-c4"></a>ドライバーの NDIS/WiFi タイムアウト エラーをデバッグ\_VERIFIER\_検出\_違反 (C4)


ある場合、 [NDIS/WIFI 検証](ndis-wifi-verification.md)オプションを選択し、Driver Verifier のドライバーには、NDIS/WiFi のタイムアウト ルールのいずれかに違反が検出された[Driver Verifier](driver-verifier.md)生成[ **バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (パラメーター 1 で、特定の NDIS/WiFi タイムアウト ルールの識別子に等しい)。

Driver Verifier は、テスト場合 NDIS/WIFI のタイムアウト ルールなど[ **NdisTimedOidComplete**](https://msdn.microsoft.com/library/windows/hardware/dn305120)、Driver Verifier のポーリング メカニズムは、サイクル数内で、ミニポート ドライバーからの応答が必要です。 各時間指定のルールには、許可されている独自の最大のサイクルが定義します。 最大値を超えると、Driver Verifier のバグ チェックが生成されます。 このセクションでは、これらの違反をデバッグするため、いくつかの戦略の例について説明します。

## <a name="debugging-ndiswifi-timeout-errors"></a>NDIS/WIFI タイムアウト エラーのデバッグ


-   [使用してバグ チェックに関する情報を表示するために分析。](#use-analyze-to-display-information-about-the-bug-check)
-   [使用して、! ruleinfo 拡張コマンド](#use-the-ruleinfo-extension-command)
-   [最後のクリックして\_呼び出す\_違反の場所を識別するためにスタックのリンク](#identify-the-location-of-the-violation)
-   [NDIS/WIFI タイムアウト違反の原因を修正](#fixing-the-cause-of-the-ndis-wifi-timeout-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用してバグ チェックに関する情報を表示するために分析。

デバッガーの制御をした後に発生するすべてのバグ チェックと同様、最適な最初の手順が実行するが、 [ **! 分析-v** ](https://msdn.microsoft.com/library/windows/hardware/ff562112)コマンド。

```
DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 00092003, ID of the 'NdisTimedOidComplete' rule that was violated.
Arg2: 8521dd34, A pointer to the string describing the violated rule condition.
Arg3: 9c17b860, Address of internal rule state (second argument to !ruleinfo).
Arg4: 9c1f3480, Address of supplemental states (third argument to !ruleinfo).
```

次のセクションで、 **! 分析-v** 、出力で、ルールに違反していた理由理由下に表示されます、DV\_VIOLATED\_条件フィールド。 DV\_MSDN\_リンク セクションもこのルールは、ドキュメントをリンクをプルする便利です。

```
## Debugging Details:


*** ERROR: Module load completed but symbols could not be loaded for NdisTimedOidComplete.sys

DV_VIOLATED_CONDITION:  Timeout on completing an NDIS OID request.

DV_MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278804

DRIVER_OBJECT: 98a87980

IMAGE_NAME:  NdisTimedOidComplete.sys

DEBUG_FLR_IMAGE_TIMESTAMP:  5229c857

MODULE_NAME: NdisTimedOidComplete

FAULTING_MODULE: 9fee1000 NdisTimedOidComplete
```

さらにこの分析出力ダウンできますリンクをクリックする、DV \_ルール\_情報セクションの他の規則の説明。 規則のタイムアウトの種類、現在のスタックには関連する情報は含まれません可能性があります。

```
DV_RULE_INFO: 0x92003

BUGCHECK_STR:  0xc4_NdisTimedOidComplete_XDV

DEFAULT_BUCKET_ID:  WIN8_DRIVER_FAULT

PROCESS_NAME:  System

CURRENT_IRQL:  2

ANALYSIS_VERSION: 6.13.0016.1929 (debuggers(dbg).130725-1857) amd64fre

LAST_CONTROL_TRANSFER:  from 80f87fd3 to 80f0ed14

STACK_TEXT:  
8912380c 80f87fd3 00000003 e6c3476e 00000065 nt!RtlpBreakWithStatusInstruction
89123860 80f87aed 825a6138 89123c5c 89123cac nt!KiBugCheckDebugBreak+0x1f
89123c30 80f0d8d6 000000c4 00092003 8521dd34 nt!KeBugCheck2+0x676
89123c54 80f0d80d 000000c4 00092003 8521dd34 nt!KiBugCheck2+0xc6
89123c74 85211584 000000c4 00092003 8521dd34 nt!KeBugCheckEx+0x19
89123cac 85216d54 9c17b860 9c1f3480 9c17b8dc VerifierExt!SLIC_StatefulAbort+0x1a4
89123cd0 85216ffe 85220000 85215f5b 00000000 VerifierExt!Ndis_OnTimerExpire+0x234
89123cd8 85215f5b 00000000 80ecd56a 843d0c38 VerifierExt!CheckOnTimerExpire+0x26
89123ce0 80ecd56a 843d0c38 00000000 80ecd502 VerifierExt!XdvPassiveTimerRoutine+0x1d
89123d24 80eec133 882befd0 00000000 887debc0 nt!IopProcessWorkItem+0x68
89123d70 80ec1162 00000000 e6c342be 00000000 nt!ExpWorkerThread+0x14f
89123db0 80f23201 80eebfe4 00000000 00000000 nt!PspSystemThreadStartup+0x58
89123dbc 00000000 00000000 00000000 00000000 nt!KiThreadStartup+0x15
```

### <a name="use-the-ruleinfo-extension-command"></a>使用して、! ruleinfo 拡張コマンド

**DV\_ルール\_情報:** のフィールド、 **! 分析**出力は、この規則違反に関する詳細情報を使用できるコマンドへのリンクを示しています。 この例で、リンクをクリックした場合、実行、 [ **! ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)コマンド ルールと\_ID (0x92003)、Arg3 と Arg 4 バグは、値を確認します。

```
kd> !ruleinfo 0x92003 0xffffffff9c17b860 0xffffffff9c1f3480

RULE_ID: 0x92003

RULE_NAME: NdisTimedOidComplete

RULE_DESCRIPTION:
This rule verifies if an NDIS miniport driver completes an OID in time.
The OID is tracked (a.k.a., TRACKED_OBJECT). Use !ndiskd.oid .

MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278804

CONTEXT: Miniport 0x86BD10E8

CURRENT_TIME (Timed Rules): 168 seconds

TRACKED_OBJECT: 0x86633804

LAST_CALL_STACK: 0x9C1F3480 + 0x10

RULE_STATE: 0x9C1F3480
```

### <a name="identify-the-location-of-the-violation"></a>違反の場所を識別します。

例ではここでは、NdisTimedOidComplete.sys、ミニポート ドライバーでは、スリープのサイクルに挿入、 *MPOidRequest*関数。 最後をクリックして確認できます\_呼び出す\_のスタックのリンク、 [ **! ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)出力します。 これは、Driver Verifier、NDIS という名前の表示に表示される最後の呼び出し履歴*ndisMInvokeOidRequest*前に、タイムアウトが発生しました。

```
kd> dps 0x9C1F3480 + 0x10
9c1f3490  850e1e37 ndis!ndisMInvokeOidRequest+0x16641
9c1f3494  850765c8 ndis!ndisMDoOidRequest+0x24a
9c1f3498  8507552a ndis!ndisQueueOidRequest+0x2fa
9c1f349c  8507372b ndis!ndisQuerySetMiniportEx+0xd9
9c1f34a0  85073646 ndis!ndisQuerySetMiniport+0x18
9c1f34a4  850dd9c8 ndis!ndisMDoMiniportOp+0x8c
9c1f34a8  850dd916 ndis!ndisMNotifyMachineName+0xe4
9c1f34ac  85104005 ndis!ndisMInitializeAdapter+0xad7
```

### <a name="fixing-the-cause-of-the-ndis-wifi-timeout-violation"></a>タイムアウトの違反の NDIS WIFI の原因を修正

クラッシュ ダンプが時刻指定の規則の生成されたら、クラッシュ ダンプの時点で、根本原因が見つからない可能性があります。 さらにデバッグするには、NdisKd デバッガー拡張機能のコマンドを始めることを検討を参照してください[NDIS 拡張機能 (Ndiskd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff552270)と[NDISKD 入門](https://go.microsoft.com/fwlink/p/?linkid=327569)します。 確認する必要がありますも[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)ログは、ドライバーには、ETW が実装されている場合。 このルールが有効になっていない場合は、このエラーとして姿を現します自体ユーザーのアプリケーション ハング、または[ **0x9F のバグ チェック。ドライバー\_POWER\_状態\_エラー** ](https://msdn.microsoft.com/library/windows/hardware/ff559329)最悪の事態にします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NDIS 拡張機能 (Ndiskd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff552270)

[NDISKD (パート 1) の概要](https://go.microsoft.com/fwlink/p/?linkid=327569)

[NDISKD と! ミニポート (第 2 部)]( https://go.microsoft.com/fwlink/p/?linkid=327570)

[NDISKD (パート 3) を使用したデバッグ](https://go.microsoft.com/fwlink/p/?linkid=327571)











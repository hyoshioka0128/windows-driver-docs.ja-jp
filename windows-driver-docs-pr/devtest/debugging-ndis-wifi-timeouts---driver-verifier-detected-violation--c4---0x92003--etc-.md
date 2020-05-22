---
title: デバッグ DRIVER_VERIFIER_DETECTED_VIOLATION (C4)
description: ドライバーの検証ツールは、ドライバーが NDIS/WiFi タイムアウト規則のいずれかに違反していることを検出します。
ms.assetid: 73D4B6DF-E667-4C71-B985-FCDC05837908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e4a58821359fc066888e3e6ce071c5f777f9df6
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769722"
---
# <a name="debugging-ndiswifi-time-out-errors---driver_verifier_detected_violation-c4"></a>NDIS/WiFi タイムアウトエラーのデバッグ-ドライバー \_ 検証ツールが \_ 検出した \_ 違反 (C4)


[Ndis/wifi 検証](ndis-wifi-verification.md)オプションを選択し、ドライバーの検証ツールが Ndis/wifi タイムアウトルールのいずれかに違反していることを検出した場合、[ドライバー検証ツール](driver-verifier.md)は[**バグチェック 0xc4: ドライバー \_ 検証ツールが \_ 検出 \_ **](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)した違反 (パラメーター1は特定の NDIS/wifi タイムアウト規則の識別子と同じ) を生成します。

Driver Verifier が、 [**NdisTimedOidComplete**](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete)などの NDIS/WIFI タイムアウトルールをテストしている場合、ドライバー検証ツールのポーリングメカニズムでは、多くのサイクルでミニポートドライバーからの応答が必要になります。 時間ルールごとに、許可された独自の最大サイクルが定義されています。 最大値を超えると、ドライバーの検証ツールによってバグチェックが生成されます。 ここでは、これらの違反をデバッグするための方法の例について説明します。

## <a name="debugging-ndiswifi-timeout-errors"></a>NDIS/WIFI タイムアウトエラーのデバッグ


-   [! Analyze を使用して、バグチェックに関する情報を表示します](#use-analyze-to-display-information-about-the-bug-check)
-   [! Ruleinfo extension コマンドを使用します。](#use-the-ruleinfo-extension-command)
-   [[最後の \_ 呼び出し履歴] リンクをクリックして、 \_ 違反の場所を特定します。](#identify-the-location-of-the-violation)
-   [NDIS/WIFI タイムアウト違反の原因を修正しています](#fixing-the-cause-of-the-ndis-wifi-timeout-violation)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>! Analyze を使用して、バグチェックに関する情報を表示します

バグチェックが発生した場合と同様に、デバッガーを制御したら、最初に[**! analyze-v**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)コマンドを実行します。

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

**! Analyze-v**出力の次のセクションでは、[DV \_ 違反の条件] フィールドの下に規則違反が発生した理由が表示され \_ ます。 また、 \_ \_ このルールに関するドキュメントへのリンクを取得する場合も、「DV MSDN link」セクションを参照してください。

```
## Debugging Details:


*** ERROR: Module load completed but symbols could not be loaded for NdisTimedOidComplete.sys

DV_VIOLATED_CONDITION:  Timeout on completing an NDIS OID request.

DV_MSDN_LINK: https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete

DRIVER_OBJECT: 98a87980

IMAGE_NAME:  NdisTimedOidComplete.sys

DEBUG_FLR_IMAGE_TIMESTAMP:  5229c857

MODULE_NAME: NdisTimedOidComplete

FAULTING_MODULE: 9fee1000 NdisTimedOidComplete
```

この分析出力の下にある [DV ルールの情報] セクションのリンクをクリックすると、 \_ \_ 追加のルールの説明が表示されます。 タイムアウトの種類のルールの場合、現在のスタックに関連情報が含まれていない可能性があります。

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

### <a name="use-the-ruleinfo-extension-command"></a>! Ruleinfo extension コマンドを使用します。

**! Analyze**出力の " **DV \_ RULE \_ INFO:** " フィールドには、この規則違反に関する詳細情報を検索するために使用できるコマンドへのリンクが示されています。 この例では、リンクをクリックすると、 [**! ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)コマンドがルール \_ ID (0X92003) の Arg3 および Arg 4 バグチェック値と共に実行されます。

```
kd> !ruleinfo 0x92003 0xffffffff9c17b860 0xffffffff9c1f3480

RULE_ID: 0x92003

RULE_NAME: NdisTimedOidComplete

RULE_DESCRIPTION:
This rule verifies if an NDIS miniport driver completes an OID in time.
The OID is tracked (a.k.a., TRACKED_OBJECT). Use !ndiskd.oid .

MSDN_LINK: https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndistimedoidcomplete

CONTEXT: Miniport 0x86BD10E8

CURRENT_TIME (Timed Rules): 168 seconds

TRACKED_OBJECT: 0x86633804

LAST_CALL_STACK: 0x9C1F3480 + 0x10

RULE_STATE: 0x9C1F3480
```

### <a name="identify-the-location-of-the-violation"></a>違反の場所を特定する

ここで使用している例では、ミニポートドライバー NdisTimedOidComplete には、 *Mpoidrequest*関数にスリープサイクルが挿入されています。 \_ \_ [**! RULEINFO**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)出力の最後の呼び出し履歴リンクをクリックして確認できます。 これは、ドライバーの検証ツールによって表示される最後の呼び出し履歴です。これは、タイムアウトが発生する前に、NDIS が*ndisMInvokeOidRequest*という名前であることを示しています。

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

### <a name="fixing-the-cause-of-the-ndis-wifi-timeout-violation"></a>NDIS WIFI タイムアウト違反の原因を修正しています

時間指定のルールに対してクラッシュダンプが生成された場合、クラッシュダンプ時に根本原因が見つかる可能性があります。 さらにデバッグするには、NdisKd デバッガー拡張機能のコマンドから始めることを検討してください。詳細については、「 [NDIS Extensions (ndiskd .dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/ndis-extensions--ndiskd-dll-) 」および「 [ndiskd の](https://docs.microsoft.com/archive/blogs/ndis/getting-started-with-ndiskd)概要」を参照してください。 また、ドライバーで ETW が実装されている場合は、 [Windows イベントトレーシング (etw)](event-tracing-for-windows--etw-.md)ログを確認することが必要になる場合もあります。 このルールが有効になっていない場合、このエラーは、ユーザーアプリケーションが最適にハングしたとき、またはバグチェック 0x9F (最悪の場合は[**ドライバーの \_ 電源 \_ 状態 \_ エラー**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x9f--driver-power-state-failure) ) によって発生します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[NDIS 拡張機能 (Ndiskd.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/ndis-extensions--ndiskd-dll-)

[NDISKD の概要 (パート 1)](https://docs.microsoft.com/archive/blogs/ndis/getting-started-with-ndiskd)

[NDISKD と! ミニポート (パート 2)](https://docs.microsoft.com/archive/blogs/ndis/ndiskd-and-miniport)

[NDISKD を使用したデバッグ (パート 3)](https://docs.microsoft.com/archive/blogs/ndis/debugging-with-ndiskd)











---
title: ruleinfo
description: Ruleinfo コマンドは、ドライバーの検証規則に関する情報を表示します。
ms.assetid: 025FAAFA-7A5C-462C-9CC2-AA55530CD371
keywords:
- ruleinfo Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ruleinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04c852ebeca9cf09f0303a60cb957c76d8137391
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534709"
---
# <a name="ruleinfo"></a>!ruleinfo


**! Ruleinfo**コマンドは、ドライバーの検証規則に関する情報を表示します。

```dbgcmd
!ruleinfo RuleId [RuleState [SubState]]
```

## <a name="span-idddk__ptov_dbgspanspan-idddk__ptov_dbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>パラメータ


<span id="_______RuleId______"></span><span id="_______ruleid______"></span><span id="_______RULEID______"></span>*RuleId*   
検証規則の ID。 これは、DRIVER VERIFIER によっ[**て \_ \_ 検出された \_ 違反**](bug-check-0xc4--driver-verifier-detected-violation.md)のバグチェックの最初の引数です。

<span id="_______RuleState______"></span><span id="_______rulestate______"></span><span id="_______RULESTATE______"></span>*Rulestate*   
違反に関する追加の状態情報。 これは、**ドライバー \_ 検証ツールで \_ 検出された \_ 違反**バグチェックの3番目の引数です。

<span id="_______SubState______"></span><span id="_______substate______"></span><span id="_______SUBSTATE______"></span>*SubState*下位状態   
違反に関するサブ状態情報。 これは、 **DRIVER \_ VERIFIER で \_ 検出された \_ 違反**バグチェックの4番目の引数です。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ext .dll

<a name="remarks"></a>注釈
-------

このコマンドは、Driver Verifier 拡張機能のルールにのみ適用されます。つまり、ID が2以上のルールです。

次の例は、[**ドライバー \_ 検証ツールが検出し \_ た \_ 違反**](bug-check-0xc4--driver-verifier-detected-violation.md)バグチェックの4つの引数を示しています。

```dbgcmd
DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
...
Arguments:
Arg1: 0000000000091001, ID of the 'NdisOidComplete' rule that was violated.
Arg2: fffff800002d49d0, A pointer to the string describing the violated rule condition.
Arg3: ffffe000027b8370, Address of internal rule state (second argument to !ruleinfo).
Arg4: ffffe000027b83f8, Address of supplemental states (third argument to !ruleinfo).

## Debugging Details:


DV_VIOLATED_CONDITION:  This OID should only be completed with NDIS_STATUS_NOT_ACCEPTED, 
                        NDIS_STATUS_SUCCESS, or NDIS_STATUS_PENDING.

DV_MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278802

DRIVER_OBJECT: ffffe0000277a2b0
...

STACK_TEXT:  
ffffd000`2118ff58 fffff803`4c83afa2 : 00000000`000000c4 00000000`00000001 ...
ffffd000`2118ff60 fffff803`4c83a8c0 : 00000000`00000003 00000000`00091001 ...
...

STACK_COMMAND:  kb

FOLLOWUP_NAME:  Xxxx

FAILURE_BUCKET_ID:  Xxxx
...
```

上記の出力では、ルール ID (0x91001) は Arg1 として表示されます。 Arg3 と Arg4 は、ルールの状態と下位の情報のアドレスです。 ルール ID、ルールの状態、および下位部分を **! ruleinfo**に渡すと、ルールの説明と、ルールの詳細なドキュメントへのリンクを取得できます。

```dbgcmd
3: kd> !ruleinfo 0x91001 0xffffe000027b8370 0xffffe000027b83f8

RULE_ID: 0x91001

RULE_NAME: NdisOidComplete

RULE_DESCRIPTION:
This rule verifies if an NDIS miniport driver completes an OID correctly.
Check RULE_STATE for Oid ( use !ndiskd.oid ), which can be one of the following:
1) NULL,
2) Pending OID, or
3) Previous OID if no OID is pending.

MSDN_LINK: https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-ndisoidcomplete

CONTEXT: Miniport 0xFFFFE0000283F1A0

CURRENT_TIME (Timed Rules): 142 seconds

RULE_STATE: 0xFFFFE000027B83F8
```

 

 






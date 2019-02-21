---
title: ruleinfo
description: Ruleinfo コマンドでは、Driver Verifier の規則に関する情報が表示されます。
ms.assetid: 025FAAFA-7A5C-462C-9CC2-AA55530CD371
keywords:
- Windows デバッグ ruleinfo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ruleinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c4b75b692992085c20b7988766b4d46b4b49eef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558033"
---
# <a name="ruleinfo"></a>! ruleinfo


**! Ruleinfo**コマンドは、Driver Verifier の規則に関する情報を表示します。

```dbgcmd
!ruleinfo RuleId [RuleState [SubState]]
```

## <a name="span-idddkptovdbgspanspan-idddkptovdbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>パラメーター


<span id="_______RuleId______"></span><span id="_______ruleid______"></span><span id="_______RULEID______"></span> *RuleId*   
検証規則の ID。 これは、最初の引数、 [**ドライバー\_VERIFIER\_検出\_違反**](bug-check-0xc4--driver-verifier-detected-violation.md)バグ チェックします。

<span id="_______RuleState______"></span><span id="_______rulestate______"></span><span id="_______RULESTATE______"></span> *RuleState*   
違反に関する追加の状態情報。 これは、3 番目の引数、**ドライバー\_VERIFIER\_検出\_違反**バグ チェックします。

<span id="_______SubState______"></span><span id="_______substate______"></span><span id="_______SUBSTATE______"></span> *下位状態*   
サブ状態の違反に関する情報。 これは、4 番目の引数、**ドライバー\_VERIFIER\_検出\_違反**バグ チェック。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll

<a name="remarks"></a>注釈
-------

このコマンドは、Driver Verifier 拡張; 規則にのみ適用されます。つまり、ルールは 0x10000 以上 ID があります。

次の例では、4 つの引数を[**ドライバー\_VERIFIER\_検出\_違反**](bug-check-0xc4--driver-verifier-detected-violation.md)バグ チェックします。

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

上記の出力として、Arg1 ルール ID (0x91001) が表示されます。 Arg3 と Arg4、ルールの状態と substate 情報のアドレスです。 ルール ID、ルールの状態およびに下位状態を渡すことができます **! ruleinfo**ルールとルールの詳細なドキュメントへのリンクの説明を取得します。

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

MSDN_LINK: https://go.microsoft.com/fwlink/p/?linkid=278802

CONTEXT: Miniport 0xFFFFE0000283F1A0

CURRENT_TIME (Timed Rules): 142 seconds

RULE_STATE: 0xFFFFE000027B83F8
```

 

 






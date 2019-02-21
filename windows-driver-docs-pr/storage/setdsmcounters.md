---
title: SetDSMCounters 関数
description: SetDSMCounters メソッドは、特定の DSM のタイマー カウンターの設定に使用されます。
ms.assetid: 6ea2ae07-d50e-48af-92da-7a5083a75bc7
keywords:
- 記憶装置の SetDSMCounters 関数
topic_type:
- apiref
api_name:
- SetDSMCounters
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e08c7f773f9fa31352c1da62da982958219ec11a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557455"
---
# <a name="setdsmcounters-function"></a>SetDSMCounters 関数


SetDSMCounters メソッドは、特定の DSM のタイマー カウンターの設定に使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SetDSMCounters(
   [in, Description("DSM Context"):amended] uint64              DSMcontext,
   [in, Description("DSM Timer Counters"):amended] DSM_COUNTERS DsmCounters
);
```

<a name="parameters"></a>パラメーター
----------

*DSMcontext*   
64-ビット フィールド DSM コンテキストを提供します。

*DsmCounters*   
DSM\_カウンター構造体。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MPIO が属する\_WMI\_メソッド WMI クラスです。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">MPIOwmi.h (include MPIOwmi.h)</td>
</tr>
</tbody>
</table>

 

 






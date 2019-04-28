---
title: ClearPathHealthCounters 関数
description: ClearPathHealthCounters メソッドは、MPIO ディスクの特定のパスの収集されたすべての MPIO の正常性の統計をクリアに使用されます。
ms.assetid: 97f110c9-50c4-4570-ad5e-d1d17b711c6a
keywords:
- 記憶装置の ClearPathHealthCounters 関数
topic_type:
- apiref
api_name:
- ClearPathHealthCounters
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bf3dafd907adb31d354a6fd7bb3a0fdc43fa538c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360929"
---
# <a name="clearpathhealthcounters-function"></a>ClearPathHealthCounters 関数


ClearPathHealthCounters メソッドは、MPIO ディスクの特定のパスの収集されたすべての MPIO の正常性の統計をクリアに使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void ClearPathHealthCounters(
   [in, Description("64-bit Path Identifier"):amended] uint64 PathID
);
```

<a name="parameters"></a>パラメーター
----------

*PathID*   
64-ビット フィールド、デバイスに関連付けられているパスを指定します。

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

 

 






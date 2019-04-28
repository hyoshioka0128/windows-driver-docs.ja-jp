---
title: ClearMpioDiskHealthCounters 関数
description: ClearMpioDiskHealthCounters メソッドは、MPIO ディスクの収集の MPIO の統計情報をクリアに使用されます。
ms.assetid: 1ac415b2-87d4-430d-8713-a871c6af1006
keywords:
- 記憶装置の ClearMpioDiskHealthCounters 関数
topic_type:
- apiref
api_name:
- ClearMpioDiskHealthCounters
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a44ed8a1d28bd03383d46b11421daedc737ccd1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379996"
---
# <a name="clearmpiodiskhealthcounters-function"></a>ClearMpioDiskHealthCounters 関数


ClearMpioDiskHealthCounters メソッドは、MPIO ディスクの収集の MPIO の統計情報をクリアに使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void ClearMpioDiskHealthCounters(
   [in, Description("MPIO Disk Ordinal"):amended] uint32 DiskOrdinal
);
```

<a name="parameters"></a>パラメーター
----------

*DiskOrdinal*   
MPIO を表す 32 ビット ディスクの序数値。

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

 

 






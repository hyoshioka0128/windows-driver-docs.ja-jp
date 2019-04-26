---
title: GetPathConfiguration 関数
description: GetPathConfiguration メソッドを使用して、パスごとにデバイス情報を取得します。
ms.assetid: 1661746f-5a5a-48af-b876-c57f19de4923
keywords:
- 記憶装置の GetPathConfiguration 関数
topic_type:
- apiref
api_name:
- GetPathConfiguration
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5d81c1dbbd0dd708699cb1f70f5cc068dd02f3d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354074"
---
# <a name="getpathconfiguration-function"></a>GetPathConfiguration 関数


GetPathConfiguration メソッドを使用して、パスごとにデバイス情報を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetPathConfiguration(
   [in, Description("64-bit Path Identifier"):amended] uint64 PathID,
   [out] uint32                                               EntryCount,
   [out, WmiSizeIs("EntryCount")] SCSI_ADDR                   Address[]
);
```

<a name="parameters"></a>パラメーター
----------

*PathID*   
64-ビット フィールド、デバイスに関連付けられているパスを指定します。

*EntryCount*   
32-ビット フィールドを出力が含まれるエントリの数を示します。

*アドレス\[\]*   
多くの SCSI を格納する配列\_で指定された構造体のアドレス、 *EntryCount*パラメーター。

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

 

 






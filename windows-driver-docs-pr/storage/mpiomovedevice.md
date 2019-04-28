---
title: MPIOMoveDevice 関数
description: MPIOMoveDevice メソッドは、デバイス上のアクティブ パスの設定に使用されます。
ms.assetid: aa3da461-ea55-4f60-b957-eb6b6cc3aeec
keywords:
- 記憶装置の MPIOMoveDevice 関数
topic_type:
- apiref
api_name:
- MPIOMoveDevice
api_location:
- MPIOwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d99804d6eb0aecdbf9d529ec0627f077c519538
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377471"
---
# <a name="mpiomovedevice-function"></a>MPIOMoveDevice 関数


MPIOMoveDevice メソッドは、デバイス上のアクティブ パスの設定に使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void MPIOMoveDevice(
   [in, Description("MPIO Disk Ordinal"):amended] uint32    DiskOrdinal,
   [in, Description("Move Flags."):amended] uint32          Flags,
   [in, Description("PathID to set Active"):amended] uint64 PathID
);
```

<a name="parameters"></a>パラメーター
----------

*DiskOrdinal*   
32 ビット、MPIO を指定するディスクの序数値。

*フラグ*   
32-ビット フィールド、デバイスの移動に関連付けられているフラグを指定します。

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

 

 






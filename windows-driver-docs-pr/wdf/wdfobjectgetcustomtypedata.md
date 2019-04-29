---
title: WdfObjectGetCustomTypeData マクロ
description: WdfObjectGetCustomTypeData マクロでは、ドライバーは以前、framework のオブジェクトとカスタムの型に関連付けられたデータを取得します。
ms.assetid: 60A6546B-84C6-4A53-BAA1-3719DCBA63B4
keywords:
- WdfObjectGetCustomTypeData マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d51725eb8d1740c10024987ddba5cb15c7f9e9c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385737"
---
# <a name="wdfobjectgetcustomtypedata-macro"></a>WdfObjectGetCustomTypeData マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectGetCustomTypeData**マクロは、ドライバーは以前、framework のオブジェクトとカスタムの型に関連付けられたデータを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PULONG WdfObjectGetCustomTypeData(
  [in]  Handle,
  [in]  Type
);
```

<a name="parameters"></a>パラメーター
----------

*処理*\[で\]  
Framework のオブジェクトへのハンドル。

*型*\[で\]  
カスタム型のシンボル名。

<a name="return-value"></a>戻り値
------------

**WdfObjectGetCustomTypeData** 、ドライバーは、framework のオブジェクトと以前の呼び出しにカスタムの型に関連付けられているデータを返す[ **WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)します。

<a name="remarks"></a>注釈
-------

オブジェクトのドライバーの種類の詳細については、次を参照してください。 [Framework オブジェクトのカスタム型](https://msdn.microsoft.com/library/windows/hardware/hh406457)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td><p>最小 KMDF バージョン</p></td>
<td><p>1.11</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject.h (Wdf.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 







---
title: WdfObjectIsCustomType マクロ
description: WdfObjectIsCustomType マクロは、framework のオブジェクトが、指定したカスタム型かどうかを判断します。
ms.assetid: EE3CC41D-6FBA-49A2-A2A0-C7E818F6FAAA
keywords:
- WdfObjectIsCustomType マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ba823aba603d630fca01bd84f61ac10c6e9bed7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570478"
---
# <a name="wdfobjectiscustomtype-macro"></a>WdfObjectIsCustomType マクロ


\[KMDF および UMDF に適用されます。\]

**WdfObjectIsCustomType**マクロは、framework のオブジェクトが、指定したカスタム型かどうかを決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
BOOLEAN WdfObjectIsCustomType(
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

指定したオブジェクトが指定されたカスタム型の場合は、TRUE を返します。 それ以外の場合、FALSE を返します。

<a name="remarks"></a>コメント
-------

オブジェクトのカスタム種類の詳細については、[Framework オブジェクトのカスタム型](https://msdn.microsoft.com/library/windows/hardware/hh406457)を参照してください。

<a name="requirements"></a>必要条件
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

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

 

 







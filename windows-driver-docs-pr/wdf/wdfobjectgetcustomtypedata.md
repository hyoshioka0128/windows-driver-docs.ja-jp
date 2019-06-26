---
title: WdfObjectGetCustomTypeData マクロ
description: WdfObjectGetCustomTypeData マクロでは、ドライバーは以前、framework のオブジェクトとカスタムの型に関連付けられたデータを取得します。
ms.assetid: 60A6546B-84C6-4A53-BAA1-3719DCBA63B4
keywords:
- WdfObjectGetCustomTypeData マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62f1508c9897e1b9f4beff59fe0c293bfdc8a04b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372080"
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

オブジェクトのドライバーの種類の詳細については、次を参照してください。 [Framework オブジェクトのカスタム型](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-custom-types)します。

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

 

 







---
title: WDF_DECLARE_CUSTOM_TYPE マクロ
description: WDF_DECLARE_CUSTOM_TYPE マクロは、名前とドライバーのカスタム型のアクセサー メソッドを作成します。
ms.assetid: DF496E17-B3D4-4983-8506-40810ECAEA3E
keywords:
- WDF_DECLARE_CUSTOM_TYPE マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c854288285992a6e451d02a4b3715411700a3e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373444"
---
# <a name="wdfdeclarecustomtype-macro"></a>WDF_DECLARE_CUSTOM_TYPE マクロ


\[KMDF および UMDF に適用されます。\]

**WDF_DECLARE_CUSTOM_TYPE**マクロ名とドライバーのカスタム型のアクセサー メソッドを作成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void WDF_DECLARE_CUSTOM_TYPE(
    _customtype
);
```

<a name="parameters"></a>パラメーター
----------

*_customtype*   
ドライバーで定義されたカスタム型の名前。

<a name="return-value"></a>戻り値
------------

このマクロでは、値は返されません。

<a name="remarks"></a>注釈
-------

呼び出すときに**WDF_DECLARE_CUSTOM_TYPE**ドライバーは、独自のカスタム型の名前を定義します。 カスタム型の名前を選択する場合は、ドライバーのドメインに固有の名前を選択します。 通常、始めないでください、カスタムの型名のプレフィックスを持つ*Wdf*します。

オブジェクトのカスタム種類の詳細については、次を参照してください。 [Framework オブジェクトのカスタム型](https://msdn.microsoft.com/library/windows/hardware/hh406457)します。

<a name="examples"></a>例
--------

次のコード例では、 **WDF_DECLARE_CUSTOM_TYPE** MY_CUSTOM_TYPE カスタム型の名前を宣言するマクロ。 ドライバーは、ヘッダー ファイルでは通常、グローバル データを宣言するドライバーの領域で行を配置する必要があります。

```cpp
WDF_DECLARE_CUSTOM_TYPE(MY_CUSTOM_TYPE)
```

次のコード例は、要求オブジェクトを作成し、次を使用して、 [ **WdfObjectAddCustomType** ](wdfobjectaddcustomtype.md)メソッドに関連付ける、 **MY_CUSTOM_TYPE**カスタム型で、要求オブジェクト。

```cpp
WDFREQUEST Request;
WDF_OBJECT_ATTRIBUTES MyRequestObjectAttributes;

WDF_OBJECT_ATTRIBUTES_INIT(&amp;MyRequestObjectAttributes);

status = WdfRequestCreate(
                          &amp;MyRequestObjectAttributes
                          NULL,
                          &amp;Request
                          );

if (!NT_SUCCESS(status)) {
    return status;
}

status = WdfObjectAddCustomType(
                          Request,
                          MY_CUSTOM_TYPE
                          );

if (!NT_SUCCESS(status)) {
    return status;
}
```

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


[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectAddCustomTypeWithData**](wdfobjectaddcustomtypewithdata.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 







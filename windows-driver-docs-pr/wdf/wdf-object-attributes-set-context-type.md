---
title: WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロ
description: WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロは、オブジェクトのドライバー定義コンテキスト情報をオブジェクトの WDF_OBJECT_ATTRIBUTES 構造体に挿入します。
ms.assetid: cac8b8f4-cc6b-4e6c-ad0b-dee58e4673ff
keywords:
- WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロ
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a911369335024996c4adc77bf9aafef13966b11e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845417"
---
# <a name="wdf_object_attributes_set_context_type-macro"></a>WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロ


\[KMDF と UMDF\] に適用されます

WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロは、オブジェクトのドライバー定義コンテキスト情報をオブジェクトの[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体に挿入します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
    _attributes,
    _contexttype
);
```

<a name="parameters"></a>パラメーター
----------

*_attributes*   
オブジェクトの[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体へのポインター。

*_contexttype*   
オブジェクトのコンテキスト空間の内容を記述するドライバー定義の構造体の構造体型の名前。

<a name="return-value"></a>戻り値
------------

このマクロは値を返しません。

<a name="remarks"></a>注釈
-------

[**WDF_OBJECT_ATTRIBUTES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)を呼び出した後、WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロを使用する必要があります。

WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE マクロの使用方法の詳細については、「 [Framework オブジェクトコンテキスト空間](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-context-space)」を参照してください。

このマクロを使用するコード例については、「 [**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)」を参照してください。

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
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF バージョン</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject .h (Wdf を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

[**WDF_OBJECT_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)

[**WDF_OBJECT_ATTRIBUTES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)

[**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**](wdf-object-attributes-init-context-type.md)

 

 







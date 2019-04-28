---
title: IPrinterBidiSchemaElement BidiType メソッド
description: BidiType メソッドは、Bidi スキーマ要素の型を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 7E074633-E3AA-45F3-A0B6-621E97E983A8
keywords:
- 印刷デバイスの BidiType メソッド
- BidiType メソッド、印刷デバイス IPrinterBidiSchemaElement インターフェイス
- IPrinterBidiSchemaElement インターフェイス、印刷デバイス BidiType メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.BidiType
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7271f72d0ea0d010a4c8a15549f99dbdfd8f91e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371204"
---
# <a name="iprinterbidischemaelementbiditype-method"></a>IPrinterBidiSchemaElement::BidiType メソッド

BidiType メソッドは、Bidi スキーマ要素の型を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT BidiType(
  [out, retval] PrinterBidiSchemaElementType *pType
);
```

<a name="parameters"></a>パラメーター
----------

*pType* \[out, retval\]  
返される要素の型。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

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
<td>Desktop</td>
</tr>
<tr class="even">
<td><p>バージョン</p></td>
<td><p>Windows 8 以降</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)

[**PrinterBidiSchemaElementType**](printerbidischemaelementtype.md)

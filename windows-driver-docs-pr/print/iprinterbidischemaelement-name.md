---
title: IPrinterBidiSchemaElement 名メソッド
description: 名前のメソッドは、Bidi スキーマ要素の名前を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 682B3DFE-EE21-4C96-B585-1D63287C33A0
keywords:
- 印刷デバイス メソッドを名前します。
- 印刷デバイス、IPrinterBidiSchemaElement インターフェイスのメソッドを名前します。
- IPrinterBidiSchemaElement インターフェイス、印刷デバイス名メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.Name
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbe247e5f9cd7f9716a4bfa7c401b6a6d1bbc18c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578572"
---
# <a name="iprinterbidischemaelementname-method"></a>IPrinterBidiSchemaElement::Name メソッド

名前のメソッドは、Bidi スキーマ要素の名前を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT Name(
  [out, retval] BSTR *pbstrSchema
);
```

<a name="parameters"></a>パラメーター
----------

*pbstrSchema* \[out, retval\]  
返される要素の名前。

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

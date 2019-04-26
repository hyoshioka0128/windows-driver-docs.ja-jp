---
title: IPrinterBidiSchemaResponses AddEnum メソッド
description: AddEnum メソッドは、双方向のタイプの新しい応答を追加します。\_コレクションを列挙します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: B172DF90-63F8-4064-8781-EB0E8D799C1A
keywords:
- 印刷デバイスの AddEnum メソッド
- AddEnum メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス印刷デバイス、AddEnum メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddEnum
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4cd1e0bd3633f61d6bfdd8b0ec647e6916d79bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351644"
---
# <a name="iprinterbidischemaresponsesaddenum-method"></a>IPrinterBidiSchemaResponses::AddEnum メソッド

AddEnum メソッドは、双方向のタイプの新しい応答を追加します。\_コレクションを列挙します。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddEnum(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマです。

*bstrValue* \[in\]  
列挙値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

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
<td>Desktop</td>
</tr>
<tr class="even">
<td><p>バージョン</p></td>
<td><p>Windows 8 以降</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)

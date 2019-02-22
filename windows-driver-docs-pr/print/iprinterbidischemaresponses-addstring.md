---
title: IPrinterBidiSchemaResponses AddString メソッド
description: AddString メソッドは、双方向のタイプの新しい応答を追加します。\_コレクションへの文字列。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ACBE70E7-5A2B-4472-B1A3-40722D849119
keywords:
- AddString メソッド印刷デバイス
- AddString メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddString メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddString
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 843f04bb47bcc68603f8be4bbecdb8cd58c4bbdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552166"
---
# <a name="iprinterbidischemaresponsesaddstring-method"></a>IPrinterBidiSchemaResponses::AddString メソッド

AddString メソッドは、双方向のタイプの新しい応答を追加します。\_コレクションへの文字列。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddString(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマです。

*bstrValue* \[in\]  
文字列の応答です。

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
<td><p>Windows 8 以降</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)

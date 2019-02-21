---
title: IPrinterBidiSchemaResponses AddRequeryKey メソッド
description: GetSchemas 呼び出しからの戻り時に再クエリする新しい QueryKey を AddRequeryKey メソッドに追加します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: D2C418C4-3C1B-4CEA-9F39-036C4DB2A483
keywords:
- 印刷デバイスの AddRequeryKey メソッド
- AddRequeryKey メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddRequeryKey メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddRequeryKey
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 335f75d02acd7c6661a013aec81c2e4beb1898b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556843"
---
# <a name="iprinterbidischemaresponsesaddrequerykey-method"></a>IPrinterBidiSchemaResponses::AddRequeryKey メソッド

GetSchemas 呼び出しからの戻り時に再クエリする新しい QueryKey を AddRequeryKey メソッドに追加します。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddRequeryKey(
  [in] BSTR   bstrQueryKey
);
```

<a name="parameters"></a>パラメーター
----------

 *bstrQueryKey* \[in\]  
新しい QueryKey します。

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

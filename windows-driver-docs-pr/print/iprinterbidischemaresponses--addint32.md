---
title: IPrinterBidiSchemaResponses AddInt32 メソッド
description: AddInt32 メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションに INT。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: F937B098-9C13-4337-82A6-C26DAA8B7068
keywords:
- 印刷デバイスの AddInt32 メソッド
- AddInt32 メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddInt32 メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddInt32
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c980d99dc50e5da1e731132b5ffe7d9703267cc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351680"
---
# <a name="iprinterbidischemaresponsesaddint32-method"></a>IPrinterBidiSchemaResponses::AddInt32 メソッド

AddInt32 メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションに INT。

<a name="syntax"></a>構文
------

```cpp
HRESULT  AddInt32(
  [in] BSTR bstrSchema,
  [in] LONG lValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマです。

*lValue* \[in\]  
新しい値。

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

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)

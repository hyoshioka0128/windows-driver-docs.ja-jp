---
title: IPrinterBidiSchemaResponses AddBool メソッド
description: AddBool メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションにブール値。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 8D1C9198-DE72-4348-84EE-C3B875D14E6A
keywords:
- 印刷デバイスの AddBool メソッド
- AddBool メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddBool メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddBool
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e091d231c1bda1bc98f6260b26e073dd03f1f1ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573601"
---
# <a name="iprinterbidischemaresponsesaddbool-method"></a>IPrinterBidiSchemaResponses::AddBool メソッド

AddBool メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションにブール値。

<a name="syntax"></a>構文
------

```cpp
HRESULT  AddBool(
  [in] BSTR bstrSchema,
  [in] BOOL bValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマです。

*bValue* \[in\]  
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

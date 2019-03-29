---
title: IPrinterBidiSchemaResponses AddFloat メソッド
description: AddFloat メソッドは、双方向のタイプの新しい応答を追加します。\_コレクションに寄せて配置します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 99A66884-3528-43C3-AC56-CE0AA64AB328
keywords:
- 印刷デバイスの AddFloat メソッド
- AddFloat メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddFloat メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddFloat
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60dffed4a7b0147fd7e8266d987f8e147db8af9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580879"
---
# <a name="iprinterbidischemaresponsesaddfloat-method"></a>IPrinterBidiSchemaResponses::AddFloat メソッド

AddFloat メソッドは、双方向のタイプの新しい応答を追加します。\_コレクションに寄せて配置します。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddFloat(
  [in] BSTR    bstrSchema,
  [in] FLOAT  fValue 
);
```

<a name="parameters"></a>パラメーター
----------

 *bstrSchema* \[in\]  
スキーマです。

 *fValue* \[in\]  
新しい浮動小数点値。

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

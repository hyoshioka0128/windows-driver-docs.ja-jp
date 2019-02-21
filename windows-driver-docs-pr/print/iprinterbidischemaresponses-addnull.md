---
title: IPrinterBidiSchemaResponses AddNull メソッド
description: AddNull メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションに NULL です。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 36796227-7EE4-43C8-9AD7-51A3929D1CE2
keywords:
- 印刷デバイスの AddNull メソッド
- AddNull メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddNull メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddNull
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21dcc47f9497003d4b79d1f2f21398a65a55fe21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537847"
---
# <a name="iprinterbidischemaresponsesaddnull-method"></a>IPrinterBidiSchemaResponses::AddNull メソッド

AddNull メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションに NULL です。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddNull(
  [in] BSTR bstrSchema
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマ名。

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

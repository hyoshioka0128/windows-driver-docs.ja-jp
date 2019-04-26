---
title: IPrinterBidiSchemaResponses AddText メソッド
description: AddText メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションにテキスト。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 2421D77A-E0B2-4114-A27E-59E0D9A88E7C
keywords:
- 印刷デバイスの AddText メソッド
- AddText メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddText メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddText
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c35fca3151be6c17859aacecacbb900173c7fae1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351639"
---
# <a name="iprinterbidischemaresponsesaddtext-method"></a>IPrinterBidiSchemaResponses::AddText メソッド

AddText メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションにテキスト。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddText(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマです。

*bstrValue* \[in\]  
テキスト。

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

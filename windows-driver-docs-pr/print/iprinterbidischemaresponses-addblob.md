---
title: IPrinterBidiSchemaResponses AddBlob メソッド
description: AddBlob メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションに BLOB。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 9CB33F44-5DB8-4504-AD88-AEBE99C1E527
keywords:
- 印刷デバイスの AddBlob メソッド
- AddBlob メソッド、印刷デバイス IPrinterBidiSchemaResponses インターフェイス
- IPrinterBidiSchemaResponses インターフェイス、印刷デバイス AddBlob メソッド
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddBlob
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5bf5d1d44db427dd71efd043be9ef97523b297c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351660"
---
# <a name="iprinterbidischemaresponsesaddblob-method"></a>IPrinterBidiSchemaResponses::AddBlob メソッド

AddBlob メソッドは、双方向のタイプの新しい応答を追加します。\_をコレクションに BLOB。

<a name="syntax"></a>構文
------

```cpp
HRESULT AddBlob(
  [in] BSTR      bstrSchema,
  [in] IDispatch *pArray
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSchema* \[in\]  
スキーマです。

*pArray* \[in\]  
配列です。

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

---
title: Iasphelp オープン メソッド
description: Open メソッドは、ASP Web ページをプリンターにアクセスできます。
MS-HAID:
- webfnc\_7fa3a36d-4bf6-46d2-9336-e024d3aa1eec.xml
- print.iasphelp\_open
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: f4e39b76-3118-41d8-a5f8-501d884cbcdb
keywords:
- 印刷デバイスの open メソッド
- Open メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス印刷デバイス、Open メソッド
topic_type:
- apiref
api_name:
- Iasphelp.Open
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 499de74e720d5bd8c23880e7a64819e0df90420d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559619"
---
# <a name="iasphelpopen-method"></a>Iasphelp::Open メソッド

**開く**メソッドは、プリンターへのアクセスを開く ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT Open(
  [in] BSTR bstrPrinterName
);
```

<a name="parameters"></a>パラメーター
----------

*bstrPrinterName* \[in\]  
プリンター名を含む文字列への呼び出し元が指定のポインター。

<a name="return-value"></a>戻り値
------------

Win32 エラー コードを返すこともできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>S_OK を返します</strong></td>
<td><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>ERROR_INVALID_PRINTER_NAME</strong></td>
<td><p>無効なプリンターの名前。</p></td>
</tr>
<tr class="odd">
<td><strong>ERROR_NOT_ENOUGH_MEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、印刷スプーラーを呼び出すことによって指定されたプリンターへのアクセスを取得**ようになりました**関数。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

後に、 **Iasphelp::Open**呼び出し、プリンターはされるまで開いたまま、 [ **Iasphelp::Close** ](iasphelp-close.md)メソッドが呼び出されるまで、または**Iasphelp::Open**が別のプリンターの名前で再度呼び出されます。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
```

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
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**Iasphelp::Close**](iasphelp-close.md)

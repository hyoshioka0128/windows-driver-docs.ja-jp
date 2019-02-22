---
title: Iasphelp get\_ErrorDscp メソッド
description: ErrorDscp プロパティは、エラー コードをわかりやすい文字列に変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_55f547fe-4cbe-4905-b268-afd7af400de4.xml
- print.iasphelp\_errordscp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 46d44c54-4fd5-489f-9624-1df3c8917237
keywords:
- 印刷デバイスの get_ErrorDscp メソッド
- get_ErrorDscp メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_ErrorDscp メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_ErrorDscp
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16568f8224786cabf4b8a857d0d87de3bfe62173
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561044"
---
# <a name="iasphelpgeterrordscp-method"></a>Iasphelp::get\_ErrorDscp メソッド

**ErrorDscp**プロパティは、エラー コードをわかりやすい文字列に変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_ErrorDscp(
  [in]  long lErrCode,
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*lErrCode* \[in\]  
わかりやすい文字列に変換するエラー コードを指定します。

*pVal* \[out\]  
エラー コードに対応するわかりやすい文字列を受け取る場所への呼び出し元が指定のポインター、 *lErrCode*パラメーター。

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
<td><strong>E_HANDLE</strong></td>
<td><p><strong>Iasphelp::Open</strong>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_POINTER</strong></td>
<td><p>無効な<em>pVal</em>ポインター。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::ErrorDscp**プロパティのクエリを実行できます。

```vb
Dim objPrinter, ErrorCode, ErrorString
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
...
' Get error code.
...
ErrorString = objPrinter.ErrorDscp(ErrorCode)
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

[**Iasphelp::Open**](iasphelp-open.md)

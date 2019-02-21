---
title: Iasphelp get\_ShareName メソッド
description: ShareName プロパティは、プリンターの共有名を取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_68b8e99e-a40b-44ee-94c8-2a8bcc293fa3.xml
- print.iasphelp\_sharename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: fdb93613-9c7f-49ea-b90e-684b63e6417a
keywords:
- 印刷デバイスの get_ShareName メソッド
- get_ShareName メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_ShareName メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_ShareName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 805acbb28a55420e46e5a9fabef87475fa375fa8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549411"
---
# <a name="iasphelpgetsharename-method"></a>Iasphelp::get\_ShareName メソッド

**ShareName**プロパティは、プリンターの共有名を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_ShareName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
共有名の文字列へのポインターを受信する場所への呼び出し元が指定のポインター。

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
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::ShareName**プロパティのクエリを実行できます。

```vb
Dim objPrinter, DrvrName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
DrvrName = objPrinter.ShareName
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

---
title: Iasphelp get\_IsHTTP メソッド
description: IsHTTP プロパティは、HTTP ポートにプリンターが接続されているかどうかを判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_e3e58eea-498f-4e85-8072-2c49ac50d733.xml
- print.iasphelp\_ishttp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 54aaed11-8f18-433b-b774-c695a85b813e
keywords:
- 印刷デバイスの get_IsHTTP メソッド
- get_IsHTTP メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_IsHTTP メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_IsHTTP
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f6058d7e5de23aa7b556a7a87241dabfdaaa976
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538564"
---
# <a name="iasphelpgetishttp-method"></a>Iasphelp::get\_IsHTTP メソッド

**IsHTTP**プロパティは、HTTP ポートにプリンターが接続されているかどうかを判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_IsHTTP(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
受信するメモリ位置への呼び出し元が指定したポインター **TRUE** HTTP ポートにプリンターが接続されている場合と**FALSE**それ以外の場合。

<a name="return-value"></a>戻り値
------------

プロパティは、次の表に、値のいずれかを返します。

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

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::IsHTTP**プロパティのクエリを実行できます。

```vb
Dim objPrinter, IsHTTPPort
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
IsHTTPPort = objPrinter.IsHTTP
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

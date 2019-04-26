---
title: IOleCvt DecodeUnicodeName メソッド
description: DecodeUnicodeName プロパティは、同等の ANSI に Unicode 文字列を変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_50fe9203-d31e-4af4-a34f-b32dfd3dd7b1.xml
- print.iolecvt\_decodeunicodename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: d00fdabd-611a-4f26-8ca5-21ba8c28d993
keywords:
- 印刷デバイスの DecodeUnicodeName メソッド
- DecodeUnicodeName メソッド、印刷デバイス IOleCvt インターフェイス
- IOleCvt インターフェイス、印刷デバイス DecodeUnicodeName メソッド
topic_type:
- apiref
api_name:
- IOleCvt.DecodeUnicodeName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f585b640594a8737272f7238c1a3c3428b3d69d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345281"
---
# <a name="iolecvtdecodeunicodename-method"></a>IOleCvt::DecodeUnicodeName メソッド

**DecodeUnicodeName**プロパティは、等価な ANSI に Unicode 文字列を変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
[propget, id(3), helpstring("property DecodeUnicodeName")] HRESULT DecodeUnicodeName(
  [in]          BSTR bstrSrcName,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSrcName* \[in\]  
呼び出し元が指定した Unicode 文字列を変換します。

*pVal* \[out, retval\]  
翻訳された文字列を受け取る場所への呼び出し元が指定のポインター。

<a name="return-value"></a>戻り値
------------

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
<td><strong>S_OK</strong></td>
<td><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_POINTER</strong></td>
<td><p>有効なメモリの場所に少なくとも 1 つのパラメーターが指していません。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

```vb
Dim OleCvt, strPrinter, strEncodedPrinter
Set OleCvt = Server.CreateObject("OlePrn.OleCvt")
strEncodedPrinter = Request ( "eprinter" )
strPrinter = OleCvt.DecodeUnicodeName (strEncodedPrinter)
```

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
</tbody>
</table>

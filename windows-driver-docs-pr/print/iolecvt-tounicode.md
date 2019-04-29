---
title: IOleCvt ToUnicode メソッド
description: ToUnicode プロパティは、指定されたコード ページを使用して 1 つの Unicode 文字列に変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_37f4684f-4af9-4e25-8c5e-6ad63748cf5d.xml
- print.iolecvt\_tounicode
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e03997f6-e9b5-403e-99da-52504960cb99
keywords:
- 印刷デバイスの ToUnicode メソッド
- ToUnicode メソッド、印刷デバイス IOleCvt インターフェイス
- IOleCvt インターフェイス、印刷デバイス ToUnicode メソッド
topic_type:
- apiref
api_name:
- IOleCvt.ToUnicode
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d65d923424f33bc48dc3201f46c4cda11266ab94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324859"
---
# <a name="iolecvttounicode-method"></a>IOleCvt::ToUnicode メソッド

**ToUnicode**プロパティが指定されたコード ページを使用して 1 つの Unicode 文字列に変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
[propget, id(4), helpstring("property ToUnicode")] HRESULT ToUnicode(
  [in]          BSTR bstrString,
  [in]          Long lCodePage,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*bstrString* \[in\]  
変換対象の呼び出し元が指定した文字列。

*lCodePage* \[in\]  
変換に使用する呼び出し元が指定のコード ページ。 詳細については、「解説」を参照してください。

*pVal* \[out, retval\]  
変換された Unicode 文字列を受け取る場所への呼び出し元が指定のポインター。

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

<a name="remarks"></a>注釈
-------

設定、 *lCodePage*に対して定義されているコード ページ識別子のいずれかのパラメーター、*コードページ*のパラメーター、 **MultiByteToWideChar**関数。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

ほとんどのアプリケーションでは、今すぐデータの文字エンコーディングを Unicode (utf-16) を使用して、いくつかの Windows デスクトップ アプリケーションは、Windows コード ページに基づいて文字セットを使用します。 コード ページは、国際文字を ANSI 文字のコードが 127 より大きい値に割り当てます。 コード ページに関する詳細については、Windows SDK のドキュメントを参照してください。

該当する場合、日本語のコード ページを使用して Unicode に変換します。

```vb
If strLang = "JP" Then
    tmpStr = OleCvt.ToUnicode (str, 932)
Else
    tmpStr = str
End If
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

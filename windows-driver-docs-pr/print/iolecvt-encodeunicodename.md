---
title: IOleCvt EncodeUnicodeName メソッド
description: EncodeUnicodeName プロパティは、等価の Unicode を ANSI 文字列を変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_e31e8dae-76bb-4250-9d16-090a987c0dbf.xml
- print.iolecvt\_encodeunicodename
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 326a9374-7ed5-4521-999a-2c4c59faa617
keywords:
- 印刷デバイスの EncodeUnicodeName メソッド
- EncodeUnicodeName メソッド、印刷デバイス IOleCvt インターフェイス
- IOleCvt インターフェイス、印刷デバイス EncodeUnicodeName メソッド
topic_type:
- apiref
api_name:
- IOleCvt.EncodeUnicodeName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cca05c967042ef8a32b7c837badd59f4db6bebb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528522"
---
# <a name="iolecvtencodeunicodename-method"></a>IOleCvt::EncodeUnicodeName メソッド

**EncodeUnicodeName**プロパティを等価の Unicode、ANSI 文字列を変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
[propget, id(2), helpstring("property EncodeUnicodeName")] HRESULT EncodeUnicodeName(
  [in]          BSTR bstrSrcName,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*bstrSrcName* \[in\]  
呼び出し元が指定を変換する文字列を ANSI です。

*pVal* \[out, retval\]  
呼び出し元は、翻訳された文字列を受け取る場所へのポインターを指定します。

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
<td><strong>S_OK を返します</strong></td>
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
strMyUrl = "MyPage.asp?MyVariable=" & 
            OleCvt.EncodeUnicodeName("My&Unicode&Parameter")
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

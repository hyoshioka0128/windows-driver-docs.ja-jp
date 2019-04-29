---
title: IOleCvt ToUtf8 メソッド
description: ToUtf8 プロパティは、utf-8 形式に Unicode 文字の文字列を変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_b88265bd-9013-4c9b-abe2-00010d5b43c3.xml
- print.iolecvt\_toutf8
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1c20041f-b05d-4158-8838-650d25118c65
keywords:
- 印刷デバイスの ToUtf8 メソッド
- ToUtf8 メソッド、印刷デバイス IOleCvt インターフェイス
- IOleCvt インターフェイス、印刷デバイス ToUtf8 メソッド
topic_type:
- apiref
api_name:
- IOleCvt.ToUtf8
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ec2ff373d5e825d357314657cc37d99a76a2c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324815"
---
# <a name="iolecvttoutf8-method"></a>IOleCvt::ToUtf8 メソッド

**ToUtf8**プロパティは、utf-8 形式に Unicode 文字の文字列を変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
[propget, id(1), helpstring("property ToUtf8")] HRESULT ToUtf8(
  [in]          BSTR bstrUnicode,
  [out, retval] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*bstrUnicode* \[in\]  
Utf-8 形式に変換する呼び出し元が指定した文字列。

*pVal* \[out, retval\]  
呼び出し元は、変換後の文字列を受け取る場所へのポインターを指定します。

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

Utf-8 では、UCS (Universal Multibyte Octet-Coded 文字セット) の文字のすべての代替のコード化された表現形式です。 テキスト データは、0x00 から 0x7f までの範囲内の個々 のオクテットが ISO/IEC 4873、C0 一連の ISO/IEC 2022 の 8 ビットの構造に従ってコントロール関数を含むに従って定義を持つことを前提としている通信システム経由で送信するために使用します。

次の例では、次のように機能します。**書き込み**utf-8 形式に変換された文字列を返します。 提供するグローバル変数`bUTF8`は**TRUE**します。 それ以外の場合**書き込み**変更されていない文字列を返します。

```vb
Function Write (strUnicode)
    If bUTF8 Then
        Write = OleCvt.ToUtf8 (strUnicode)
    Else
        Write = strUnicode
    End If
End Function
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

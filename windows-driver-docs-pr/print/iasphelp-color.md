---
title: Iasphelp get\_色メソッド
description: 色のプロパティは、プリンターがカラー印刷をサポートしているかを判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_1eb57c03-7aa3-4acb-8a2c-3327a37e019d.xml
- print.iasphelp\_color
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: aa075ce7-15fd-4c24-b704-b7b240414d05
keywords:
- 印刷デバイスの get_Color メソッド
- get_Color メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_Color メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_Color
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1829772e2828e6289eca3b3e8fa2edfcd9a1a18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550167"
---
# <a name="iasphelpgetcolor-method"></a>Iasphelp::get\_色メソッド

**色**プロパティは、プリンターがカラー印刷をサポートしているかを判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_Color(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
受信場所へのポインターの呼び出し元が指定**TRUE**プリンターがカラー印刷をサポートしている場合または**FALSE**そうでない場合。

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
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::Color**プロパティのクエリを実行できます。

```vb
Dim objPrinter, HasColor
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
HasColor = objPrinter.Color
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

---
title: Iasphelp get\_MaximumResolution メソッド
description: MaximumResolution プロパティは、プリンターの最大解像度を判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_156e8337-489a-44e6-9c81-0a8f6dd3aa08.xml
- print.iasphelp\_maximumresolution
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 74dffe85-0e6d-4c2c-a933-2afb68624c76
keywords:
- 印刷デバイスの get_MaximumResolution メソッド
- get_MaximumResolution メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_MaximumResolution メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_MaximumResolution
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c9d90063a67bbbc9003780781ad6af5b6108f31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537275"
---
# <a name="iasphelpgetmaximumresolution-method"></a>Iasphelp::get\_MaximumResolution メソッド

**MaximumResolution**プロパティは、プリンターの最大解像度を判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_MaximumResolution(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
プリンターの最大解像度、インチあたりのドットで表す数値の値を受け取る呼び出し元が指定した場所。

<a name="return-value"></a>戻り値
------------

このプロパティは、次の表に、値のいずれかを返します。

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

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::MaximumResolution**プロパティのクエリを実行できます。

```vb
Dim objPrinter, MaxRes
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
MaxRes = objPrinter.MaximumResolution
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

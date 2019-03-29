---
title: Iasphelp get\_PageRate メソッド
description: PageRate プロパティは、プリンターのページの割合を決定する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_f356953e-ac15-4948-9a6e-b83d3aec8e7b.xml
- print.iasphelp\_pagerate
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 010f4871-f64f-465f-a78b-a86f91a9f194
keywords:
- 印刷デバイスの get_PageRate メソッド
- get_PageRate メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_PageRate メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_PageRate
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3bff7d93b6a3d3ddea2f937fbd4f0f39fd2efb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572690"
---
# <a name="iasphelpgetpagerate-method"></a>Iasphelp::get\_PageRate メソッド

**PageRate**プロパティは、プリンターのページの割合を決定する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_PageRate(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
プリンターのページの割合を表す数値を受信する呼び出し元が指定の場所。 ページの割合を表す単位、プリンターに依存します。 ページの料金の詳細については、次の「解説」を参照してください。

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
<td><strong>S_OK</strong></td>
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


ページの割合を測定する単位を確認するのには、クエリ、 [ **Iasphelp::PageRateUnit** ](iasphelp-pagerateunit.md)プロパティ。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::PageRate**プロパティのクエリを実行できます。

```vb
Dim objPrinter, PtrPageRate
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrPageRate = objPrinter.PageRate
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

## <a name="see-also"></a>関連項目

[**Iasphelp::PageRateUnit**](iasphelp-pagerateunit.md)

[**Iasphelp::Open**](iasphelp-open.md)

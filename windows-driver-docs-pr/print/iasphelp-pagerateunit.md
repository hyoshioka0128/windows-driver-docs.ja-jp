---
title: Iasphelp get\_PageRateUnit メソッド
description: PageRateUnit のページの割合を表す単位を決定する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_c3c557fb-2ce9-4260-838a-4bd0e56fb63d.xml
- print.iasphelp\_pagerateunit
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1b528527-a03a-4fab-b118-5c744759a0a1
keywords:
- 印刷デバイスの get_PageRateUnit メソッド
- get_PageRateUnit メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_PageRateUnit メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_PageRateUnit
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acbf199ce49bb180b2640134d7e8f09c46be1fab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560310"
---
# <a name="iasphelpgetpagerateunit-method"></a>Iasphelp::get\_PageRateUnit メソッド

**PageRateUnit**のページの割合を表す単位を決定する ASP Web ページを使用します。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_PageRateUnit(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
ページの割合で使用される単位を示す値を受け取るメモリ位置への呼び出し元が指定のポインター。 4 つの値は、次の表に表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>印刷速度単位は、1 分あたりのページです。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>印刷速度単位には、1 秒あたりの文字です。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>印刷速度の単位は、1 分あたりの行数です。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>印刷速度の単位は、1 分あたりインチです。</p></td>
</tr>
</tbody>
</table>

これらの値が定数 PRINTRATEUNIT 対応\_PPM、PRINTRATEUNIT\_CPS、PRINTRATEUNIT\_LPM、および PRINTRATEUNIT\_IPM、Wingdi.h ヘッダー ファイルで定義されています。 これらの定数の詳細については、の説明を参照して、 **DeviceCapabilities** Windows SDK のドキュメント内の関数。

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

単位を決定するには、このプロパティを照会、 [ **Iasphelp::PageRate** ](iasphelp-pagerate.md)プロパティの値が表されます。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::PageRateUnit**プロパティのクエリを実行できます。

```vb
Dim objPrinter, PtrPageRateUnit
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrPageRate = objPrinter.PageRateUnit
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

[**Iasphelp::PageRate**](iasphelp-pagerate.md)

[**Iasphelp::Open**](iasphelp-open.md)

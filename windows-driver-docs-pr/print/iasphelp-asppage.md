---
title: Iasphelp get\_AspPage メソッド
description: AspPage プロパティは、プリンターに固有の詳細を記述するために使用される初期の ASP ファイルのディレクトリ パスを取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_6b636ee3-bc4f-4fbd-8ad9-87d6abcf3b35.xml
- print.iasphelp\_asppage
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 325c0666-b4c4-48b5-b14f-bdb81e1ee5d2
keywords:
- 印刷デバイスの get_AspPage メソッド
- get_AspPage メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_AspPage メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_AspPage
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f40d9320c8ac462432598094e3e77979ca5afced
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574417"
---
# <a name="iasphelpgetasppage-method"></a>Iasphelp::get\_AspPage メソッド


**AspPage**プロパティがプリンター固有の詳細を記述するために使用される初期の ASP ファイルのディレクトリ パスを取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_AspPage(
  [in]  DWORD dwPage,
  [out] BSTR  *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*dwPage* \[in\]  
1 にする必要があります。

*pVal* \[out\]  
プリンター固有の詳細を記述する最初の Web ページへのディレクトリ パスを指定するサイズ プレフィックス付きの Unicode 文字列を受け取る場所への呼び出し元が指定のポインター。

<a name="return-value"></a>戻り値
------------

このメソッドは、これらの値のいずれかを返すことができます。

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
<td><strong>E_NOTIMPL</strong></td>
<td><p>ASP ファイルは使用できません。</p></td>
</tr>
<tr class="even">
<td><strong>E_POINTER</strong></td>
<td><p>無効な<em>pVal</em>ポインター。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

メソッドをページの ASP ファイルを検索する場所を確認するで説明されているアルゴリズムを使用して[するプリンターの詳細ページが表示されますか?](https://docs.microsoft.com/windows-hardware/drivers/print/which-printer-details-page-is-displayed-)します。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::AspPage**プロパティのクエリを実行できます。

```vb
    Dim objPrinter, strPrinter, str
    strPrinter = Session("MS_printer")
    Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
    objPrinter.Open strPrinter
    str = objPrinter.ASPPage(1)
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

[**Iasphelp::Open**](iasphelp-open.md)

---
title: Iasphelp get\_DriverName メソッド
description: ドライバー名プロパティは、プリンター ドライバーの名前を取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_99826bd3-a4fb-41b4-9f05-10598c4fcc01.xml
- print.iasphelp\_drivername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 656c8d36-23c0-46ae-81fd-a1123d5ab068
keywords:
- 印刷デバイスの get_DriverName メソッド
- get_DriverName メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_DriverName メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_DriverName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28776d64f6c6e405c5535d6e6f662571c8f8bccb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573793"
---
# <a name="iasphelpgetdrivername-method"></a>Iasphelp::get\_DriverName メソッド

**DriverName**プロパティは、プリンター ドライバーの名前を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_DriverName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
ドライバー名文字列へのポインターを受け取る場所への呼び出し元が指定のポインター。

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
<td><strong>S_OK</strong></td>
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

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::DriverName**プロパティのクエリを実行できます。

```vb
Dim objPrinter, DrvrName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
DrvrName = objPrinter.DriverName
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

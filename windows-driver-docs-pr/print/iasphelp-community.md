---
title: Iasphelp get\_コミュニティ メソッド
description: コミュニティのプロパティは、プリント サーバーの簡易ネットワーク管理プロトコル (SNMP) のコミュニティ名を取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_1d85e932-6de7-468a-b1dd-8a5678c65615.xml
- print.iasphelp\_community
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 39e8dff6-9eaf-43dd-b8ca-46982f3eae18
keywords:
- 印刷デバイスの get_Community メソッド
- get_Community メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_Community メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_Community
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf5783315979561f9d4a097f4580dde8f3dfa94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392869"
---
# <a name="iasphelpgetcommunity-method"></a>Iasphelp::get\_コミュニティ メソッド

**コミュニティ**プロパティは、プリント サーバーの簡易ネットワーク管理プロトコル (SNMP) のコミュニティ名を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_Community(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
コミュニティ名の文字列へのポインターを受信する場所への呼び出し元が指定のポインター。

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
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

プリンターが TCP/IP ポート モニタによってサポートされていない場合、返される文字列が空です。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::Community**プロパティのクエリを実行できます。

```vb
Dim objPrinter, CommName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
CommName = objPrinter.Community
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

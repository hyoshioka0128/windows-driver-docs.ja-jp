---
title: ISNMP GetList メソッド
description: GetList メソッドでは、SNMP Oid の配列に関連付けられている値を取得する ASP Web ページを使用します。
MS-HAID:
- webfnc\_44ada708-01e2-42c3-8080-bd7cf0e46b0e.xml
- print.isnmp\_getlist
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 6ee90c77-578e-4c2c-b955-4b549625ca14
keywords:
- 印刷デバイスの GetList メソッド
- GetList メソッド、印刷デバイス ISNMP インターフェイス
- ISNMP インターフェイス印刷デバイス、GetList メソッド
topic_type:
- apiref
api_name:
- ISNMP.GetList
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0005ceda8efe8fa4fa8d47c2b2e80a0395c0ed7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537846"
---
# <a name="isnmpgetlist-method"></a>ISNMP::GetList メソッド

`GetList`メソッドは、SNMP Oid の配列に関連付けられている値を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT GetList(
  [in]  VARIANT *varList,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>パラメーター
----------

*varList* \[in\]  
SNMP の OID の文字列の配列への呼び出し元が指定のポインター。

*varValue* \[out\]  
SNMP の OID 値の配列のアドレスを受け取る場所への呼び出し元が指定のポインター。

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
<td><strong>E_FAIL</strong></td>
<td><p><strong>ISNMP::Open</strong>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_INVALIDARG</strong></td>
<td><p>指定された SNMP OID が無効です。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrRequest** SNMP OID 値を取得します。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

[ **ISNMP::Open** ](isnmp-open.md)メソッドは、前に呼び出す必要があります、`ISNMP::GetList`メソッドを呼び出すことができます。

```vb
Dim StrIP, strCommunity, objSNMP, OIDArray, OIDValueArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDArray = Array("25.3.2.1.5", "25.3.5.1.1")
OIDValueArray = objSNMP.GetList (OIDArray)
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
<tr class="odd">
<td><p>Header</p></td>
<td>Olesnmp.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**ISNMP::Open**](isnmp-open.md)

---
title: ISNMP Set メソッド
description: Set メソッドには、ASP Web ページ、SNMP OID と値を関連付けることができます。
MS-HAID:
- webfnc\_b0392f7d-7d17-41ce-97fe-8f8baa691c78.xml
- print.isnmp\_set
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 7eac82e7-3f19-4eda-8706-eac6aa2b8dae
keywords:
- 印刷デバイスの set メソッド
- メソッド、印刷デバイス ISNMP インターフェイスを設定します。
- ISNMP インターフェイス印刷デバイス、Set メソッド
topic_type:
- apiref
api_name:
- ISNMP.Set
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d1bd97050f50ef5169bab0e77c119f8a69dc3ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384173"
---
# <a name="isnmpset-method"></a>ISNMP::Set メソッド

`Set`メソッドは、SNMP OID と値を関連付ける ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT Set(
  [in]  BSTR    bstrOID,
  [out] VARIANT varValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrOID* \[で\]  
SNMP の OID の文字列に呼び出し元が指定のポインター。

*varValue* \[out\]  
OID の値を格納している呼び出し元が指定の場所です。

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
<td><strong>E_FAIL</strong></td>
<td><p><strong>ISNMP::Open</strong>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_INVALIDARG</strong></td>
<td><p>指定された SNMP OID が無効です。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrRequest** SNMP OID 値を設定する関数。 詳細については、Windows SDK のドキュメントを参照してください。

[ **ISNMP::Open** ](isnmp-open.md)メソッドは、前に呼び出す必要があります、`ISNMP::Set`メソッドを呼び出すことができます。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValue
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
...
' Determine value to assign to OID; store it in OIDValue.
...
objSNMP.Set ("43.18.1.1.2", OIDValue)
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

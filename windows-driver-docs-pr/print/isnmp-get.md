---
title: ISNMP Get メソッド
description: Get メソッドでは、SNMP OID で識別される値を取得する ASP Web ページを使用します。
MS-HAID:
- webfnc\_e3167766-cd60-4ae7-9c06-9a1ccb5ac3b9.xml
- print.isnmp\_get
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 0cecdc34-63d9-46da-ba4e-a44780f5bb25
keywords:
- 印刷デバイス メソッドを取得します。
- メソッドの印刷デバイス、ISNMP インターフェイスを取得します。
- ISNMP インターフェイス印刷デバイス、Get メソッド
topic_type:
- apiref
api_name:
- ISNMP.Get
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e938b7782787e61f2b741848e54a00da6e0a1892
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384192"
---
# <a name="isnmpget-method"></a>ISNMP::Get メソッド

`Get`メソッドは、SNMP OID で識別される値を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT Get(
  [in]  BSTR    bstrOID,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrOID* \[で\]  
OID の文字列に呼び出し元が指定のポインター。

*varValue* \[out\]  
OID の値を受け取る呼び出し元が指定した場所。

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
<td><p>指定した OID が無効です。</p></td>
</tr>
<tr class="even">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrRequest** OID 値を取得します。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

[ **ISNMP::Open** ](isnmp-open.md)メソッドは、前に呼び出す必要があります、`ISNMP::Get`メソッドを呼び出すことができます。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValue
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDValue = objSNMP.Get ("43.18.1.1.2")
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

---
title: ISNMP OIDFromString メソッド
description: OIDFromString メソッドでは、SNMP OID の文字列を数値配列に変換する ASP Web ページを使用します。
MS-HAID:
- webfnc\_de08026f-5b6b-4c82-a653-2e16606e6b85.xml
- print.isnmp\_oidfromstring
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: a0e12657-c34e-4aff-a068-911a6aa6959d
keywords:
- 印刷デバイスの OIDFromString メソッド
- OIDFromString メソッド、印刷デバイス ISNMP インターフェイス
- ISNMP インターフェイス、印刷デバイス OIDFromString メソッド
topic_type:
- apiref
api_name:
- ISNMP.OIDFromString
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1458d9820f7bc2766c8f07f74b982d1b5d6a6fa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532670"
---
# <a name="isnmpoidfromstring-method"></a>ISNMP::OIDFromString メソッド

`OIDFromString`メソッドは、SNMP OID の文字列を数値配列に変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT OIDFromString(
  [in]  BSTR    bstrOID,
  [out] VARIANT *varOID
);
```

<a name="parameters"></a>パラメーター
----------

*bstrOID* \[で\]  
SNMP の OID の文字列に呼び出し元が指定のポインター。

*varOID* \[out\]  
SNMP の OID を表す整数値の配列へのポインターを受け取る呼び出し元が指定の場所。

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
<td><strong>E_INVALIDARG</strong></td>
<td><p>指定された SNMP OID が無効です。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrStrToOid** SNMP OID の文字列を対応するオブジェクト識別子の内部構造に変換する関数。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

```vb
Dim StrIP, strCommunity, objSNMP, OIDArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDArray = objSNMP.OIDFromString (". 43.18.1.1.2")
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

---
title: ISNMP GetTree メソッド
description: GetTree メソッドでは、SNMP OID の指定したルートの下にサブノードのセットに関連付けられている値を取得する ASP Web ページを使用します。
MS-HAID:
- webfnc\_bb1a8a21-716c-41ab-8b88-5f26d19575fa.xml
- print.isnmp\_gettree
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: a58cc911-dc09-4847-b4b7-cf97326cd444
keywords:
- 印刷デバイスの GetTree メソッド
- GetTree メソッド、印刷デバイス ISNMP インターフェイス
- ISNMP インターフェイス、印刷デバイス GetTree メソッド
topic_type:
- apiref
api_name:
- ISNMP.GetTree
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 902fb78760f48d5f928495146f776caf90acef7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384184"
---
# <a name="isnmpgettree-method"></a>ISNMP::GetTree メソッド

`GetTree`メソッドは、SNMP OID の指定したルートの下にサブノードのセットに関連付けられている値を取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT GetTree(
  [in]  BSTR    varTree,
  [out] VARIANT *varValue
);
```

<a name="parameters"></a>パラメーター
----------

*varTree* \[in\]  
SNMP OID ルートを識別する、呼び出し元が指定の文字列。

*varValue* \[out\]  
SNMP の OID の文字列と関連付けられている値を含む 2 次元配列のアドレスを受け取る呼び出し元が指定の場所。

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

このメソッドは、 **SnmpMgrRequest** SNMP OID にサブノードの値を取得します。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

[ **ISNMP::Open** ](isnmp-open.md)メソッドは、前に呼び出す必要があります、`ISNMP::GetTree`メソッドを呼び出すことができます。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValueArray
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDValueArray = objSNMP.GetTree ("43.18.1.1.2")
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
<tr class="odd">
<td><p>Header</p></td>
<td>Olesnmp.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**ISNMP::Open**](isnmp-open.md)

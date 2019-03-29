---
title: ISNMP GetAsByte メソッド
description: GetAsByte メソッドでは、SNMP OID で識別される値を取得して、値を符号なし整数に変換するために、ASP Web ページを使用します。
MS-HAID:
- webfnc\_915155f7-8444-4824-88be-808f10a9ff8e.xml
- print.isnmp\_getasbyte
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 0a9d170d-486f-49e9-a8f9-c0d8b17f681b
keywords:
- 印刷デバイスの GetAsByte メソッド
- GetAsByte メソッド、印刷デバイス ISNMP インターフェイス
- ISNMP インターフェイス、印刷デバイス GetAsByte メソッド
topic_type:
- apiref
api_name:
- ISNMP.GetAsByte
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2daf9bf51c6ec3f814aa188616d26538f583e493
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570533"
---
# <a name="isnmpgetasbyte-method"></a>ISNMP::GetAsByte メソッド

`GetAsByte`メソッドは、SNMP OID で識別される値を取得して、値を符号なし整数に変換するために、ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT GetAsByte(
  [in]  BSTR  bstrOID,
  [out] PUINT puValue
);
```

<a name="parameters"></a>パラメーター
----------

*bstrOID* \[で\]  
呼び出し元が指定 BSTR 値を SNMP OID が含まれています。

*puValue* \[out\]  
符号なし整数値を受け取る場所への呼び出し元が指定のポインター。

<a name="return-value"></a>戻り値
------------

このメソッドは、次の表に、値のいずれかを返します。

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
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrRequest** SNMP OID で識別される値を取得します。 メソッドでは、呼び出し元に値が渡される、前に、呼び出し元が符号なし整数に変換します。 詳細については**SnmpMgrRequest**、Windows SDK のマニュアルを参照してください。

次のデータ型の`ISNMP::GetAsByte`メソッドが、呼び出し元が受け取る等価符号なし整数値をする SNMP OID で識別されるスカラー値に変換します。

-   ASN\_整数

-   ASN\_RFC1155\_カウンター

-   ASN\_RFC1155\_ゲージ

-   ASN\_RFC1155\_TIMETICKS

-   ASN\_UNSIGNED32

次のデータ型の SNMP OID で識別される値のサイズが 2 つのバイトを超えない場合、メソッド、文字列、配列、または非透過の値の先頭の要素にパック、呼び出し元が受け取る符号なし整数値。

-   ASN\_ビット

-   ASN\_OCTETSTRING

-   ASN\_RFC1155\_OPAQUE

-   ASN\_シーケンス

メソッドは、上記のリストにないデータ型からの変換を現在サポートしていません。 これらのデータ型の詳細については、Windows SDK のドキュメントで、SNMP 管理 API の説明を参照してください。

[ **ISNMP::Open** ](isnmp-open.md)メソッドは、前に呼び出す必要があります、`ISNMP::GetAsByte`メソッドを呼び出すことができます。

```vb
Dim StrIP, strCommunity, objSNMP, OIDValue
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
OIDValue = objSNMP.GetAsByte ("25.3.5.1.2")
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

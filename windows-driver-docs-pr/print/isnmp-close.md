---
title: ISNMP Close メソッド
description: Close メソッドにより、ASP Web ページを SNMP エージェントへの通信パスを閉じます。
MS-HAID:
- webfnc\_e925ae51-c717-4b4f-8ab2-b18e9d770c63.xml
- print.isnmp\_close
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ea3c462d-881d-48ad-8751-d3ee0468697e
keywords:
- 印刷デバイスの close メソッド
- Close メソッド、印刷デバイス ISNMP インターフェイス
- ISNMP インターフェイス印刷デバイス、Close メソッド
topic_type:
- apiref
api_name:
- ISNMP.Close
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19d980f4b1d98cc90c17f5e179e5ea42e625e804
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528303"
---
# <a name="isnmpclose-method"></a>ISNMP::Close メソッド

`Close`メソッドは、SNMP エージェントへの通信パスを閉じる ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT Close();
```

<a name="parameters"></a>パラメーター
----------

このメソッドにはパラメーターはありません。

<a name="return-value"></a>戻り値
------------

メソッド常に返します S\_ok をクリックします。

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrClose**関数は、Windows SDK ドキュメントでは、以前の呼び出しによって作成された通信パスを閉じるには説明されている、 [ **ISNMP::Open**](isnmp-open.md)メソッド。

```vb
Dim StrIP, strCommunity, objSNMP
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
...
objSNMP.Close
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

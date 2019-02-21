---
title: ISNMP Open メソッド
description: Open メソッドは、ASP Web ページを指定した SNMP エージェントへの通信パスを作成できます。
MS-HAID:
- webfnc\_2be497fa-98d8-4fb3-997c-fa1345ed4648.xml
- print.isnmp\_open
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: a5d1a8a2-5953-4b7f-8f8e-cb84520ae9e8
keywords:
- 印刷デバイスの open メソッド
- Open メソッド、印刷デバイス ISNMP インターフェイス
- ISNMP インターフェイス印刷デバイス、Open メソッド
topic_type:
- apiref
api_name:
- ISNMP.Open
api_location:
- olesnmp.h
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f5975b57e19f5dda2cb96ffe5788b1e9d14835
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538631"
---
# <a name="isnmpopen-method"></a>ISNMP::Open メソッド

`Open`メソッドは、指定した SNMP エージェントへの通信パスを作成する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT Open(
  [in] BSTR    bstrHost,
  [in] BSTR    bstrCommunity,
  [in] VARIANT varRetry,
  [in] VARIANT varTimeout
);
```

<a name="parameters"></a>パラメーター
----------

*bstrHost* \[in\]  
SNMP エージェントのシステムを識別する文字列への呼び出し元が指定のポインター。 ドット区切り 10 進数の IP アドレスまたは IP アドレス、8.12 表記で、IPX アドレスまたはイーサネット アドレスに解決されるホスト名のいずれかを指定できます。

*bstrCommunity* \[で\]  
SNMP エージェント システムのコミュニティ名を表す文字列への呼び出し元が指定のポインター。

*varRetry* \[in\]  
省略可能な呼び出し元が指定の再試行の値。 指定されていない場合は、既定値が使用されます。 推奨値は、2 です。

*varTimeout* \[in\]  
省略可能な呼び出し元が指定のタイムアウト値 (ミリ秒)。 指定されていない場合は、既定値が使用されます。 推奨値は、1000 です。

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
<td><p>いずれか、 <em>varRetry</em>または<em>varTimeOut</em>を短整数値を変換できませんでした。</p></td>
</tr>
<tr class="odd">
<td><strong>E_FAIL</strong></td>
<td><p>呼び出し<strong>SnmpMgrOpen</strong>できませんでした。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、 **SnmpMgrOpen** 、同じパラメーターを持つ関数として`ISNMP::Open`します。 この関数の詳細については、Windows SDK のドキュメントを参照してください。

後に、`ISNMP::Open`呼び出し、SNMP エージェントへの通信パスはされるまで開いたまま、 [ **ISNMP::Close** ](isnmp-close.md)メソッドが呼び出されるまで、または`ISNMP::Open`が再度呼び出されます。

```vb
Dim StrIP, strCommunity, objSNMP
strIP = Session("MS_IPaddress")
strCommunity = Session ("MS_Community")
Set objSNMP = Server.CreateObject("OlePrn.OleSNMP")
objSNMP.Open strIP, strCommunity, 2, 1000
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

[**ISNMP::Close**](isnmp-close.md)

---
title: Iasphelp get\_MibErrorDscp メソッド
description: MibErrorDscp プロパティは、簡易ネットワーク管理プロトコル (SNMP) 管理情報ベース (MIB) エラー コード、エラーの説明テキストに変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_3931fbc6-1960-4d40-a6e3-8816ee832c89.xml
- print.iasphelp\_miberrordscp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: b2ab9414-8401-4ec4-a235-f6a8da93523b
keywords:
- 印刷デバイスの get_MibErrorDscp メソッド
- get_MibErrorDscp メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_MibErrorDscp メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_MibErrorDscp
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6acc8a6a5d9e39e823dcee7d687e7ac56bbc5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549505"
---
# <a name="iasphelpgetmiberrordscp-method"></a>Iasphelp::get\_MibErrorDscp メソッド

**MibErrorDscp**プロパティは、簡易ネットワーク管理プロトコル (SNMP) 管理情報ベース (MIB) エラー コード、エラーの説明テキストに変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_MibErrorDscp(
  [in]  DWORD dwError,
  [out] BSTR  *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*dwError* \[in\]  
呼び出し元が指定した SNMP MIB エラー コード。

*pVal* \[out\]  
エラーの説明テキストを含む文字列へのポインターを受け取る呼び出し元が指定した場所。

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
<td><strong>E_POINTER</strong></td>
<td><p>無効な<em>pVal</em>ポインター。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

```vb
Dim objPrinter, MIBErrorCode, MIBErrorString
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
...
' Get error code from MIB.
...
MIBErrorString = objPrinter.MibErrorDscp(ErrorCodeMIB)
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

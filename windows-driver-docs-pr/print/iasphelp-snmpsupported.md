---
title: Iasphelp get\_SNMPSupported メソッド
description: SNMPSupported プロパティは、プリンターの SNMP を使用しているかを判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_2128dc9d-a113-4061-a6c9-3ebe2a304dd5.xml
- print.iasphelp\_snmpsupported
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 17e3986b-3eb6-4c9d-ae4f-338e9cce439a
keywords:
- 印刷デバイスの get_SNMPSupported メソッド
- get_SNMPSupported メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_SNMPSupported メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_SNMPSupported
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8991703d7aed966333bf2dd15d64901cd1f7b42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365520"
---
# <a name="iasphelpgetsnmpsupported-method"></a>Iasphelp::get\_SNMPSupported メソッド

**SNMPSupported**プロパティは、プリンターの SNMP を使用しているかを判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_SNMPSupported(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
受信場所へのポインターの呼び出し元が指定**TRUE** SNMP は、プリンターで使用されている場合または**FALSE**でない場合。

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

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::SNMPSupported**プロパティのクエリを実行できます。

```vb
Dim objPrinter, UsingSNMP
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
UsingSNMP = objPrinter.SNMPSupported
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
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**Iasphelp::Open**](iasphelp-open.md)

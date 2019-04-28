---
title: Iasphelp get\_SNMPDevice メソッド
description: SNMPDevice プロパティは、プリンターの SNMP デバイスのインデックスで定義された RFC 1759) を取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_e4a9d1b3-1168-45a7-98cb-9c19fdf83009.xml
- print.iasphelp\_snmpdevice
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 4ae42406-6a19-4af0-88c5-bc4375bb648c
keywords:
- 印刷デバイスの get_SNMPDevice メソッド
- get_SNMPDevice メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_SNMPDevice メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_SNMPDevice
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5eec7ac38d7a5dc782f2bc36c8d0019015c7c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365491"
---
# <a name="iasphelpgetsnmpdevice-method"></a>Iasphelp::get\_SNMPDevice メソッド

**SNMPDevice**プロパティ (RFC 1759 で定義) されたプリンターの SNMP デバイスのインデックスを取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_SNMPDevice(
  [out] DWORD *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
プリンターの SNMP デバイスのインデックスを表す数値の値を受け取る呼び出し元が指定した場所。

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

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::SNMPDevice**プロパティのクエリを実行できます。

```vb
Dim objPrinter, SNMPDeviceIndex
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
SNMPDeviceIndex = objPrinter.SNMPDevice
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

## <a name="see-also"></a>関連項目

[**Iasphelp::Open**](iasphelp-open.md)

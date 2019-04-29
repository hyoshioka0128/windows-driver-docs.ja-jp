---
title: Iasphelp get\_IPAddress メソッド
description: IPAddress プロパティは、プリンターの IP アドレスを取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_f0b5a4c6-50db-48a0-a10d-2a835cac32ac.xml
- print.iasphelp\_ipaddress
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 535ea9fa-fff7-47fd-84ae-f61526f1b622
keywords:
- 印刷デバイスの get_IPAddress メソッド
- get_IPAddress メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_IPAddress メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_IPAddress
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bf6125f58ca21bddae590c8a738daca1d50ff10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392880"
---
# <a name="iasphelpgetipaddress-method"></a>Iasphelp::get\_IPAddress メソッド

**IPAddress**プロパティは、プリンターの IP アドレスを取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_IPAddress(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
呼び出し元が指定した IP アドレス文字列へのポインターを受信する場所へのポインター。

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
<td><p><strong>Iasphelp::Open</strong>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::IPAddress**プロパティのクエリを実行できます。

プリンターが TCP/IP ポート モニタによってサポートされていない場合、返される文字列が空です。

```vb
Dim objPrinter, PrinterIP
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PrinterIP = objPrinter.IPAddress
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

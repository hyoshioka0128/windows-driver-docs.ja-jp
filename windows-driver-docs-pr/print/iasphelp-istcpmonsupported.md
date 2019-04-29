---
title: Iasphelp get\_IsTCPMonSupported メソッド
description: IsTCPMonSupported プロパティは、Microsoft の標準の TCP/IP ポート モニタは、プリンターで使用されているかを判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_54f72229-524a-4bf2-917d-6a3ffcc27959.xml
- print.iasphelp\_istcpmonsupported
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 79ec0584-183d-476d-aca2-e85479248091
keywords:
- 印刷デバイスの get_IsTCPMonSupported メソッド
- get_IsTCPMonSupported メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_IsTCPMonSupported メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_IsTCPMonSupported
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7d4a3958e062ce9501dd2d12b805cad6e6ad18a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392853"
---
# <a name="iasphelpgetistcpmonsupported-method"></a>Iasphelp::get\_IsTCPMonSupported メソッド

**IsTCPMonSupported**プロパティは、Microsoft の標準的なかどうかを判断する ASP Web ページを使用できます。 TCP/IP[ポート モニター](https://docs.microsoft.com/windows-hardware/drivers/print/port-monitors)プリンターで使用されています。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_IsTCPMonSupported(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
受信場所へのポインターの呼び出し元が指定**TRUE** 、プリンターに TCP/IP ポート モニターを使用している場合または**FALSE**でない場合。

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

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::IsTCPMonSupported**プロパティのクエリを実行できます。

```vb
Dim objPrinter, UseStdMon
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
UseStdMon = objPrinter.IsTCPMonSupported
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

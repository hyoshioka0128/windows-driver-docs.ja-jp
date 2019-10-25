---
title: Iasphelp\_MediaReady メソッドの取得
description: MediaReady プロパティを使用すると、ASP Web ページで、現在使用可能なプリンターのすべての用紙形式に名前を指定した一連の文字列を取得できます。
MS-HAID:
- webfnc\_b10e8434-7e12-4bb5-8c43-77cb890f72a8.xml
- print.iasphelp\_mediaready
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1e90649a-6075-4b78-93fd-781c3e363b5f
keywords:
- get_MediaReady メソッドの印刷デバイス
- get_MediaReady メソッドの印刷デバイス、Iasphelp インターフェイス
- Iasphelp インターフェイスの印刷デバイス、get_MediaReady メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_MediaReady
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99dd80c0fb7807f0d820d06f4f71734444653cff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838096"
---
# <a name="iasphelpget_mediaready-method"></a>Iasphelp:: get\_MediaReady メソッド

**Mediaready**プロパティを使用すると、ASP Web ページで、現在使用可能なプリンターのすべての用紙形式に名前を指定した一連の文字列を取得できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_MediaReady(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[\]  
現在使用可能なプリンターのすべての用紙形式に名前を指定した一連の文字列へのポインターを受け取る、呼び出し元が指定した場所。

<a name="return-value"></a>戻り値
------------

このプロパティは、次の表に示すいずれかの値を返します。

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
<td><p>操作は成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_HANDLE</strong></td>
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"><strong>Iasphelp:: Open</strong></a>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、DC\_MEDIAREADY フラグが設定された状態でプリンタードライバーの[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数を呼び出すことによって、現在使用可能な用紙の名前の一覧を取得します。

Iasphelp:: **MediaReady**プロパティを照会する前に、 [**Iasphelp:: Open**](iasphelp-open.md)メソッドを呼び出す必要があります。

```vb
Dim objPrinter, MediaReadyArray
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
MediaReadyArray = objPrinter.MediaReady
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

[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)

[**Iasphelp:: Open**](iasphelp-open.md)

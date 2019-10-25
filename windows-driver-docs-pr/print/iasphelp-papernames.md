---
title: Iasphelp\_の Pagenames メソッドの取得
description: "\"Paper Names\" プロパティを使用すると、ASP Web ページは、プリンターのすべての用紙形式に名前を指定した文字列のセットを取得できます。"
MS-HAID:
- webfnc\_be2b332f-6300-4b3e-9fa7-fd2fd0bdffe5.xml
- print.iasphelp\_papernames
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 558cf0a6-d98b-4d59-ae37-d19ced289bf0
keywords:
- get_PaperNames メソッドの印刷デバイス
- get_PaperNames メソッドの印刷デバイス、Iasphelp インターフェイス
- Iasphelp インターフェイスの印刷デバイス、get_PaperNames メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_PaperNames
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2188eadfb899378be54de358a2cee5dee388f1f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838093"
---
# <a name="iasphelpget_papernames-method"></a>Iasphelp:: get\_Pagenames メソッド

"Paper **names** " プロパティを使用すると、ASP Web ページは、プリンターのすべての用紙形式に名前を指定した文字列のセットを取得できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_PaperNames(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[\]  
プリンターのすべての用紙形式を表す文字列のセットへのポインターを受け取る、呼び出し元が指定した場所。

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

このプロパティのハンドラーは、DC\_paper NAMES フラグが設定されたプリンタードライバーの[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)関数を呼び出すことによって、用紙の種類の一覧を取得します。

Iasphelp: [ **: Open**](iasphelp-open.md)メソッドは、 **iasphelp::P apernames**プロパティを照会する前に呼び出す必要があります。

```vb
Dim objPrinter, PaperNameArray
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PaperNameArray = objPrinter.PaperNames
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

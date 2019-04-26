---
title: Iasphelp get\_PaperNames メソッド
description: PaperNames プロパティは、プリンターの用紙のすべてのフォームの名前を示す文字列のセットを取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_be2b332f-6300-4b3e-9fa7-fd2fd0bdffe5.xml
- print.iasphelp\_papernames
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 558cf0a6-d98b-4d59-ae37-d19ced289bf0
keywords:
- 印刷デバイスの get_PaperNames メソッド
- get_PaperNames メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_PaperNames メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_PaperNames
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3efc5f51ea2aad42977eb26e6da0354232e7225e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357234"
---
# <a name="iasphelpgetpapernames-method"></a>Iasphelp::get\_PaperNames メソッド

**PaperNames**プロパティは、プリンターの用紙のすべてのフォームの名前を示す文字列のセットを取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_PaperNames(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
プリンターのすべての紙のフォームを表す文字列のセットを指すポインターを受け取る呼び出し元が指定の場所。

<a name="return-value"></a>戻り値
------------

このプロパティは、次の表に、値のいずれかを返します。

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

このプロパティのハンドラーを呼び出して、プリンター ドライバーの紙のフォームの一覧を取得する[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities) DC で関数を\_PAPERNAMES フラグを設定します。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::PaperNames**プロパティのクエリを実行できます。

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

[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)

[**Iasphelp::Open**](iasphelp-open.md)

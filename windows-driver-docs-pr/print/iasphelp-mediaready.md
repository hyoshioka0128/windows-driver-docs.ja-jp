---
title: Iasphelp get\_MediaReady メソッド
description: MediaReady プロパティは、その名前が現在使用可能なプリンターのフォーム用紙のすべての一連の文字列を取得する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_b10e8434-7e12-4bb5-8c43-77cb890f72a8.xml
- print.iasphelp\_mediaready
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1e90649a-6075-4b78-93fd-781c3e363b5f
keywords:
- 印刷デバイスの get_MediaReady メソッド
- get_MediaReady メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_MediaReady メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_MediaReady
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a5a7721ffeda339468e553b1d055218b6694fe0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578465"
---
# <a name="iasphelpgetmediaready-method"></a>Iasphelp::get\_MediaReady メソッド

**MediaReady**プロパティは現在使用可能な紙のフォームのすべてをプリンターの名前を示す文字列のセットを取得する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_MediaReady(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
その名前が現在使用可能なプリンターのフォーム用紙のすべての文字列のセットへのポインターを受信する呼び出し元が指定の場所。

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
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このメソッドは、プリンター ドライバーを呼び出すことによって現在使用可能な紙のフォームの名前の一覧を取得します[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities) DC で関数を\_MEDIAREADY。フラグを設定します。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::MediaReady**プロパティのクエリを実行できます。

```vb
Dim objPrinter, MediaReadyArray
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
MediaReadyArray = objPrinter.MediaReady
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

[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)

[**Iasphelp::Open**](iasphelp-open.md)

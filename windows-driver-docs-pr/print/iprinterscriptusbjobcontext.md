---
title: Iプリンター Scriptusbjobcontext インターフェイス
description: Iプリンター Scriptusbjobcontext インターフェイスは、startPrintJob JavaScript 関数にパラメーターとして渡されます。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 236F6B00-39D8-4084-BAE0-C349AD550040
keywords:
- Iプリンター Scriptusbjobcontext インターフェイスの印刷デバイス
- Iプリンター Scriptusbjobcontext インターフェイスの印刷デバイス、説明
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0477bdc5096f06394f4131147bfca3fa47c25866
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837857"
---
# <a name="iprinterscriptusbjobcontext-interface"></a>Iプリンター Scriptusbjobcontext インターフェイス

Iプリンター Scriptusbjobcontext インターフェイスは、 **startPrintJob** JavaScript 関数にパラメーターとして渡されます。

<a name="members"></a>Members
-------

**Iプリンター Scriptusbjobcontext**インターフェイスは、 [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイスから継承されます。 **Iプリンター Scriptusbjobcontext**には、次の種類のメンバーもあります。

-   [メソッド](#methods)

### <a name="methods"></a>メソッド

**Iプリンター Scriptusbjobcontext**インターフェイスには、これらのメソッドがあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-jobpropertybag.md" data-raw-source="[&lt;strong&gt;JobPropertyBag&lt;/strong&gt;](iprinterscriptusbjobcontext-jobpropertybag.md)"><strong>JobPropertyBag</strong></a></td>
<td><p>現在の印刷ジョブに関連付けられているプロパティバッグを返します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-printedpagecount.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>現在のジョブの印刷デバイスによって印刷されたページ数を返します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-printedpagecount-in.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount-in.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>現在のジョブの印刷デバイスによって印刷されたページ数を設定します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-returncodes.md" data-raw-source="[&lt;strong&gt;ReturnCodes&lt;/strong&gt;](iprinterscriptusbjobcontext-returncodes.md)"><strong>ReturnCodes</strong></a></td>
<td><p>IHV が JavaScript 関数に対して定義したリターンコード値を指定できるオブジェクトを返します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-temporarystreams.md" data-raw-source="[&lt;strong&gt;TemporaryStreams&lt;/strong&gt;](iprinterscriptusbjobcontext-temporarystreams.md)"><strong>一時ストリーム</strong></a></td>
<td><p>現在のジョブの IHV JavaScript 関数で使用できる永続データストリームの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream" data-raw-source="[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)">IPrinterScriptableSequentialStream</a>インターフェイスの配列を返します。</p></td>
</tr>
</tbody>
</table>

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
</tbody>
</table>

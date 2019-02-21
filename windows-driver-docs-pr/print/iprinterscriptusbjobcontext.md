---
title: IPrinterScriptUsbJobContext インターフェイス
description: IPrinterScriptUsbJobContext インターフェイスは、startPrintJob JavaScript 関数にパラメーターとして渡されます。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 236F6B00-39D8-4084-BAE0-C349AD550040
keywords:
- IPrinterScriptUsbJobContext インターフェイス印刷デバイス
- IPrinterScriptUsbJobContext インターフェイス、印刷デバイスの説明
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f662d41a3ccfad4852054ec9b36d28fae2aed89b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529411"
---
# <a name="iprinterscriptusbjobcontext-interface"></a>IPrinterScriptUsbJobContext インターフェイス

IPrinterScriptUsbJobContext インターフェイスがパラメーターとして渡される、 **startPrintJob** JavaScript 関数。

<a name="members"></a>Members
-------

**IPrinterScriptUsbJobContext**インターフェイスから継承、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 **IPrinterScriptUsbJobContext**これらの種類のメンバーがあります。

-   [メソッド](#methods)

### <a name="methods"></a>メソッド

**IPrinterScriptUsbJobContext**インターフェイスがこれらのメソッド。

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
<td><p>現在の印刷ジョブに関連付けられたプロパティ バッグを返します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-printedpagecount.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>現在のジョブで印刷デバイスによって印刷されたページ数を返します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-printedpagecount-in.md" data-raw-source="[&lt;strong&gt;PrintedPageCount&lt;/strong&gt;](iprinterscriptusbjobcontext-printedpagecount-in.md)"><strong>PrintedPageCount</strong></a></td>
<td><p>現在のジョブで印刷デバイスによって印刷されたページ数を設定します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontext-returncodes.md" data-raw-source="[&lt;strong&gt;ReturnCodes&lt;/strong&gt;](iprinterscriptusbjobcontext-returncodes.md)"><strong>開始</strong></a></td>
<td><p>IHV は、JavaScript 関数の定義のリターン コード値を提供できるオブジェクトを返します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontext-temporarystreams.md" data-raw-source="[&lt;strong&gt;TemporaryStreams&lt;/strong&gt;](iprinterscriptusbjobcontext-temporarystreams.md)"><strong>TemporaryStreams</strong></a></td>
<td><p>配列を返します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream" data-raw-source="[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)">IPrinterScriptableSequentialStream</a>は現在のジョブ、IHV JavaScript 関数で使用できる永続的なデータ ストリームのインターフェイス。</p></td>
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

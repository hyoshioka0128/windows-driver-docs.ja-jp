---
title: IPrinterScriptUsbWritePrintDataProgress インターフェイス
description: IPrinterScriptUsbWritePrintDataProgress インターフェイスは、writePrintData JavaScript 関数の呼び出しでパラメーターとして渡されます。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: E22725DA-2BD5-4FBC-A3E4-A3C5678A9E57
keywords:
- IPrinterScriptUsbWritePrintDataProgress 印刷デバイスをインターフェイスします。
- IPrinterScriptUsbWritePrintDataProgress 記載されている印刷デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8330eb195ea94869a387d8939ba7c63fc9fdaa1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349208"
---
# <a name="iprinterscriptusbwriteprintdataprogress-interface"></a>IPrinterScriptUsbWritePrintDataProgress インターフェイス

IPrinterScriptUsbWritePrintDataProgress インターフェイスがパラメーターとして渡される、 **writePrintData** JavaScript 関数の呼び出し。

<a name="members"></a>メンバー
-------

**IPrinterScriptUsbWritePrintDataProgress**インターフェイスから継承、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 **IPrinterScriptUsbWritePrintDataProgress**これらの種類のメンバーがあります。

-   [メソッド](#methods)

### <a name="methods"></a>メソッド

**IPrinterScriptUsbWritePrintDataProgress**インターフェイスがこれらのメソッド。

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
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>IHV JavaScript 関数は、このメソッドが呼び出された時点で処理されたバイト数を返します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md" data-raw-source="[&lt;strong&gt;ProcessedByteCount&lt;/strong&gt;](iprinterscriptusbwriteprintdataprogress-processedbytecount-in.md)"><strong>ProcessedByteCount</strong></a></td>
<td><p>IHV JavaScript 関数は、このメソッドが呼び出された時に処理されたバイト数を設定します。</p></td>
</tr>
</tbody>
</table>

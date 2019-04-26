---
title: IPrinterScriptUsbJobContextReturnCodes インターフェイス
description: IPrinterScriptUsbJobContextReturnCodes インターフェイスは、IHV は、JavaScript 関数に対して定義されている戻り値の配列を表します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 8E34748E-B9F9-4404-9B40-04EA72EEA322
keywords:
- IPrinterScriptUsbJobContextReturnCodes 印刷デバイスをインターフェイスします。
- IPrinterScriptUsbJobContextReturnCodes 記載されている印刷デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09802d98945e348e23c02d4377f4b09b607c5a59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349200"
---
# <a name="iprinterscriptusbjobcontextreturncodes-interface"></a>IPrinterScriptUsbJobContextReturnCodes インターフェイス

IPrinterScriptUsbJobContextReturnCodes インターフェイスは、IHV は、JavaScript 関数に対して定義されている戻り値の配列を表します。

このインターフェイスは、によって返される、 [ **IPrinterScriptUsbJobContext::ReturnCodes** ](iprinterscriptusbjobcontext-returncodes.md)メソッド。

<a name="members"></a>メンバー
-------

**IPrinterScriptUsbJobContextReturnCodes**インターフェイスから継承、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 **IPrinterScriptUsbJobContextReturnCodes**これらの種類のメンバーがあります。

-   [メソッド](#methods)

### <a name="methods"></a>メソッド

**IPrinterScriptUsbJobContextReturnCodes**インターフェイスがこれらのメソッド。

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
<td><a href="iprinterscriptusbjobcontextreturncodes-abortthejob.md" data-raw-source="[&lt;strong&gt;AbortTheJob&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-abortthejob.md)"><strong>AbortTheJob</strong></a></td>
<td><p>印刷ジョブを中止する必要がある USBMon に通知するには、'4' の値を返します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontextreturncodes-devicebusy.md" data-raw-source="[&lt;strong&gt;DeviceBusy&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-devicebusy.md)"><strong>DeviceBusy</strong></a></td>
<td><p>デバイスの通信チャネルはこの時点でデータを受け付けていませんこと USBMon に通知するには、'3' の値を返します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-failure.md" data-raw-source="[&lt;strong&gt;Failure&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-failure.md)"><strong>エラー</strong></a></td>
<td><p>メソッドの呼び出しが失敗した USBMon に通知するには、'1' の値を返します。</p></td>
</tr>
<tr class="even">
<td><a href="iprinterscriptusbjobcontextreturncodes-retry.md" data-raw-source="[&lt;strong&gt;Retry&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-retry.md)"><strong>再試行</strong></a></td>
<td><p>USBMon メソッドの呼び出しより多くの作業が完了すると、成功したことを通知するには、'2' の値を返します。</p></td>
</tr>
<tr class="odd">
<td><a href="iprinterscriptusbjobcontextreturncodes-success.md" data-raw-source="[&lt;strong&gt;Success&lt;/strong&gt;](iprinterscriptusbjobcontextreturncodes-success.md)"><strong>成功</strong></a></td>
<td><p>関数呼び出しが正常に完了した USBMon を通知するためにゼロ (0) の値を返します。</p></td>
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

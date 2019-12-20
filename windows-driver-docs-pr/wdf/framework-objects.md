---
title: フレームワーク オブジェクト
description: フレームワーク オブジェクト
ms.assetid: bd9ec812-205d-4f9a-b85b-4e3a2f7556bd
keywords:
- UMDF オブジェクト WDK、一覧
- フレームワークオブジェクト WDK UMDF、一覧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f4102c03ac4697cb929a7511dc5164d4ef49d29
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210768"
---
# <a name="framework-objects"></a>フレームワーク オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次の表は、各フレームワークオブジェクトの基本情報、オブジェクトのインターフェイスへのリンク、およびコアフレームワークオブジェクトに関する詳細情報へのリンクを示しています。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Objectname</th>
<th align="left">ObjectInterface</th>
<th align="left">目的</th>
<th align="left">Defaultparent</th>
<th align="left">ドライバー overridedefaultparent を使用できますか。</th>
<th align="left">ドライバーは所有できますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="framework-driver-object.md" data-raw-source="[Driver object](framework-driver-object.md)">Driver オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver" data-raw-source="[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)">IWDFDriver</a></p></td>
<td align="left"><p>ドライバーを表します。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-device-object.md" data-raw-source="[Device object](framework-device-object.md)">デバイスオブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice" data-raw-source="[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)">IWDFDevice</a></p></td>
<td align="left"><p>デバイスを表します。</p></td>
<td align="left"><p>Driver オブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-file-object.md" data-raw-source="[File object](framework-file-object.md)">ファイルオブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td align="left"><p>ファイルを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p></p>
いいえ (フレームワークによって作成された場合)。はい (ドライバーによって作成された場合)</td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-interrupt-object.md" data-raw-source="[Interrupt object](framework-interrupt-object.md)">Interrupt オブジェクト</a></p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt" data-raw-source="[IWDFInterrupt](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt)">IWDFInterrupt</a></td>
<td align="left"><p>割り込みを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-queue-object.md" data-raw-source="[Queue object](framework-i-o-queue-object.md)">Queue オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue" data-raw-source="[IWDFIoQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue)">IWDFIoQueue</a></p></td>
<td align="left"><p>I/o 要求を受信する i/o キューを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-i-o-request-object.md" data-raw-source="[Request object](framework-i-o-request-object.md)">要求オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest" data-raw-source="[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)">IWDFIoRequest</a></p></td>
<td align="left"><p>I/o 要求を表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p></p>
いいえ (フレームワークによって作成された場合)。はい (ドライバーによって作成された場合)</td>
<td align="left"><p></p>
いいえ (リダイレクトされた要求など、フレームワークによって作成された場合)。はい (ドライバーによって作成された場合)</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-target-object.md" data-raw-source="[Target object](framework-i-o-target-object.md)">ターゲットオブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget" data-raw-source="[IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)">IWDFIoTarget</a></p></td>
<td align="left"><p>別のドライバーが要求を送信するドライバーを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p></p>
いいえ (既定のターゲットの場合)はい (他のすべてのターゲットについて)</td>
</tr>
<tr class="even">
<td align="left"><p>USB デバイスオブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice" data-raw-source="[IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)">IWDFUsbTargetDevice</a></p></td>
<td align="left"><p>USB に接続されているデバイスを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>はい (ターゲットオブジェクトを参照)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USB パイプオブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe" data-raw-source="[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)">IWDFUsbTargetPipe</a></p></td>
<td align="left"><p>USB デバイスパイプを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>はい (ターゲットオブジェクトを参照)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB インターフェイスオブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)">IWDFUsbInterface</a></p></td>
<td align="left"><p>USB デバイスインターフェイスを表します。</p></td>
<td align="left"><p>デバイスオブジェクト</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>はい (ターゲットオブジェクトを参照)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-base-object.md" data-raw-source="[Base object](framework-base-object.md)">基本オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject" data-raw-source="[IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)">IWDFObject</a></p></td>
<td align="left"><p>一般的な基本オブジェクトを表します。</p></td>
<td align="left"><p>Driver オブジェクト</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>はい (ドライバーによって作成された場合)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-memory-object.md" data-raw-source="[Memory object](framework-memory-object.md)">Memory オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[IWDFMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)">IWDFMemory</a></p></td>
<td align="left"><p>メモリオブジェクトを表します。</p></td>
<td align="left"><p>Driver オブジェクト</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p></p>
いいえ (フレームワークによって作成された場合)。はい (ドライバーによって作成された場合)</td>
</tr>
</tbody>
</table>

 

 

 






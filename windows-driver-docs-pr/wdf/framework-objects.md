---
title: フレームワーク オブジェクト
description: フレームワーク オブジェクト
ms.assetid: bd9ec812-205d-4f9a-b85b-4e3a2f7556bd
keywords:
- 一覧表示された WDK、UMDF オブジェクト
- 一覧表示されたフレームワーク オブジェクト WDK UMDF、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a80824e0662eb8d652acd84c97cdee8108a29bd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384451"
---
# <a name="framework-objects"></a>フレームワーク オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の表は、各フレームワーク オブジェクト、オブジェクトのインターフェイスへのリンクと core framework のオブジェクトに関する詳細情報へのリンクに関する基本情報を提供します。

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
<th align="left">ルオブジェクトインタ</th>
<th align="left">目的</th>
<th align="left">Defaultparent</th>
<th align="left">ドライバー overridedefaultparent ことができますか。</th>
<th align="left">自身がドライバーですか?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="framework-driver-object.md" data-raw-source="[Driver object](framework-driver-object.md)">ドライバー オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver" data-raw-source="[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)">IWDFDriver</a></p></td>
<td align="left"><p>ドライバーを表します</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-device-object.md" data-raw-source="[Device object](framework-device-object.md)">デバイス オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice" data-raw-source="[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)">IWDFDevice</a></p></td>
<td align="left"><p>デバイスを表します</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-file-object.md" data-raw-source="[File object](framework-file-object.md)">ファイル オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td align="left"><p>ファイルを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p>
フレームワークの機能によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-interrupt-object.md" data-raw-source="[Interrupt object](framework-interrupt-object.md)">オブジェクトを中断します。</a></p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt" data-raw-source="[IWDFInterrupt](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfinterrupt)">IWDFInterrupt</a></td>
<td align="left"><p>割り込みを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-queue-object.md" data-raw-source="[Queue object](framework-i-o-queue-object.md)">キュー オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfioqueue" data-raw-source="[IWDFIoQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfioqueue)">IWDFIoQueue</a></p></td>
<td align="left"><p>I/O 要求を受信する I/O キューを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-i-o-request-object.md" data-raw-source="[Request object](framework-i-o-request-object.md)">オブジェクトを要求します。</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest" data-raw-source="[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)">IWDFIoRequest</a></p></td>
<td align="left"><p>I/O 要求を表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p></p>
フレームワークの機能によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
<td align="left"><p></p>
(たとえば、リダイレクトされた要求); framework によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-target-object.md" data-raw-source="[Target object](framework-i-o-target-object.md)">ターゲット オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget" data-raw-source="[IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget)">IWDFIoTarget</a></p></td>
<td align="left"><p>別のドライバーが要求を送信するドライバーを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p>
いいえ、既定のターゲット。はい、その他のすべてのターゲット</td>
</tr>
<tr class="even">
<td align="left"><p>USB デバイス オブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice" data-raw-source="[IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)">IWDFUsbTargetDevice</a></p></td>
<td align="left"><p>USB に接続されているデバイスを表します。</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>[はい] (ターゲット オブジェクトを参照してください)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USB パイプ オブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe" data-raw-source="[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)">IWDFUsbTargetPipe</a></p></td>
<td align="left"><p>USB デバイスのパイプを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>[はい] (ターゲット オブジェクトを参照してください)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB インターフェイス オブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbinterface)">IWDFUsbInterface</a></p></td>
<td align="left"><p>USB デバイスのインターフェイスを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>[はい] (ターゲット オブジェクトを参照してください)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-base-object.md" data-raw-source="[Base object](framework-base-object.md)">基本オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject" data-raw-source="[IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)">IWDFObject</a></p></td>
<td align="left"><p>一般的な基本オブジェクトを表します</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>ドライバーによって作成された場合ははい。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-memory-object.md" data-raw-source="[Memory object](framework-memory-object.md)">メモリ オブジェクト</a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[IWDFMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfmemory)">IWDFMemory</a></p></td>
<td align="left"><p>メモリ オブジェクトを表します</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p></p>
フレームワークの機能によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
</tr>
</tbody>
</table>

 

 

 






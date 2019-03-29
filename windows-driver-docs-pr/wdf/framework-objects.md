---
title: フレームワーク オブジェクト
description: フレームワーク オブジェクト
ms.assetid: bd9ec812-205d-4f9a-b85b-4e3a2f7556bd
keywords:
- 一覧表示された WDK、UMDF オブジェクト
- 一覧表示されたフレームワーク オブジェクト WDK UMDF、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f1a58238ff1f83e45559f62a00c3ee6d9a4770
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570646"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558893" data-raw-source="[IWDFDriver](https://msdn.microsoft.com/library/windows/hardware/ff558893)">IWDFDriver</a></p></td>
<td align="left"><p>ドライバーを表します</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-device-object.md" data-raw-source="[Device object](framework-device-object.md)">デバイス オブジェクト</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556917" data-raw-source="[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)">IWDFDevice</a></p></td>
<td align="left"><p>デバイスを表します</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>いいえ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-file-object.md" data-raw-source="[File object](framework-file-object.md)">ファイル オブジェクト</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558912" data-raw-source="[IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)">IWDFFile</a></p></td>
<td align="left"><p>ファイルを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p></p>
フレームワークの機能によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-interrupt-object.md" data-raw-source="[Interrupt object](framework-interrupt-object.md)">オブジェクトを中断します。</a></p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/hh451283" data-raw-source="[IWDFInterrupt](https://msdn.microsoft.com/library/windows/hardware/hh451283)">IWDFInterrupt</a></td>
<td align="left"><p>割り込みを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-queue-object.md" data-raw-source="[Queue object](framework-i-o-queue-object.md)">キュー オブジェクト</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558943" data-raw-source="[IWDFIoQueue](https://msdn.microsoft.com/library/windows/hardware/ff558943)">IWDFIoQueue</a></p></td>
<td align="left"><p>I/O 要求を受信する I/O キューを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-i-o-request-object.md" data-raw-source="[Request object](framework-i-o-request-object.md)">オブジェクトを要求します。</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558985" data-raw-source="[IWDFIoRequest](https://msdn.microsoft.com/library/windows/hardware/ff558985)">IWDFIoRequest</a></p></td>
<td align="left"><p>I/O 要求を表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p></p>
フレームワークの機能によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
<td align="left"><p></p>
(たとえば、リダイレクトされた要求); framework によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-target-object.md" data-raw-source="[Target object](framework-i-o-target-object.md)">ターゲット オブジェクト</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559170" data-raw-source="[IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170)">IWDFIoTarget</a></p></td>
<td align="left"><p>別のドライバーが要求を送信するドライバーを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p></p>
いいえ、既定のターゲット。はい、その他のすべてのターゲット</td>
</tr>
<tr class="even">
<td align="left"><p>USB デバイス オブジェクト</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560362" data-raw-source="[IWDFUsbTargetDevice](https://msdn.microsoft.com/library/windows/hardware/ff560362)">IWDFUsbTargetDevice</a></p></td>
<td align="left"><p>USB に接続されているデバイスを表します。</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>[はい] (ターゲット オブジェクトを参照してください)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USB パイプ オブジェクト</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560391" data-raw-source="[IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)">IWDFUsbTargetPipe</a></p></td>
<td align="left"><p>USB デバイスのパイプを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>[はい] (ターゲット オブジェクトを参照してください)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USB インターフェイス オブジェクト</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560312" data-raw-source="[IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)">IWDFUsbInterface</a></p></td>
<td align="left"><p>USB デバイスのインターフェイスを表します</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>[はい] (ターゲット オブジェクトを参照してください)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-base-object.md" data-raw-source="[Base object](framework-base-object.md)">基本オブジェクト</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560200" data-raw-source="[IWDFObject](https://msdn.microsoft.com/library/windows/hardware/ff560200)">IWDFObject</a></p></td>
<td align="left"><p>一般的な基本オブジェクトを表します</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>ドライバーによって作成された場合ははい。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-memory-object.md" data-raw-source="[Memory object](framework-memory-object.md)">メモリ オブジェクト</a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559249" data-raw-source="[IWDFMemory](https://msdn.microsoft.com/library/windows/hardware/ff559249)">IWDFMemory</a></p></td>
<td align="left"><p>メモリ オブジェクトを表します</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p></p>
フレームワークの機能によって作成された場合は、なしドライバーによって作成された場合ははい。</td>
</tr>
</tbody>
</table>

 

 

 






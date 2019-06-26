---
title: IStiUSD インターフェイスの提供
description: IStiUSD インターフェイスの提供
ms.assetid: ed15b56b-0b63-4983-a4ff-df379a2b9de9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d11e17a702c58a2025e997326e6d1fe35e99bf4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376504"
---
# <a name="providing-an-istiusd-interface"></a>IStiUSD インターフェイスの提供





WIA は STI に基づいています。 STI に WIA ミニドライバーの統合を確保するために、ミニドライバーがから派生したインターフェイスを実装する必要があります、 [IStiUSD インターフェイス メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)します。 このインターフェイスは、WIA ミニドライバーに存在する必要があります。 **IStiUSD**インターフェイス (ドライバーの読み込み) などのデバイスを管理するために使用および手段が、 [IStiDevice インターフェイス メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)静止画像デバイスと通信します。 ミニドライバーはから派生したインターフェイスを完全に実装する必要があります、 [ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize) WIA サービスによって読み込まれるメソッド。

通常、 **IStiUSD**インターフェイス メソッドは、によって定義された同じ名前のメソッドによって呼び出される、 **IStiDevice**インターフェイス。 ミニドライバーを通常実装**IStiUSD**インターフェイス メソッドを呼び出して、適切なカーネル モード ドライバー。 各ミニドライバーがメソッドでない場合は、すべてのインターフェイス メソッドを定義する必要がありますに必要なだけを返すこと STIERR\_サポートされていません。

参照してください、 *wiacam*カメラ ミニドライバー サンプルファイル*IStiUSD.cpp*、ミニドライバーを実装する方法の例については、 **IStiUSD**インターフェイス。

次の表とによって定義されたメソッドのすべてについて説明します、 **IStiUSD**インターフェイス。 メソッドを実装または WIA ミニドライバーで条件付きで実装する必要がありますが識別されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-devicereset" data-raw-source="[&lt;strong&gt;IStiUSD::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-devicereset)"><strong>IStiUSD::DeviceReset</strong></a></p></td>
<td><p>静止画像デバイスを正常に初期化された状態にリセットします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-diagnostic" data-raw-source="[&lt;strong&gt;IStiUSD::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-diagnostic)"><strong>IStiUSD::Diagnostic</strong></a></p></td>
<td><p>静止画像デバイスでは、診断テストを実行します。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape" data-raw-source="[&lt;strong&gt;IStiUSD::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape)"><strong>IStiUSD::Escape</strong></a></p></td>
<td><p>静止画像デバイスのベンダー固有の I/O 操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities" data-raw-source="[&lt;strong&gt;IStiUSD::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getcapabilities)"><strong>IStiUSD::GetCapabilities</strong></a></p></td>
<td><p>デバイスの機能に静止画像を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiUSD::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterrorinfo)"><strong>IStiUSD::GetLastErrorInfo</strong></a></p></td>
<td><p>静止画像デバイスに関連付けられている最後の既知のエラーに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata" data-raw-source="[&lt;strong&gt;IStiUSD::GetNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getnotificationdata)"><strong>IStiUSD::GetNotificationData</strong></a></p></td>
<td><p>静止画像デバイスで発生した最新のイベントの説明を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getstatus" data-raw-source="[&lt;strong&gt;IStiUSD::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getstatus)"><strong>IStiUSD::GetStatus</strong></a></p></td>
<td><p>静止画像デバイスの状態を返します。 WIA ミニドライバーは、そのデバイスにイベントを生成するには、ボタンなどのオブジェクトがある場合、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize" data-raw-source="[&lt;strong&gt;IStiUSD::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)"><strong>IStiUSD::Initialize</strong></a></p></td>
<td><p>定義する COM オブジェクトのインスタンスを初期化します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index" data-raw-source="[IStiUSD interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)">IStiUSD インターフェイス</a>します。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice)"><strong>IStiUSD::LockDevice</strong></a></p></td>
<td><p>呼び出し元によって排他的に使用のデバイスをロックします。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreadcommand)"><strong>IStiUSD::RawReadCommand</strong></a></p></td>
<td><p>読み取りは、静止画像デバイスからの情報をコマンドします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreaddata" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreaddata)"><strong>IStiUSD::RawReadData</strong></a></p></td>
<td><p>静止画像デバイスからデータを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritecommand)"><strong>IStiUSD::RawWriteCommand</strong></a></p></td>
<td><p>静止画像デバイスにコマンド情報を書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritedata" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritedata)"><strong>IStiUSD::RawWriteData</strong></a></p></td>
<td><p>静止画像デバイスにデータを書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle" data-raw-source="[&lt;strong&gt;IStiUSD::SetNotificationHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-setnotificationhandle)"><strong>IStiUSD::SetNotificationHandle</strong></a></p></td>
<td><p>デバイス イベントの呼び出し元に通知するために、ミニドライバーが使用する必要がありますイベント ハンドルを指定します。 WIA ミニドライバーは、そのデバイスにイベントを生成するには、ボタンなどのオブジェクトがある場合、このメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-unlockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-unlockdevice)"><strong>IStiUSD::UnLockDevice</strong></a></p></td>
<td><p>デバイスのポートを閉じます。 WIA ミニドライバーは、このメソッドを実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





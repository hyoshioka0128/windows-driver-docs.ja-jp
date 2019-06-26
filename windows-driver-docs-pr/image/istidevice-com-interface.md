---
title: IStiDevice COM インターフェイス
description: IStiDevice COM インターフェイス
ms.assetid: b026fb74-9ce6-4d4e-8a5b-402731904064
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eca2a64e4a28dd377c95de15d5ecab2a9f5a707
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378915"
---
# <a name="istidevice-com-interface"></a>IStiDevice COM インターフェイス





**IStiDevice** COM インターフェイスと通信する機能をアプリケーションがデバイスを静止画像を提供します。 インターフェイス メソッドを使用すると、アプリケーション データとの通知を受け取る診断テストを実行するコマンド、送受信[イメージ デバイス イベントではまだ](still-image-device-events.md)とデバイスの機能と状態情報を取得します。

アクセス、 **IStiDevice**インターフェイスを呼び出すことによって取得、 **CreateDevice**のメソッド、 [IStillImage COM インターフェイス](istillimage-com-interface.md)します。 多くは、 **IStiDevice**によって定義された同じ名前のメソッドを呼び出すことによってインターフェイスのメソッドが実装されている、 [IStiUSD COM インターフェイス](istiusd-com-interface.md)します。

次の表とすべてのによって提供されるメソッドについて説明します、 **IStiDevice**インターフェイス。 テーブルでは、通常、各メソッドを呼び出す必要のあるクライアントの種類を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
<th>一般的な呼び出し元</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-devicereset" data-raw-source="[&lt;strong&gt;IStiDevice::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-devicereset)"><strong>IStiDevice::DeviceReset</strong></a></p></td>
<td><p>静止画像デバイスを既知の状態にリセットします。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-diagnostic" data-raw-source="[&lt;strong&gt;IStiDevice::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-diagnostic)"><strong>IStiDevice::Diagnostic</strong></a></p></td>
<td><p>静止画像デバイスで診断テストを実行します。</p></td>
<td><p>スキャナーとカメラのコントロール パネル</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-escape" data-raw-source="[&lt;strong&gt;IStiDevice::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-escape)"><strong>IStiDevice::Escape</strong></a></p></td>
<td><p>静止画像デバイスには、ベンダー固有の I/O 操作の要求を送信します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getcapabilities" data-raw-source="[&lt;strong&gt;IStiDevice::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getcapabilities)"><strong>IStiDevice::GetCapabilities</strong></a></p></td>
<td><p>デバイスの機能に静止画像を返します。</p></td>
<td><p>イベント モニターを静止画像します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterror" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterror)"><strong>IStiDevice::GetLastError</strong></a></p></td>
<td><p>静止画像デバイスに関連付けられている最後の既知のエラーを返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlasterrorinfo)"><strong>IStiDevice::GetLastErrorInfo</strong></a></p></td>
<td><p>静止画像デバイスに関連付けられている最後の既知のエラーに関する情報を返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata" data-raw-source="[&lt;strong&gt;IStiDevice::GetLastNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata)"><strong>IStiDevice::GetLastNotificationData</strong></a></p></td>
<td><p>静止画像デバイスで発生した最新のイベントの説明を返します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getstatus" data-raw-source="[&lt;strong&gt;IStiDevice::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getstatus)"><strong>IStiDevice::GetStatus</strong></a></p></td>
<td><p>静止画像デバイスの状態情報を返します。</p></td>
<td><p>イメージの取得 Api と、まだイベント モニターの画像</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-initialize" data-raw-source="[&lt;strong&gt;IStiDevice::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-initialize)"><strong>IStiDevice::Initialize</strong></a></p></td>
<td><p>オブジェクトのインスタンスを初期化します。</p></td>
<td><p>直接呼び出されません</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-lockdevice)"><strong>IStiDevice::LockDevice</strong></a></p></td>
<td><p>呼び出し元によって排他的に使用のデバイスをロックします。</p></td>
<td><p>すべて<strong>IStiDevice</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreadcommand)"><strong>IStiDevice::RawReadCommand</strong></a></p></td>
<td><p>読み取りは、静止画像デバイスからの情報をコマンドします。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreaddata" data-raw-source="[&lt;strong&gt;IStiDevice::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawreaddata)"><strong>IStiDevice::RawReadData</strong></a></p></td>
<td><p>静止画像デバイスからデータを読み取ります。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritecommand)"><strong>IStiDevice::RawWriteCommand</strong></a></p></td>
<td><p>送信は、静止画像デバイス情報をコマンドします。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritedata" data-raw-source="[&lt;strong&gt;IStiDevice::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-rawwritedata)"><strong>IStiDevice::RawWriteData</strong></a></p></td>
<td><p>静止画像デバイスにデータを書き込みます。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-release" data-raw-source="[&lt;strong&gt;IStiDevice::Release&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-release)"><strong>IStiDevice::Release</strong></a></p></td>
<td><p>オブジェクトのインスタンスを閉じて、アクセス権を削除、 <strong>IStiDevice</strong>インターフェイス。</p></td>
<td><p>すべて<strong>IStiDevice</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe" data-raw-source="[&lt;strong&gt;IStiDevice::Subscribe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe)"><strong>IStiDevice::Subscribe</strong></a></p></td>
<td><p>デバイス イベントの通知を受け取る、呼び出し元を登録します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice" data-raw-source="[&lt;strong&gt;IStiDevice::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unlockdevice)"><strong>IStiDevice::UnLockDevice</strong></a></p></td>
<td><p>デバイスのロックを解除します。</p></td>
<td><p>すべて<strong>IStiDevice</strong>クライアント インターフェイス</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unsubscribe" data-raw-source="[&lt;strong&gt;IStiDevice::UnSubscribe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unsubscribe)"><strong>IStiDevice::UnSubscribe</strong></a></p></td>
<td><p>デバイス イベントの通知に登録されているアプリケーションの一覧から、呼び出し元を削除します。</p></td>
<td><p>イメージの取得 Api</p></td>
</tr>
</tbody>
</table>

 

 

 





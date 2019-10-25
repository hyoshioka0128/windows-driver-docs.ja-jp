---
title: IStiUSD インターフェイスの提供
description: IStiUSD インターフェイスの提供
ms.assetid: ed15b56b-0b63-4983-a4ff-df379a2b9de9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab282f73d6bce43b50096639bb926789ba9f2e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840766"
---
# <a name="providing-an-istiusd-interface"></a>IStiUSD インターフェイスの提供





WIA は、STI でビルドされます。 STI とミニドライバーの統合を確実にするために、ミニドライバーは、 [i のインターフェイスメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)から派生したインターフェイスを実装する必要があります。 このインターフェイスは、WIA ミニドライバーに存在している必要があります。 デバイスの管理には**i(** ドライバーの読み込みなど) のインターフェイスが使用されます。これは、 [iのデバイスインターフェイスメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)が静止イメージデバイスと通信する手段です。 ミニドライバーは、WIA サービスによって読み込まれるために、 [**i:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドから派生したインターフェイスを完全に実装する必要があります。

通常、iare **us**インターフェイスメソッドは、 **iare device**インターフェイスで定義されている同様の名前付きメソッドによって呼び出されます。 ミニドライバーは、通常、適切なカーネルモードドライバーを呼び出すことによって**Istiusd**インターフェイスメソッドを実装します。 各ミニドライバーは、すべてのインターフェイスメソッドを定義する必要がありますが、メソッドが不要な場合は、単に、サポートされていない\_を返すことができます。

ミニドライバーが**I_a usd**インターフェイスを実装する方法の例については、 *wiacam*カメラサンプルミニドライバー*ファイルを参照*してください。

次の表は、 **Iの米国**インターフェイスで定義されているすべてのメソッドの一覧とその説明を示しています。 WIA ミニドライバーによって実装または条件付きで実装する必要があるメソッドが識別されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset" data-raw-source="[&lt;strong&gt;IStiUSD::DeviceReset&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset)"><strong>Ievicereset::D</strong></a></p></td>
<td><p>静止イメージデバイスを既知の初期化済み状態にリセットします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic" data-raw-source="[&lt;strong&gt;IStiUSD::Diagnostic&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic)"><strong>I(米ドル)::D iとらわれない</strong></a></p></td>
<td><p>静止イメージデバイスで診断テストを実行します。 このメソッドは、WIA ミニドライバーが実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape" data-raw-source="[&lt;strong&gt;IStiUSD::Escape&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)"><strong>I、Usd:: Escape</strong></a></p></td>
<td><p>静止イメージデバイスでベンダー固有の i/o 操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities" data-raw-source="[&lt;strong&gt;IStiUSD::GetCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)"><strong>Iと Usd:: GetCapabilities</strong></a></p></td>
<td><p>静止イメージデバイスの機能を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo" data-raw-source="[&lt;strong&gt;IStiUSD::GetLastErrorInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo)"><strong>Iと Usd:: GetLastErrorInfo</strong></a></p></td>
<td><p>静止イメージデバイスに関連付けられている最後の既知のエラーに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata" data-raw-source="[&lt;strong&gt;IStiUSD::GetNotificationData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)"><strong>I、Usd:: GetNotificationData</strong></a></p></td>
<td><p>静止イメージデバイスで発生した最新のイベントの説明を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus" data-raw-source="[&lt;strong&gt;IStiUSD::GetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)"><strong>IGetStatus::</strong></a></p></td>
<td><p>静止イメージデバイスの状態を返します。 イベントを生成できるボタンなどのオブジェクトがデバイスにある場合、WIA ミニドライバーはこのメソッドを実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize" data-raw-source="[&lt;strong&gt;IStiUSD::Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)"><strong>Iと Usd:: Initialize</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index" data-raw-source="[IStiUSD interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)">Iwhere-object インターフェイス</a>を定義する COM オブジェクトのインスタンスを初期化します。 このメソッドは、WIA ミニドライバーが実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::LockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)"><strong>I_ Usd:: LockDevice</strong></a></p></td>
<td><p>呼び出し元によって排他的に使用されるようにデバイスをロックします。 このメソッドは、WIA ミニドライバーが実装する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand)"><strong>IStiUSD:: RawReadCommand</strong></a></p></td>
<td><p>静止イメージデバイスからコマンド情報を読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata" data-raw-source="[&lt;strong&gt;IStiUSD::RawReadData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)"><strong>IRawReadData::</strong></a></p></td>
<td><p>静止イメージデバイスからデータを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteCommand&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand)"><strong>IStiUSD:: RawWriteCommand</strong></a></p></td>
<td><p>コマンド情報を静止イメージデバイスに書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata" data-raw-source="[&lt;strong&gt;IStiUSD::RawWriteData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)"><strong>IStiUSD:: RawWriteData</strong></a></p></td>
<td><p>静止イメージデバイスにデータを書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle" data-raw-source="[&lt;strong&gt;IStiUSD::SetNotificationHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)"><strong>Iと Usd:: SetNotificationHandle</strong></a></p></td>
<td><p>ミニドライバーがデバイスイベントの呼び出し元に通知するために使用するイベントハンドルを指定します。 イベントを生成できるボタンなどのオブジェクトがデバイスにある場合、WIA ミニドライバーはこのメソッドを実装する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice" data-raw-source="[&lt;strong&gt;IStiUSD::UnLockDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)"><strong>IUnLockDevice::</strong></a></p></td>
<td><p>デバイスのポートを閉じます。 このメソッドは、WIA ミニドライバーが実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
Description: Windows.Devices.Usb 名前空間には、外部の USB デバイスと通信する Api が提供されます。
title: USB デバイス用の UWP アプリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4519017a0238e888526ce247eeeedc5b73d51084
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385339"
---
# <a name="uwp-app-for-a-usb-device"></a>USB デバイス用の UWP アプリ


[ **Windows.Devices.Usb** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)名前空間は、デバイス ドライバーとして WinUSB (Winusb.sys) を使用する外部の USB デバイスと通信する Windows アプリを提供します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talking to USB devices, start to finish (UWP app)](talking-to-usb-devices-start-to-finish.md)">USB デバイスとの対話を開始する (UWP アプリ) の完了</a></p></td>
<td><p>Windows 8.1 で導入された、Windows ランタイム Api を使用すると、ユーザーが自分の USB 周辺機器にアクセスする UWP アプリを記述できます。 このようなアプリできますユーザーが指定した条件に基づいてデバイスに接続、デバイスに関する情報を取得、デバイスにデータを送信し逆に、デバイスからのデータ ストリームを取得および割り込みデータについては、デバイスをポーリングします。</p></td>
</tr>
<tr class="even">
<td><p><a href="updating-the-app-manifest-with-usb-device-capabilities.md" data-raw-source="[How to add USB device capabilities to the app manifest](updating-the-app-manifest-with-usb-device-capabilities.md)">アプリケーション マニフェストに USB デバイスの機能を追加する方法</a></p></td>
<td><p>このトピックでは、使用する Windows アプリを必要とされるデバイスの機能を説明します、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows.Devices.Usb</strong> </a>名前空間。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">USB デバイス (UWP アプリ) に接続する方法</a></p></td>
<td><p>Windows 8.1 では、USB デバイスと対話する UWP アプリを記述できます。 アプリは、管理コマンドを送信、デバイスの情報を取得、読み取り、および一括および割り込みのエンドポイントとの間のデータを書き込むことができます。 すべての操作を行うことができます、前にデバイスを検出し、接続を確立する必要があります。</p>
<p>この部分では、使用する方法を説明します、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)"> <strong>DeviceWatcher</strong> </a>デバイスを見つけて、ファイルを開いて、アプリからの通信を開始するオブジェクト。 使用してこれが完了したら、デバイスを閉じる方法も学習します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">USB 制御転送 (UWP アプリ) を送信する方法</a></p></td>
<td><p>通常、USB デバイスと通信するアプリは、いくつかのコントロールの転送要求を送信します。 それらの要求では、デバイスに関する情報を取得し、ハードウェア ベンダーによって定義されたコントロールのコマンドを送信します。 このトピックでは、コントロールの転送と書式を設定し、UWP アプリで送信する方法について学習します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">USB 割り込み転送要求 (UWP アプリ) を送信する方法</a></p></td>
<td><p>USB デバイスは、送信または一定の間隔でデータを受信できるように、割り込みのエンドポイントをサポートできます。 これを実現する、ホストは一定の間隔でデバイスをポーリングし、データが転送されるたびに、ホストがデバイスをポーリングします。 割り込み転送は、デバイスからの割り込みのデータを取得するためほとんど使用されます。 このトピックでは、UWP アプリがデバイスから継続的な割り込みデータを取得する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">USB 一括転送要求 (UWP アプリ) を送信する方法</a></p></td>
<td><p>このトピックでは、USB 一括転送と USB デバイスと通信する UWP アプリからの転送要求を開始する方法について学習します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">USB ディスクリプター (UWP アプリ) を取得する方法</a></p></td>
<td><p>に関する情報の取得、USB デバイスとの対話の主なタスクの 1 つです。 すべての USB デバイスは、記述子と呼ばれるデータ構造がいくつかの形式で情報を提供します。 このトピックでは、UWP アプリがエンドポイント、インターフェイス、構成、およびデバイス レベルのデバイスから記述子を取得する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">USB インターフェイスの設定 (UWP アプリ) を選択する方法</a></p></td>
<td><p>このトピックでは、USB インターフェイス内の設定を変更する方法について学習します。 使用して、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)"> <strong>UsbInterfaceSetting</strong> </a>オブジェクトを現在の設定を取得し、インターフェイスで設定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-samples"></a>USB のサンプル


-   [カスタム USB デバイスへのアクセスのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [USB CDC コントロールのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [ファームウェアの更新プログラムの USB デバイスのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)

## <a name="what-are-the-limitations-of-the-namespace"></a>名前空間の制限事項とは


*できません*使用[ **Windows.Devices.Usb** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)このような場合。

-   デバイス ドライバーが Winusb.sys でない場合は。
-   デバイスの USB アイソクロナス エンドポイントと通信するには。
-   SuperSpeed 一括エンドポイントのストリームを通信するには。 それらのエンドポイントの一括転送用の USB の Windows ランタイム クラスがのみを送信またはエンドポイントの最初のストリームからデータを受信できます。
-   同時に、デバイスにアクセスする複数のアプリを許可するとします。
-   USB デバイスは、内部デバイスです。
    **注**   Api は主に周辺機器にアクセスするために設計されています。 API は、内部の USB デバイスを PC にもアクセスできます。 ただし、UWP アプリから PC 内部の USB デバイスへのアクセスは、その PC で OEM によって明示的に宣言されている権限を持つアプリに制限されます。

     

-   カーネル モード デバイス スタックが Winusb.sys の上のフィルター ドライバーです。
    **注**  このシナリオでは、特権のあるアプリのみを利用できます。

     

-   デバイスに複数の USB 構成と、先頭以外の構成を選択します。 [**Windows.Devices.Usb** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)既定で最初の構成を選択します。

## <a name="related-topics"></a>関連トピック
[**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)  




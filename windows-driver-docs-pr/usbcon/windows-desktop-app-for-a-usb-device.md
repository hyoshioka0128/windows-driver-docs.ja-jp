---
Description: アプリケーションが WinUSB 機能を呼び出して USB デバイスと通信する方法について説明します。
title: USB デバイス用の Windows デスクトップ アプリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7c0c641914c4d73925e3138e9321d1cce0ed81
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210142"
---
# <a name="windows-desktop-app-for-a-usb-device"></a>USB デバイス用の Windows デスクトップ アプリ


このトピックでは、アプリケーションが[Winusb 機能](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を呼び出して usb デバイスと通信する方法について説明します。 このようなアプリケーションでは、デバイスの関数ドライバーとして[winusb](winusb.md) (winusb .sys) をインストールする必要があります。 デバイスのカーネルモードスタック内の WinUSB。 このドライバーは、Windows\\System32\\drivers フォルダーの \\windows に含まれています。

USB デバイスの関数ドライバーとして Winusb を使用している場合は、アプリケーションから[Winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を呼び出してデバイスと通信することができます。 これらの関数は、ユーザーモードの DLL によって公開され、通信プロセスを簡略化します。 標準的な USB 操作 (デバイスの構成、制御要求の送信、デバイスとのデータの転送など) を実行するためのデバイス i/o 制御要求を構築する代わりに、アプリケーションは同等の WinUSB 関数を呼び出します。

Winusb .dll は、アプリケーションによって提供されるデータを使用して適切なデバイス i/o 制御要求を作成し、その要求を処理のために Winusb .sys に送信します。 WinUSB 関数は、USB スタックと通信するために、アプリケーションの要求に関連する適切な IOCTL を使用して[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出します。 要求が完了すると、WinUSB 関数は、Winusb .sys によって返されたすべての情報 (読み取り要求のデータなど) を呼び出しプロセスに渡します。 **DeviceIoControl**の呼び出しが成功した場合、0以外の値が返されます。 呼び出しが失敗した場合、または待機状態になっている (直ちに処理されない) 場合、 **DeviceIoControl**は0の値を返します。 エラーが発生した場合、アプリケーションは、より詳細なエラーメッセージを表示するために、 [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)を呼び出すことができます。

WinUSB 関数を使用すると、ドライバーを実装する場合と比べて、デバイスとの通信が簡単になります。 ただし、次の制限事項に注意してください。

-   WinUSB functions は、一度に1つのアプリケーションがデバイスと通信できるようにします。 デバイスと同時に通信するために複数のアプリケーションが必要な場合は、関数ドライバーを実装する必要があります。
-   Windows 8.1 する前に、WinUSB 関数は、アイソクロナスエンドポイントとの間でのデータのストリーミングをサポートしていません。
-   WinUSB 関数は、既にカーネルモードをサポートしているデバイスをサポートしていません。 このようなデバイスの例としては、それぞれテレフォニー API (TAPI) と NDIS でサポートされているモデムとネットワークアダプターがあります。
-   多機能デバイスの場合は、デバイスの INF ファイルを使用して、各 USB 関数に対してインボックスカーネルモードドライバーまたは Winusb .sys を個別に指定できます。 ただし、これらのオプションはいずれも、特定の関数に対してのみ指定できます。

**注**  WinUSB 関数には、Windows XP 以降が必要です。 これらの関数を C/C++ アプリケーションで使用して、USB デバイスと通信することができます。 WinUSB Api を使用する UWP アプリを作成するには、「 [USB デバイス用の uwp アプリ](writing-usb-device-companion-apps-for-microsoft-store.md)」を参照してください。

## <a name="getting-started"></a>作業を開始しています...


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ステップ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>手順 1</strong>-デバイス用の Windows デスクトップアプリを作成するために必要なツールを入手します。</p></td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=623328" data-raw-source="[Microsoft Visual Studio (Ultimate or Professional)]( https://go.microsoft.com/fwlink/p/?LinkId=623328)">Microsoft Visual Studio (Ultimate または Professional)</a>をインストールします。</li>
<li><a href="https://download.microsoft.com/download/E/C/E/ECE11176-1E40-46E7-A24B-D507D7F6FB65/wdk/wdksetup.exe" data-raw-source="[Windows Driver Kit (WDK) 8.1](https://download.microsoft.com/download/E/C/E/ECE11176-1E40-46E7-A24B-D507D7F6FB65/wdk/wdksetup.exe)">Windows Driver Kit (WDK) 8.1</a>をインストールします。</li>
</ul>
<div class="alert">WDK 8.1 をインストールする前に、Visual Studio をインストールする必要がある
<strong>ことに注意</strong>してください  。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p><strong>手順 2</strong>-テスト用の USB デバイスとそのハードウェア仕様を取得します。 仕様を使用して、アプリの機能と関連する設計上の決定を決定します。</p></td>
<td><p>学習目的の場合、一般的な選択肢は次のとおりです。</p>
<ul>
<li>OSR USB FX2 learning kit。 このキットは、このドキュメント セットに含まれている学習用 USB サンプルに最も適しています。 この学習キットは、 <a href="https://www.osronline.com/" data-raw-source="[OSR Online](https://www.osronline.com/)">OSR オンライン</a>で入手できます。</li>
<li>Microsoft USB テストツール (MUTT) デバイス。 MUTT ハードウェアは、 <a href="https://jjgtechnologies.com/mutt.md" data-raw-source="[JJG Technologies](https://jjgtechnologies.com/mutt.md)">Jjg テクノロジ</a>から購入できます。 デバイスにインストールされているファームウェアがインストールされていません。 ファームウェアをインストールするには、<a href="mutt-software-package.md" data-raw-source="[this Web site](mutt-software-package.md)">この Web サイト</a>から MUTT ソフトウェアパッケージをダウンロードし、MUTTUtil を実行します。 詳細については、パッケージに含まれているドキュメントを参照してください。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>手順 3</strong>-デバイスへのハンドルを取得するスケルトンアプリを記述します。</p></td>
<td><p>最初のアプリは、次の2つの方法のいずれかで作成できます。</p>
<ul>
<li><p>Visual Studio に含まれる WinUSB テンプレートに基づいてアプリを作成します。 詳細については、「 <a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB テンプレートに基づいて Windows デスクトップアプリを作成する</a>」を参照してください。</p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)">Setupapi.log</a>ルーチンを呼び出して、デバイスへのハンドルを取得し、 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"><strong>WinUsb_Initialize</strong></a>を呼び出して開きます。 詳細については、「 <a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">Winusb 機能を使用して Usb デバイスにアクセスする方法</a>」を参照してください。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>手順 6</strong>-デバイス用に winusb をインストールします。</p></td>
<td><p>デバイスの Winusb .sys をインストールします。</p>
<ul>
<li>Visual Studio を使用している場合は、Visual Studio の配置を使用して、対象のコンピューターにドライバーパッケージをインストールします。 手順については、「 <a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB テンプレートに基づいて Windows デスクトップアプリを作成する</a>」を参照してください。</li>
<li>それ以外の場合は、カスタム INF を作成してデバイスマネージャーにドライバーを手動でインストールします。 詳細については、 <a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">winusb (winusb .sys) のインストール</a>に関する説明を参照してください。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>手順 4</strong>-デバイスに関する情報を取得し、その記述子を表示します。 概念的な情報については、「<a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">すべての USB 開発者向けの概念</a>」を参照してください。</p></td>
<td><p>構成記述子、サポートされている各代替設定のインターフェイス記述子、およびエンドポイント記述子を読み取って、デバイスの機能に関する情報を取得します。</p>
<p>詳細については、「<a href="using-winusb-api-to-communicate-with-a-usb-device.md#query" data-raw-source="[Query the Device for USB Descriptors](using-winusb-api-to-communicate-with-a-usb-device.md#query)">デバイスで USB 記述子を照会する</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>手順 5</strong>: アプリから USB 制御転送を送信する。</td>
<td><p>標準のコントロール要求とベンダーコマンドをデバイスに送信します。 詳細については、「<a href="using-winusb-api-to-communicate-with-a-usb-device.md#control" data-raw-source="[Send Control Transfer to the Default Endpoint](using-winusb-api-to-communicate-with-a-usb-device.md#control)">既定のエンドポイントへの送信制御転送」を</a>参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>手順 6</strong>-アプリから一括転送または割り込み転送を送信する。</p></td>
<td><p>デバイスでサポートされている一括、割り込み、およびアイソクロナスエンドポイントとの間で読み取りおよび書き込み操作を実行します。 詳細については、「 <a href="using-winusb-api-to-communicate-with-a-usb-device.md#io" data-raw-source="[Issue I/O Requests](using-winusb-api-to-communicate-with-a-usb-device.md#io)">I/o 要求の発行</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>手順 7</strong>: アプリからのアイソクロナス転送を送信します。</p></td>
<td><p>アイソクロナス読み取り要求と書き込み要求を送信します。ほとんどの場合、データのストリーミングに使用します。 この機能は、Windows 8.1 でのみ使用できます。 詳細については、「 <a href="getting-set-up-to-use-windows-devices-usb.md" data-raw-source="[Sending USB isochronous transfers from a WinUSB desktop app](getting-set-up-to-use-windows-devices-usb.md)">winusb デスクトップアプリからの usb アイソクロナス転送の送信</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB デバイス用の Windows アプリケーションの開発](developing-windows-applications-that-communicate-with-a-usb-device.md)  
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  




---
Description: Learn about how an application can call WinUSB Functions to communicate with a USB device.
title: USB デバイスの Windows デスクトップ アプリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 557ae71709675dc25facc322c8d9a752fbd2c73f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529294"
---
# <a name="windows-desktop-app-for-a-usb-device"></a>USB デバイスの Windows デスクトップ アプリ


このトピックでは、アプリケーションを呼び出す方法について説明します[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb) USB デバイスと通信します。 このようなアプリケーションには、 [WinUSB](winusb.md) (Winusb.sys) は、デバイスの機能のドライバーとしてインストールする必要があります。 デバイスのカーネル モード スタックで WinUSB します。 このドライバーにはでの Windows が含まれて、 \\Windows\\System32\\ドライバー フォルダー。

Winusb.sys として USB デバイスの機能のドライバーを使用している場合は、呼び出す[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb) 、デバイスと通信するアプリケーションから。 ユーザー モード DLL Winusb.dll、によって公開されるこれらの関数は、通信プロセスを簡略化します。 (デバイスを構成、制御の要求を送信して転送するデータをまたはデバイスから) などの標準の USB 操作を実行するデバイスの I/O 制御要求を構築するには、代わりには、アプリケーションは、同等の WinUSB 関数を呼び出します。

Winusb.dll はアプリケーションによって提供されるデータを使用して、適切なデバイスの I/O 制御要求を作成し、要求を処理するため Winusb.sys に送信します。 WinUSB 関数を呼び出し、USB スタックと通信する、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)アプリケーションの要求に関連付けられた適切な IOCTL で関数をします。 要求が完了したら、WinUSB 関数は呼び出し元のプロセスに返信 Winusb.sys (読み取り要求からのデータ) などによって返されるすべての情報を渡します。 場合に呼び出し**DeviceIoControl**が成功すると、0 以外の値はすべて返します。 呼び出しが故障したかが保留されています (処理されませんすぐに)、 **DeviceIoControl**ゼロ値を返します。 エラーが発生した場合、アプリケーションを呼び出すことができます[ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)より詳細なエラー メッセージ。

WinUSB 関数を使用してドライバーを実装するよりも、デバイスと通信する方が簡単になります。 ただし、次の制限事項に注意してください。

-   WinUSB 関数を使用すると、デバイスと通信するために、一度に 1 つのアプリケーション。 デバイスと同時に通信するために 1 つ以上のアプリケーションを必要とする場合は、関数ドライバーを実装する必要があります。
-   Windows 8.1 では、前に WinUSB 関数は、アイソクロナス エンドポイントとの間のストリーミング データをサポートしています。
-   WinUSB 関数は、カーネル モードのサポートが既に存在するデバイスをサポートしていません。 このようなデバイスの例には、モデムとそれぞれに、テレフォニー API (TAPI) と NDIS でサポートされているネットワーク アダプターが含まれます。
-   多機能デバイスは、USB 関数ごとに個別にボックスでのカーネル モード ドライバーまたは Winusb.sys のいずれかを指定するのに、デバイスの INF ファイルを使用することができます。 ただし、これらのオプションの両方ではなく、特定の関数の 1 つだけ指定できます。

**注**  WinUSB 関数に必要な Windows XP またはそれ以降。 USB デバイスとの通信に、C/C++ アプリケーションでこれらの関数を使用できます。 WinUSB Api を使用する UWP アプリを作成するを参照してください。 [USB デバイス用の UWP アプリ](writing-usb-device-companion-apps-for-microsoft-store.md)します。

## <a name="getting-started"></a>作業の開始しています.


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>手順</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>手順 1.</strong>-デバイスの Windows デスクトップ アプリを作成する必要があるツールを入手します。</p></td>
<td><ul>
<li>インストール<a href="https://go.microsoft.com/fwlink/p/?LinkId=623328" data-raw-source="[Microsoft Visual Studio (Ultimate or Professional)]( https://go.microsoft.com/fwlink/p/?LinkId=623328)">(Ultimate または Professional)、Microsoft Visual Studio</a>します。</li>
<li>インストール、 <a href="http://download.microsoft.com/download/E/C/E/ECE11176-1E40-46E7-A24B-D507D7F6FB65/wdk/wdksetup.exe" data-raw-source="[Windows Driver Kit (WDK) 8.1](http://download.microsoft.com/download/E/C/E/ECE11176-1E40-46E7-A24B-D507D7F6FB65/wdk/wdksetup.exe)">Windows Driver Kit (WDK) 8.1</a>します。</li>
</ul>
<div class="alert">
<strong>注</strong>  WDK 8.1 をインストールする前に Visual Studio をインストールする必要があります。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p><strong>手順 2</strong>: テストの USB デバイスとそのハードウェア仕様を取得します。 定義を使用して、アプリと関連の設計に関する決定事項の機能を決定します。</p></td>
<td><p>学習目的は、一般的な選択肢があります。</p>
<ul>
<li>OSR USB FX2 ラーニング キットです。 キットは、このドキュメント セットに含まれる USB サンプルを調べる最も適しています。 ラーニング キットを入手することができます<a href="http://www.osronline.com/" data-raw-source="[OSR Online](http://www.osronline.com/)">OSR オンライン</a>します。</li>
<li>Microsoft USB Test Tool (MUTT) デバイス。 MUTT ハードウェアを購入できる<a href="http://jjgtechnologies.com/mutt.md" data-raw-source="[JJG Technologies](http://jjgtechnologies.com/mutt.md)">JJG テクノロジ</a>します。 デバイスのファームウェアがインストールされているインストールではありません。 ファームウェアをインストールするから MUTT ソフトウェア パッケージをダウンロード<a href="mutt-software-package.md" data-raw-source="[this Web site](mutt-software-package.md)">この Web サイト</a>MUTTUtil.exe を実行します。 詳細については、パッケージに付属のマニュアルを参照してください。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>手順 3</strong>-デバイスを識別するハンドルを取得するスケルトン アプリを作成します。</p></td>
<td><p>最初のアプリは、2 つの方法のいずれかで記述できます。</p>
<ul>
<li><p>Visual Studio に含まれている WinUSB テンプレートに基づいてアプリを作成します。 詳細については、<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB テンプレートに基づく Windows デスクトップ アプリを記述</a>を参照してください。</p></li>
<li><p>呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/ff550855" data-raw-source="[SetupAPI](https://msdn.microsoft.com/library/windows/hardware/ff550855)">SetupAPI</a>ルーチンをデバイスを識別するハンドルを取得して呼び出すことによって開きます<a href="https://msdn.microsoft.com/library/windows/hardware/ff540277" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540277)"> <strong>WinUsb_Initialize</strong></a>します。 詳細については、<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">WinUSB 関数を使用して、USB デバイスへのアクセス方法</a>を参照してください。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>手順 6</strong>— Winusb.sys のデバイスにインストールします。</p></td>
<td><p>デバイスの Winusb.sys をインストールします。</p>
<ul>
<li>Visual Studio を使用している場合は、Visual Studio の配置を使用して、ターゲット コンピューターでドライバー パッケージをインストールします。 手順については、<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB テンプレートに基づく Windows デスクトップ アプリを記述</a>を参照してください。</li>
<li>それ以外の場合、手動でドライバーをインストール、デバイス マネージャーにカスタム INF を記述することで。 詳細については、<a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB (Winusb.sys) インストール</a>を参照してください。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>手順 4</strong>— デバイスに関する情報を取得し、その記述子を表示します。 概念については、<a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">すべて USB 開発者の概念</a>を参照してください。</p></td>
<td><p>構成記述子、インターフェイスの記述子のサポートされている各代替設定、およびそのエンドポイント記述子を読み取ることによって、デバイスの機能に関する情報を取得します。</p>
<p>詳しくは、<a href="using-winusb-api-to-communicate-with-a-usb-device.md#query" data-raw-source="[Query the Device for USB Descriptors](using-winusb-api-to-communicate-with-a-usb-device.md#query)">記述子の USB デバイスを照会</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>手順 5</strong>-USB 制御転送をアプリから送信します。</td>
<td><p>標準のコントロール要求、仕入先のコマンドをデバイスに送信します。 詳細については、<a href="using-winusb-api-to-communicate-with-a-usb-device.md#control" data-raw-source="[Send Control Transfer to the Default Endpoint](using-winusb-api-to-communicate-with-a-usb-device.md#control)">コントロールは、既定のエンドポイントに転送送信</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>手順 6</strong>-アプリから送信一括または割り込みを転送します。</p></td>
<td><p>読み取りを実行し、一括、割り込み、およびデバイスでサポートされているアイソクロナス エンドポイントとの間に操作を記述します。 詳細については、<a href="using-winusb-api-to-communicate-with-a-usb-device.md#io" data-raw-source="[Issue I/O Requests](using-winusb-api-to-communicate-with-a-usb-device.md#io)">問題 I/O 要求</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>手順 7</strong>— アイソクロナス転送をアプリから送信します。</p></td>
<td><p>アイソクロナス読み取りを送信し、データのストリーミングに使用されるほとんどの場合、要求を記述します。 この機能は、Windows 8.1 で利用可能なだけです。 詳細については、<a href="getting-set-up-to-use-windows-devices-usb.md" data-raw-source="[Sending USB isochronous transfers from a WinUSB desktop app](getting-set-up-to-use-windows-devices-usb.md)">WinUSB デスクトップ アプリから送信する USB アイソクロナス転送</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB デバイスの Windows アプリケーションの開発](developing-windows-applications-that-communicate-with-a-usb-device.md)  
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  




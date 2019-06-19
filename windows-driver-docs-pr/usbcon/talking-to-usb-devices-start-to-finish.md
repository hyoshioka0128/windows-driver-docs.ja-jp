---
Description: Windows 8.1 で導入された、Windows ランタイム Api を使用すると、ユーザーが自分の USB 周辺機器にアクセスする UWP アプリを記述できます。
title: USB デバイスとの対話、開始から終了まで (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 431d3a959db81680f062ea57a4e1ee04d6c5d935
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161516"
---
# <a name="talking-to-usb-devices-start-to-finish-uwp-app"></a>USB デバイスとの対話、開始から終了まで (UWP アプリ)


**概要**

-   USB デバイスと通信する UWP アプリを作成するためのエンド ツー エンド チュートリアル
-   **付属のサンプル**:[カスタム USB デバイスへのアクセスのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)

**重要な API**

-   [**Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)
-   [**Windows.Devices.Enumeration**](https://msdn.microsoft.com/library/windows/apps/br225459)
-   [**Windows.Devices.Background**](https://msdn.microsoft.com/library/windows/apps/dn263409)

Windows 8.1 で導入された、Windows ランタイム Api を使用すると、ユーザーが自分の USB 周辺機器にアクセスする UWP アプリを記述できます。 このようなアプリできますユーザーが指定した条件に基づいてデバイスに接続、デバイスに関する情報を取得、デバイスにデータを送信し逆に、デバイスからのデータ ストリームを取得および割り込みデータについては、デバイスをポーリングします。

ここで説明してどのように C++ を使用して UWP アプリC#、または Visual Basic アプリはこれらのタスクを実装しに含まれるクラスの使用を示す例へのリンク[ **Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)。 アプリ マニフェストで必要なデバイス機能経由で移動方法と、デバイスが接続されているときに、アプリを起動します。 データの転送タスク、バック グラウンドで実行もバッテリ寿命を節約するためにアプリケーションが中断されたときにする方法を紹介します。

このセクションの手順に従って、またはに直接進む、[カスタム USB デバイス アクセス サンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)します。 付属のサンプルにならないように移動、コードについて説明しませんが、手順ここでは、すべてを実装します。 いくつかの手順が、**サンプルの方が**セクションがコードをすばやく見つけるのに役立ちます。 サンプルのソース ファイルの構造はシンプルでフラット ソース ファイルの複数のレイヤーをドリルダウンすることがなくコードを簡単に見つけることができます。 ただし、分割し、独自のプロジェクトを異なる方法で整理することもできます。

## <a name="in-this-section"></a>このセクションの内容


-   [**手順 1.** -デバイスのドライバーを関数として Microsoft が提供 WinUSB ドライバーをインストールします。](#step1)
-   [**手順 2**-Get デバイス インターフェイスの GUID、ハードウェア ID、およびデバイスのデバイス クラスの情報。](#step2)
-   [**手順 3**— デバイス クラスやサブクラスでは、Windows ランタイムの USB API によって許可されているプロトコルを設定するかどうかを判断します。](#step3)
-   [**手順 4**-このチュートリアルでは拡張可能な基本的 Microsoft Visual Studio 2013 プロジェクトを作成します。](#step4)
-   [**手順 5**: アプリケーション マニフェストに追加の USB デバイスの機能です。](#step5)
-   [**手順 6**— 通信デバイス、アプリを拡張します。](#step6)
-   [**手順 7**-USB デバイスのレイアウトを調査します。(推奨)](#step7)
-   [**手順 8**— を取得し、UI での USB ディスクリプターを表示するアプリを拡張します。](#step8)
-   [**手順 9**-USB 制御転送のベンダ定義を送信するアプリを拡張します。](#step9)
-   [**手順 10**-一括データの読み書きにアプリを拡張します。](#step10)
-   [**手順 11**-ハードウェアの割り込みのデータを取得するアプリを拡張します。](#step11)
-   [**手順 12**— は現在アクティブでないインターフェイス設定を選択するアプリを拡張します。](#step12)
-   [**手順 13**-デバイスを閉じます。](#step13)
-   [**手順 14**-アプリのデバイス メタデータ パッケージを作成します。](#step14)
-   [**手順 15**-デバイスがシステムに接続されている場合、アプリが起動するように、自動再生のアクティブ化を実装するためにアプリを拡張します。](#step15)
-   [**手順 16.** -アプリの中断を取得することがなく、ファームウェアの更新など、デバイスに時間のかかる USB 転送を実行できるバック グラウンド タスクを実装するためにアプリを拡張します。](#step16)
-   [**手順 17**— Windows アプリ認定キットを実行します。](#step17)

## <a name="walkthroughwriting-uwp-app-for-usb-devices"></a>チュートリアル-USB デバイスの書き込みの UWP アプリ


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
<td><a href="" id="step1"></a>
<p><strong>手順 1.</strong>-デバイスのドライバーを関数として Microsoft が提供 WinUSB ドライバーをインストールします。</p></td>
<td><p><strong>クイック スタート:</strong><a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB (Winusb.sys) のインストール</a></p>
<p>次の方法で Winusb.sys をインストールすることができます。</p>
<ul>
<li>デバイスを接続するときにお気付き Windows がロードされる Winusb.sys 自動的にデバイスがあるため、 <a href="automatic-installation-of-winusb.md" data-raw-source="[WinUSB Device](automatic-installation-of-winusb.md)">WinUSB デバイス</a>します。</li>
<li>デバイス マネージャーで、システム指定のデバイス クラスを指定することで、ドライバーをインストールします。</li>
<li>カスタム INF を使用して、ドライバーをインストールします。 これら 2 つの方法のいずれかで、INF を取得できます。
<ul>
<li>ハードウェア ベンダーから、INF を取得します。</li>
<li>Microsoft 提供の Winusb.inf ファイルを参照するカスタム INF を記述します。 詳細については、次を参照してください。 <a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB (Winusb.sys) インストール</a>します。</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="" id="step2"></a>
<p><strong>手順 2</strong>-Get デバイス インターフェイスの GUID、ハードウェア ID、およびデバイスのデバイス クラスの情報。</p></td>
<td><p>その情報は、デバイスの製造元から入手できます。</p>
<ul>
<li><p><strong>ベンダーと製品の id</strong></p>
<p>デバイス マネージャーでは、デバイスのプロパティを表示します。 <strong>詳細</strong> タブで、表示、<strong>ハードウェア Id</strong>プロパティの値。 その値は、これら 2 つの識別子の組み合わせです。 たとえば、SuperMUTT デバイス、<strong>ハードウェア Id</strong> "USB\VID_045E & PID_F001"には、製造元 ID は"0x045E"; と製品 ID が"0xF001"。</p></li>
<li><strong>デバイス クラスやサブクラスでは、プロトコル コード</strong></li>
<li><strong>デバイス インターフェイスの GUID</strong></li>
</ul>
または、レジストリの情報を表示できます。 詳細については、次を参照してください。 <a href="usb-device-specific-registry-settings.md" data-raw-source="[USB Device Registry Entries](usb-device-specific-registry-settings.md)">USB デバイスのレジストリ エントリ</a>します。</td>
</tr>
<tr class="odd">
<td><a href="" id="step3"></a>
<p><strong>手順 3</strong>— デバイス クラスやサブクラスでは、Windows ランタイムの USB API によって許可されているプロトコルを設定するかどうかを判断します。</p></td>
<td><p>UWP アプリを記述するには、場合デバイス クラスやサブクラスでは、プロトコル、デバイスのコードは、次のいずれか。</p>
<ul>
<li><code>name:cdcControl,           classId:02 * *</code></li>
<li><code>name:physical, classId:05 * *</code></li>
<li><code>name:personalHealthcare,   classId:0f 00 00</code></li>
<li><code>name:activeSync,           classId:ef 01 01</code></li>
<li><code>name:palmSync,             classId:ef 01 02</code></li>
<li><code>name:deviceFirmwareUpdate, classId:fe 01 01</code></li>
<li><code>name:irda,                 classId:fe 02 00     </code></li>
<li><code>name:measurement,          classId:fe 03 *</code></li>
<li><code>name:vendorSpecific,       classId:ff * *</code></li>
</ul></td>
</tr>
<tr class="even">
<td><a href="" id="step4"></a>
<p><strong>手順 4</strong>-このチュートリアルでは拡張可能な基本的な Visual Studio 2013 プロジェクトを作成します。</p></td>
<td>詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?linkid=617681" data-raw-source="[Getting started with UWP apps](https://go.microsoft.com/fwlink/p/?linkid=617681)">UWP アプリの概要</a>します。</td>
</tr>
<tr class="odd">
<td><a href="" id="step5"></a>
<p><strong>手順 5</strong>: アプリケーション マニフェストに追加の USB デバイスの機能です。</p></td>
<td><p><strong>クイック スタート:</strong><a href="updating-the-app-manifest-with-usb-device-capabilities.md" data-raw-source="[How to add USB device capabilities to the app manifest](updating-the-app-manifest-with-usb-device-capabilities.md)">アプリケーション マニフェストに USB デバイスの機能を追加する方法</a></p>
<p>テキスト エディターで、Package.appxmanifest ファイルを開き、追加、 <a href="https://msdn.microsoft.com/library/windows/apps/br211430" data-raw-source="[&lt;strong&gt;DeviceCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br211430)"> <strong>DeviceCapability</strong> </a>を持つ要素<strong>名前</strong>属性は、この例で示すように"usb"に設定します。</p>
<div class="alert">
<strong>注</strong>  Visual Studio 2013 での USB デバイスの機能を変更することはできません。 Package.appxmanifest ファイルを右クリックする必要があります<strong>ソリューション エクスプ ローラー</strong>選択<strong>プログラムから開く.</strong>、し<strong>XML (テキスト) エディター</strong>します。 プレーンな XML では、ファイルが開きます。
</div>
<div>
 
</div>
<pre class="syntax" space="preserve"><code>&lt;Capabilities&gt;
      &lt;!--When the device's classId is FF * *, there is a predefined name for the class. 
          You can use the name instead of the class id. 
          There are also other predefined names that correspond to a classId.--&gt;
      &lt;m2:DeviceCapability Name="usb"&gt;
          &lt;!--SuperMutt Device--&gt;
          &lt;m2:Device Id="vidpid:045E 0611"&gt;
              &lt;!--&lt;wb:Function Type="classId:ff * *"/&gt;--&gt;
              &lt;m2:Function Type="name:vendorSpecific"/&gt;
          &lt;/m2:Device&gt;
      &lt;/m2:DeviceCapability&gt;
  &lt;/Capabilities&gt;</code></pre>
<div class="code">

</div>
<p><strong>サンプルにあります。</strong>Package.appxmanifest ファイルでは、USB デバイスの機能が追加されます。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step6"></a>
<p><strong>手順 6</strong>— 通信デバイス、アプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">USB デバイス (UWP アプリ) に接続する方法</a></p>
<ol>
<li>列挙されたデバイス コレクションにデバイスを検索するための検索条件を含む高度なクエリ構文 (AQS) 文字列を構築することにより、デバイスを検索します。</li>
<li>2 つの方法のいずれかで、デバイスを開きます。
<ul>
<li><p>AQS を渡して<a href="https://msdn.microsoft.com/library/windows/apps/br225432" data-raw-source="[&lt;strong&gt;FindAllAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225432)"> <strong>FindAllAsync</strong> </a>を取得し、 <a href="https://msdn.microsoft.com/library/windows/apps/br225393" data-raw-source="[&lt;strong&gt;DeviceInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225393)"> <strong>DeviceInformation</strong> </a>デバイスのオブジェクト。</p>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/apps/xaml/hh872189" data-raw-source="[Quickstart: enumerating commonly used devices](https://msdn.microsoft.com/library/windows/apps/xaml/hh872189)">クイック スタート: デバイスを使用する一般的な列挙</a>します。</p></li>
<li>使用して、 <a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>デバイスが追加またはシステムから削除されるタイミングを検出するオブジェクト。
<ol>
<li>渡すを AQS <a href="https://msdn.microsoft.com/library/windows/apps/br225427" data-raw-source="[&lt;strong&gt;CreateWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225427)"> <strong>CreateWatcher</strong> </a>を取得し、 <a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>オブジェクト。</li>
<li>イベント ハンドラーの登録、 <a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>オブジェクト。</li>
<li>取得、 <a href="https://msdn.microsoft.com/library/windows/apps/br225393" data-raw-source="[&lt;strong&gt;DeviceInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225393)"> <strong>DeviceInformation</strong> </a>でのデバイスのオブジェクト、 <a href="https://msdn.microsoft.com/library/windows/apps/br225450" data-raw-source="[&lt;strong&gt;Added&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225450)"> <strong>Added</strong> </a>イベント ハンドラー。</li>
<li>開始し、停止、 <a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>オブジェクト。</li>
</ol>
詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/apps/xaml/hh967756" data-raw-source="[How to get notifications if devices are added, removed, or changed](https://msdn.microsoft.com/library/windows/apps/xaml/hh967756)">デバイスを追加する場合に通知を取得する方法は、削除、または変更</a>します。</li>
</ul></li>
<li>デバイス インスタンスからの取得、 <a href="https://msdn.microsoft.com/library/windows/apps/br225437" data-raw-source="[&lt;strong&gt;DeviceInformation.Id&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225437)"> <strong>DeviceInformation.Id</strong> </a>プロパティ。</li>
<li>呼び出す<a href="https://msdn.microsoft.com/library/windows/apps/dn264010" data-raw-source="[&lt;strong&gt;FromIdAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264010)"> <strong>FromIdAsync</strong> </a>デバイス インスタンスの文字列と取得を渡すことによって、 <a href="https://msdn.microsoft.com/library/windows/apps/dn263883" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263883)"> <strong>UsbDevice</strong> </a>オブジェクト。</li>
</ol>
<p><strong>サンプルにあります。</strong>Scenario1_DeviceConnect という名前のファイルを参照してください。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step7"></a>
<p><strong>手順 7</strong>(推奨)-調査、 <a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB デバイス レイアウト</a>します。</p></td>
<td><p>デバイスを構成して、データ転送の実行についての基本的な USB 概念を確認:<a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">すべての USB 開発者の概念</a>します。</p>
<p>デバイスの構成記述子、各サポートされている代替設定のインターフェイスの記述子のエンドポイント記述子を表示します。 使用して<a href="https://go.microsoft.com/fwlink/p/?linkid=617721" data-raw-source="[USBView](https://go.microsoft.com/fwlink/p/?linkid=617721)">USBView</a>すべて USB コント ローラーを参照することができます、および USB デバイスが、それらに接続されているし、デバイスの構成を調べることもできます。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step8"></a>
<p><strong>手順 8</strong>— を取得し、UI での USB ディスクリプターを表示するアプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">USB ディスクリプター (UWP アプリ) を取得する方法</a></p>
<p></p>
<ul>
<li>デバイス記述子を取得することによって取得、 <a href="https://msdn.microsoft.com/library/windows/apps/dn264002" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264002)"> <strong>UsbDevice.DeviceDescriptor</strong> </a>値。</li>
<li>取得することによって構成記述子を取得、 <a href="https://msdn.microsoft.com/library/windows/apps/dn263799" data-raw-source="[&lt;strong&gt;UsbConfiguration.ConfigurationDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263799)"> <strong>UsbConfiguration.ConfigurationDescriptor</strong> </a>値。
<ul>
<li>取得することによって設定の完全な構成記述子を取得、 <a href="https://msdn.microsoft.com/library/windows/apps/dn263802" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263802)"> <strong>UsbConfiguration.Descriptors</strong> </a>プロパティ。</li>
</ul></li>
<li>取得することによって、構成内でインターフェイスの配列を取得、 <a href="https://msdn.microsoft.com/library/windows/apps/dn263808" data-raw-source="[&lt;strong&gt;UsbConfiguration.UsbInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263808)"> <strong>UsbConfiguration.UsbInterfaces</strong> </a>プロパティ。</li>
<li>取得することで別の設定の配列を取得する<a href="https://msdn.microsoft.com/library/windows/apps/dn264291" data-raw-source="[&lt;strong&gt;UsbInterface.InterfaceSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264291)"> <strong>UsbInterface.InterfaceSettings</strong></a>します。</li>
<li><p>アクティブな代替設定内では、パイプを列挙し、関連付けられているエンドポイントを取得します。</p>
<p>エンドポイントの記述子は、これらのオブジェクトによって表されます。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn297543" data-raw-source="[&lt;strong&gt;UsbBulkInEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297543)"><strong>UsbBulkInEndpointDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn297619" data-raw-source="[&lt;strong&gt;UsbBulkOutEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297619)"><strong>UsbBulkOutEndpointDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn264294" data-raw-source="[&lt;strong&gt;UsbInterruptInEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264294)"><strong>UsbInterruptInEndpointDescriptor</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn278420" data-raw-source="[&lt;strong&gt;UsbInterruptOutEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278420)"><strong>UsbInterruptOutEndpointDescriptor</strong></a></li>
</ul></li>
</ul>
<p><strong>サンプルにあります。</strong>Scenario5_UsbDescriptors という名前のファイルを参照してください。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step9"></a>
<p><strong>手順 9</strong>-USB 制御転送のベンダ定義を送信するアプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer request (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">USB 制御転送要求 (UWP アプリ) を送信する方法</a></p>
<p></p>
<ol>
<li>デバイスのハードウェア仕様から仕入先のコマンドを取得します。</li>
<li>作成、 <a href="https://msdn.microsoft.com/library/windows/apps/dn278431" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278431)"> <strong>UsbSetupPacket</strong> </a>オブジェクトし、さまざまなプロパティを設定して、セットアップのパケットを設定します。</li>
<li>送信転送の方向に応じて、これらのメソッドが制御を転送する非同期操作を開始します。
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn264027" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264027)"><strong>SendControlInTransferAsync</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/apps/dn264044" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264044)"><strong>SendControlOutTransferAsync</strong></a></li>
</ul></li>
</ol>
<p><strong>サンプルにあります。</strong>Scenario2_ControlTransfer という名前のファイルを参照してください。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step10"></a>
<p><strong>手順 10</strong>-一括データの読み書きにアプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">USB 一括転送要求 (UWP アプリ) を送信する方法</a></p>
<p></p>
<ol>
<li>一括パイプ オブジェクトを取得する (<a href="https://msdn.microsoft.com/library/windows/apps/dn297647" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297647)"><strong>UsbBulkOutPipe</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/apps/dn297573" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297573)"> <strong>UsbBulkInPipe</strong></a>)。</li>
<li>ポリシー パラメーターを設定する一括パイプを構成します。</li>
<li>使用して、データ ストリームのセットアップ、 <a href="https://msdn.microsoft.com/library/windows/apps/br208119" data-raw-source="[&lt;strong&gt;DataReader&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208119)"> <strong>DataReader</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/apps/br208154" data-raw-source="[&lt;strong&gt;DataWriter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208154)"> <strong>datawriter の各</strong></a>オブジェクト。</li>
<li>非同期転送操作を呼び出すことによって開始<a href="https://msdn.microsoft.com/library/windows/apps/br208135" data-raw-source="[&lt;strong&gt;DataReader.LoadAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208135)"> <strong>DataReader.LoadAsync</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/apps/br208171" data-raw-source="[&lt;strong&gt;DataWriter.StoreAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br208171)"> <strong>DataWriter.StoreAsync</strong></a>します。</li>
<li>転送操作の結果を取得します。</li>
</ol>
<p><strong>サンプルにあります。</strong>Scenario4_BulkPipes という名前のファイルを参照してください。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step11"></a>
<p><strong>手順 11</strong>-ハードウェアの割り込みのデータを取得するアプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">USB 割り込み転送要求 (UWP アプリ) を送信する方法</a></p>
<p></p>
<ol>
<li>割り込みパイプ オブジェクトを取得する (<a href="https://msdn.microsoft.com/library/windows/apps/dn278416" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278416)"><strong>UsbInterruptInPipe</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/apps/dn278425" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278425)"> <strong>UsbInterruptOutPipe</strong></a>)。</li>
<li>割り込みハンドラーを実装、 <a href="https://msdn.microsoft.com/library/windows/apps/dn278418" data-raw-source="[&lt;strong&gt;DataReceived&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278418)"> <strong>DataReceived</strong> </a>イベント。</li>
<li>データの受信を開始するイベント ハンドラーを登録します。</li>
<li>データの受信を停止するイベント ハンドラーの登録を解除します。</li>
</ol>
<p><strong>サンプルにあります。</strong>Scenario3_InterruptPipes という名前のファイルを参照してください。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step12"></a>
<p><strong>手順 12</strong>— は現在アクティブでないインターフェイス設定を選択するアプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">USB インターフェイスの設定 (UWP アプリ) を選択する方法</a></p>
<p>デバイスが通信に開かれると、既定のインターフェイスとその最初の設定が選択されます。 設定を変更する場合は、次の手順に従います。</p>
<ol>
<li>使用してアクティブな USB インターフェイスの設定を取得、 <a href="https://msdn.microsoft.com/library/windows/apps/dn264285" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Selected&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264285)"> <strong>UsbInterfaceSetting.Selected</strong> </a>値。</li>
<li>呼び出して非同期操作を開始して、USB インターフェイスの設定を設定<a href="https://msdn.microsoft.com/library/windows/apps/dn264286" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264286)"> <strong>UsbInterfaceSetting.SelectSettingAsync</strong></a>します。</li>
</ol></td>
</tr>
<tr class="odd">
<td><a href="" id="step13"></a>
<p><strong>手順 13</strong>-デバイスを閉じます。</p></td>
<td><p><strong>クイック スタート:</strong><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">USB デバイス (UWP アプリ) に接続する方法</a></p>
<p>UsbDevice オブジェクトを使用して完了した後、デバイスを閉じます。</p>
<p>C++ アプリを使用して参照を解放する必要があります、<strong>削除</strong>キーワード。 C#または VB のアプリを呼び出す必要があります、 <a href="https://msdn.microsoft.com/library/windows/apps/dn264007" data-raw-source="[&lt;strong&gt;UsbDevice.Dispose&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264007)"> <strong>UsbDevice.Dispose</strong> </a>メソッド。 JavaScript アプリを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/apps/dn263990" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263990)"> <strong>UsbDevice.Close</strong></a>します。</p>
<p><strong>サンプルにあります。</strong>Scenario1_DeviceConnect という名前のファイルを参照してください。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step14"></a>
<p><strong>手順 14</strong>-アプリのデバイス メタデータ パッケージを作成します。</p></td>
<td><strong>ツール:</strong><a href="https://msdn.microsoft.com/library/windows/hardware/hh454213" data-raw-source="[Device Metadata Authoring Wizard](https://msdn.microsoft.com/library/windows/hardware/hh454213)">デバイス メタデータの作成ウィザード</a>
<ul>
<li>Windows Driver Kit (WDK) のインストールがある場合は開く<strong>ドライバー</strong> &gt; <strong>デバイス メタデータ</strong> &gt; <strong>Authoring</strong>します。</li>
<li>スタンドアロン SDK をインストールした場合、ツールは <em>&lt;install_path&gt;</em>\bin\x86\DeviceMetadataWizardexe します。</li>
</ul>
<p>アプリをウィザードの手順に従って、デバイスに関連付けます。 このデバイスの情報を入力します。</p>
<p></p>
<ul>
<li><strong>デバイス情報</strong>ページで、入力<strong>モデル名</strong>、<strong>製造元</strong>、および<strong>説明</strong>します。</li>
<li><strong>ハードウェア情報</strong> ページで、デバイスのハードウェア ID を入力します。</li>
</ul>
<p><strong>デバイスの特権を持つアプリとしてアプリを宣言するには、次の手順を実行します。</strong></p>
<ol>
<li><p><strong>アプリ情報</strong>] ページの [、<strong>特権付きアプリケーション</strong>グループで、入力、<strong>パッケージ名</strong>、<strong>パブリッシャー名</strong>、および<strong>UWP アプリ ID</strong>します。</p>
<p><img src="images/privileged-app.png" alt="device metatdata for privileged apps" /></p>
<div class="alert">
<strong>注</strong>  チェックを行わない、 <strong>Access カスタム ドライバー</strong>オプション。
</div>
<div>
 
</div></li>
<li>開く、<strong>完了</strong>タブ。選択、<strong>システムのローカル メタデータ ストアにパッケージをコピー</strong>チェック ボックスをオンします。</li>
<li>コントロール パネルを開いて、デバイス接続<strong>デバイスとプリンターの表示</strong>し、デバイスのアイコンが正しいことを確認します。</li>
</ol>
<p><strong>サンプルにあります。</strong>DeviceMetadata フォルダーを参照してください。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step15"></a>
<p><strong>手順 15</strong>-デバイスがシステムに接続されている場合、アプリが起動するように、自動再生のアクティブ化を実装するためにアプリを拡張します。</p></td>
<td><p><strong>クイック スタート:</strong><a href="https://msdn.microsoft.com/library/windows/apps/xaml/jj161017" data-raw-source="[Register an app for an AutoPlay device](https://msdn.microsoft.com/library/windows/apps/xaml/jj161017)">自動再生デバイスのアプリを登録します。</a></p>
<p>デバイスがシステムに接続されている場合、そのアプリが起動されるため、自動再生機能を追加できます。 (特権またはそれ以外の場合) のすべての UWP アプリの自動再生を有効にすることができます。</p>
<p></p>
<ol>
<li>デバイス メタデータ パッケージをデバイスが自動再生通知に応答する方法を指定する必要があります。 <strong>Windows 情報</strong>] タブで、[、 <strong>UWP デバイス アプリ</strong>オプションし、次に示すようにアプリの情報を入力します。</li>
<li><p>アプリ マニフェストで追加<strong>自動再生デバイス</strong>次に示すように、宣言と起動情報。</p>
<p><img src="images/autoplay.png" alt="AutoPlay" /></p></li>
<li>App クラスの OnActivated メソッドで、アプリがデバイスでアクティブ化を確認します。 である場合、メソッドを含む DeviceEventArgs パラメーター値を受け取る、 <a href="https://msdn.microsoft.com/library/windows/apps/br225437" data-raw-source="[&lt;strong&gt;DeviceInformation.Id&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225437)"> <strong>DeviceInformation.Id</strong> </a>プロパティの値。 これは、同じ値で説明されている<a href="#step6" data-raw-source="[&lt;strong&gt;Step 6&lt;/strong&gt;—Extend the app to open the device for communication](#step6)"><strong>手順 6</strong>— 通信デバイス、アプリを拡張</a>します。</li>
</ol>
<p><strong>サンプルにあります。</strong>自動再生をという名前のファイルを参照してください。 JavaScript、default.js を参照してください。</p></td>
</tr>
<tr class="even">
<td><a href="" id="step16"></a>
<p><strong>手順 16.</strong>-アプリの中断を取得することがなく、ファームウェアの更新など、デバイスへの長さの転送を実行できるバック グラウンド タスクを実装するためにアプリを拡張します。</p></td>
<td><p>バック グラウンド タスクを実装するために、2 つのクラスを作成する必要があります。</p>
<p>バック グラウンド タスク クラスの実装、 <a href="https://msdn.microsoft.com/library/windows/apps/br224794" data-raw-source="[&lt;strong&gt;IBackgroundTask&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br224794)"> <strong>IBackgroundTask</strong> </a>インターフェイスし、実際のコードいずれかの同期を作成または更新を周辺機器にはが含まれています。 バック グラウンド タスクのクラスは、バック グラウンド タスクがトリガーされたときと、アプリのアプリケーション マニフェストで指定されたエントリ ポイントから実行されます。</p>
<div class="alert">
<strong>注</strong>Windows 8.1 で提供されるデバイスのバック グラウンド タスク インフラストラクチャ。 詳細については、Windows はバック グラウンド タスクを参照してください<a href="https://msdn.microsoft.com/library/windows/apps/xaml/hh977056" data-raw-source="[Supporting your app with background tasks](https://msdn.microsoft.com/library/windows/apps/xaml/hh977056)">バック グラウンド タスクを使用してアプリをサポートしている</a>します。
</div>
<div>
 
</div>
<p><strong>バック グラウンド タスク クラス</strong></p>
<ol>
<li>実装、 <a href="https://msdn.microsoft.com/library/windows/apps/br224794" data-raw-source="[&lt;strong&gt;IBackgroundTask&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br224794)"> <strong>IBackgroundTask</strong> </a> Windows のバック グラウンド タスクのインフラストラクチャで必要なインターフェイスです。</li>
<li>クラスに渡される DeviceUseDetails インスタンスを取得、<strong>実行</strong>進行状況を報告するには、このインスタンスがキャンセル イベントを登録して、Microsoft Store アプリをバックアップ メソッドを使用します。</li>
<li><strong>実行</strong>メソッドもデバイスのバック グラウンド同期コードを実装するプライベート OpenDevice と WriteToDeviceAsync メソッドを呼び出します。</li>
</ol>
<p>UWP アプリでは、登録し、DeviceUseTrigger のバック グラウンド タスクをトリガーします。 アプリでは、ユーザー登録をトリガー、および、バック グラウンド タスクの進行状況を処理します。</p>
<div class="alert">
<strong>注</strong>  DeviceServicingTrigger バック グラウンドに次の手順を適用できることの例のコード タスクを使用して、対応するオブジェクト。 2 つのトリガーのオブジェクトとその対応する Api の唯一の違いは、Windows によって行われたポリシーのチェックです。
</div>
<div>
 
</div>
<ol>
<li>DeviceUseTrigger および BackgroundTaskRegistration オブジェクトを作成します。</li>
<li>任意のバック グラウンド タスクは、このサンプル アプリケーションで登録されていたし、タスクで登録解除メソッドを呼び出すことによってキャンセルされ、かどうかを確認します。</li>
<li>デバイスを同期するバック グラウンド タスクを登録します。 SetupBackgroundTask メソッドは、次の手順で SyncWithDeviceAsync メソッドから呼び出されます。
<ol>
<li>DeviceUseTrigger を初期化し、後で使用するために保存します。</li>
<li>BackgroundTaskBuilder オブジェクトを作成し、Name、TaskEntryPoint SetTrigger プロパティとメソッドを使用して、アプリの DeviceUseTrigger オブジェクトとバック グラウンド タスクの名前を登録します。 オブジェクト BackgroundTaskBuilder の TaskEntryPoint プロパティは、バック グラウンド タスクがトリガーされたときに実行されるバック グラウンド タスク クラスの完全名に設定されます。</li>
<li>入力候補および Microsoft Store アプリをユーザーに入力候補および進行状況の更新を提供できるように、バック グラウンド タスクから進行状況イベントを登録します。</li>
</ol></li>
<li>プライベート SyncWithDeviceAsync メソッドは、デバイスと同期して、バック グラウンド同期を開始するバック グラウンド タスクを登録します。
<ol>
<li>前の手順から SetupBackgroundTask メソッドの呼び出しし、デバイスを同期するバック グラウンド タスクを登録します。</li>
<li>バック グラウンド タスクを開始するプライベート StartSyncBackgroundTaskAsync メソッドを呼び出します。</li>
<li>バック グラウンド タスクが開始時にデバイスを開くことがあることを確認するデバイスにアプリのハンドルを閉じます。
<div class="alert">
<strong>注</strong>  バック グラウンド タスクを RequestAsync を呼び出す前に、Microsoft Store アプリがデバイスへの接続を閉じる必要がありますので、更新プログラムを実行するデバイスを開く必要があります
</div>
<div>
 
</div></li>
<li>バック グラウンド タスクとバック グラウンド タスクが正常に開始するかどうかを判断するために使用 RequestAsync から DeviceTriggerResults オブジェクトを返します。 は、トリガーを起動する DeviceUseTrigger オブジェクトの RequestAsync メソッドを呼び出します。
<div class="alert">
<strong>注</strong>  Windows をチェックして、すべての必要なタスクの開始に使用ポリシーは、完了したことを確認します。 すべてのポリシーのチェックが完了した場合、操作が進行中に安全に中断するアプリを許可する、Microsoft Store アプリの外部でバック グラウンド タスクとして、更新操作が実行されているようになりました。 Windows はまた、ランタイムの要件を強制し、それらの要件が満たされた不要になった場合は、バック グラウンド タスクをキャンセルします。
</div>
<div>
 
</div></li>
<li>StartSyncBackgroundTaskAsync から返された DeviceTriggerResults オブジェクトを使用して、バック グラウンド タスクが正常に開始されましたかを判断します。 Switch ステートメントは、DeviceTriggerResults から結果を検査に使用されます。</li>
</ol></li>
<li>バック グラウンド タスクからの進行状況でアプリの UI を更新するプライベート OnSyncWithDeviceProgress イベント ハンドラーを実装します。</li>
<li>バック グラウンド タスクが完了したときに、バック グラウンド タスクからフォア グラウンド アプリへの移行を処理するためにプライベート OnSyncWithDeviceCompleted イベント ハンドラーを実装します。
<ol>
<li>BackgroundTaskCompletedEventArgs オブジェクトの CheckResults メソッドを使用して、バック グラウンド タスクによって例外がスローされたかどうかを判断します。</li>
<li>これで、バック グラウンド タスクが完了し、ユーザーに通知する UI が更新されるアプリはフォア グラウンド アプリによって使用のデバイスを再度開かれます。</li>
</ol></li>
<li>実装のプライベート ボタンのクリックしてイベント ハンドラーを起動し、バック グラウンド タスクの取り消し、UI から。
<ol>
<li>プライベート Sync_Click イベント ハンドラーは、前の手順で説明されている SyncWithDeviceAsync メソッドを呼び出します。</li>
<li>プライベート CancelSync_Click イベント ハンドラーでは、バック グラウンド タスクをキャンセルするプライベート CancelSyncWithDevice メソッドを呼び出します。</li>
</ol></li>
<li>プライベート CancelSyncWithDevice メソッドは、登録を解除し、BackgroundTaskRegistration オブジェクトを登録解除メソッドを使用して、デバイスを再度開くことができますので、任意のアクティブなデバイスの同期をキャンセルします。</li>
</ol>
<p><strong>サンプルにあります。</strong>Scenario7_Sync ファイルという名前のファイルを参照してください。 バック グラウンド クラスは、IoSyncBackgroundTask に実装されます。</p></td>
</tr>
<tr class="odd">
<td><a href="" id="step17"></a>
<p><strong>手順 17</strong>— Windows アプリ認定キットを実行します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/hh694081" data-raw-source="[Using the Windows App Certification Kit](https://msdn.microsoft.com/library/windows/apps/hh694081)">Windows アプリ認定キットの使用</a></p>
<p>推奨。 Windows アプリ認定キットを実行すると、主要な機能をアプリに追加したときにこれ行う必要がありますので、アプリが Microsoft Store の要件を満たしていることを確認できます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="want-to-know-more"></a>その他の情報


その他の関連するサンプルについて説明します。

**関連するサンプル**

-   [USB CDC コントロールのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [ファームウェアの更新プログラムの USB デバイスのサンプル](https://go.microsoft.com/fwlink/p/?linkid=309716)

[UWP アプリケーションの UI での開始 (XAML) を完了するには](https://msdn.microsoft.com/library/windows/apps/xaml/dn263191)

UWP アプリ UI の設計について説明します。

[使用して UWP アプリのためのロードマップC#および Visual Basic](https://msdn.microsoft.com/library/windows/apps/br229583)と[C++ を使った UWP アプリのためのロードマップ](https://msdn.microsoft.com/library/windows/apps/hh700360)

C++ を使用する UWP アプリを作成する方法の詳細はC#、または一般的な Visual Basic です。

[非同期プログラミング (UWP アプリ)](https://msdn.microsoft.com/library/windows/apps/hh464924)

拡張の時間の長さは機能するときに、応答性の高い状態を維持がかかる場合があります、アプリを作成する方法について説明します。

 

 





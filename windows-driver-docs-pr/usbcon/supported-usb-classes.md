---
Description: このトピックでは、サポートされている USB デバイスクラス用の Microsoft 提供のドライバーの一覧を示します。
title: Windows に含まれる USB デバイス クラス ドライバー
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: f60f7ce8283bb6710ac2803abf49dd518ec2c537
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007645"
---
# <a name="usb-device-class-drivers-included-in-windows"></a>Windows に含まれる USB デバイス クラス ドライバー

このトピックでは、サポートされている USB デバイスクラス用の Microsoft 提供のドライバーの一覧を示します。

- Microsoft 提供の USB 用ドライバー-承認されたデバイスクラス。
- 複合デバイスの場合は、各機能に物理デバイスオブジェクト (PDOs) を作成する[USB 汎用親ドライバー (Usbccgp)](usb-common-class-generic-parent-driver.md)を使用します。
- 非複合デバイスまたは複合デバイスの機能については、 [winusb (winusb .sys)](winusb.md)を使用します。

**USB ドライバーをインストールする場合:** USB デバイスクラスドライバーをダウンロードする必要はありません。 これらは自動的にインストールされます。 これらのドライバーとそのインストールファイルは、Windows に含まれています。 これらのファイルは、@no__t 0Windows @ no__t-1System32 @ no__t-2DriverStore @ no__t-3FileRepository フォルダーにあります。 ドライバーは Windows Update によって更新されます。

**カスタムドライバーを作成する場合は、次のようにします。** USB デバイス用のドライバーを作成する前に、Microsoft 提供のドライバーがデバイス要件を満たしているかどうかを確認します。 デバイスが属する USB デバイスクラスで Microsoft 提供のドライバーを使用できない場合は、汎用ドライバーである Winusb. sys または Usbccgp を使用することを検討してください。 必要な場合にのみドライバーを記述します。 [USB クライアントドライバーを開発するためのドライバーモデルの選択](winusb-considerations.md)には、さらに多くのガイドラインが含まれています。

## <a name="usb-device-classes"></a>USB デバイスクラス

*USB デバイスクラス*は、類似した特性を持つデバイスのカテゴリであり、共通の機能を実行します。 これらのクラスとその仕様は、USB IF によって定義されます。 各デバイスクラスは USB によって識別されます。承認されたクラス、サブクラス、およびプロトコルコードは、ファームウェアのデバイス記述子に IHV によって提供されます。 Microsoft では、 *USB デバイスクラスドライバー*と呼ばれるいくつかのデバイスクラス用にインボックスドライバーを提供しています。 サポートされているデバイスクラスに属するデバイスがシステムに接続されている場合は、Windows によってクラスドライバーが自動的に読み込まれ、追加のドライバーを必要としないデバイス機能が自動的に読み込まれます。

ハードウェアベンダーは、サポートされているデバイスクラスのドライバーを作成しないでください。 Windows クラスのドライバーでは、クラスの仕様で説明されているすべての機能がサポートされていない場合があります。 デバイスの機能の一部がクラスドライバーによって実装されていない場合、ベンダーは、デバイスによって提供される機能の範囲全体をサポートするために、クラスドライバーと連携する補助ドライバーを提供する必要があります。

USB に関する一般的な情報-承認されたデバイスクラスについては、「 [Usb テクノロジ](https://www.usb.org/developers/defined_class/)」 web サイトを参照してください。

USB クラスの仕様とクラスコードの現在の一覧については、 [USB DWG の web サイト](https://www.usb.org/about/dwg_charter/)を参照してください。

## <a name="device-setup-classes"></a>デバイスセットアップクラス

Windows では、デバイスの機能を示すデバイス*セットアップクラス*によってデバイスが分類されます。

Microsoft では、ほとんどのデバイスのセットアップクラスを定義しています。 Ihv と Oem は、新しいデバイスセットアップクラスを定義できますが、既存のクラスが適用されていない場合に限ります。 詳細については、「[システム定義のデバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))」を参照してください。

USB デバイス用の2つの重要なデバイスセットアップクラスは次のとおりです。

- **Usbdevice** {88 Bae032-5a81-49F0-bc3de4ff138216d6}:Ihv は、別のクラスに属していないカスタムデバイスに対して、このクラスを使用する必要があります。 このクラスは、USB ホストコントローラーおよびハブでは使用されません。

- **USB** {36fc9e60-c465-11cf-8056-444553540000}:Ihv は、カスタムデバイスにこのクラスを使用することはできません。 これは、USB ホストコントローラーおよび USB ハブ用に予約されています。

デバイスのセットアップクラスは、前に説明した USB デバイスクラスとは異なります。 たとえば、オーディオデバイスは、その記述子に01h という USB デバイスクラスコードを持っています。 システムに接続されている場合、Windows は、Microsoft が提供する、Usbaudio を読み込みます。 デバイスマネージャーでは、デバイスは **[サウンド、ビデオ、およびゲームコントローラー]** の下に表示されます。これは、デバイスセットアップクラスがメディアであることを示します。

## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供の USB デバイスクラスドライバー

<table>
  <thead>
    <tr>
      <th>USB-IF クラスコード</th>
      <th>デバイスセットアップクラス</th>
      <th>Microsoft 提供のドライバーおよび INF</th>
      <th>Windows のサポート</th>
     <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>オーディオ (01h)</td>
      <td><strong>メディア</strong></br>
{4d36e96c-e325-11ce-bfc1-08002be10318}</td>
      <td>Usbaudio. sys<p>Wdma\_usb.inf</p></td>
      <td>Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、Usbaudio ドライバーを使用して USB オーディオデバイスクラスをサポートしています。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components">カーネルモード WDM オーディオコンポーネント</a>」の「Usbaudio クラスシステムドライバー」を参照してください。 Windows audio のサポートの詳細については、Windows web サイト<a href="https://go.microsoft.com/fwlink/p/?linkid=8751">のオーディオデバイステクノロジ</a>に関する web サイトを参照してください。</td>
    </tr>
    <tr>
      <td rowspan="4">通信と CDC 制御 (02h)</td>
        <tr>
        <td><strong>シリアル</strong></br>{4D36E978-E325-11CE-BFC1-08002BE10318}</td>
        <td>Usbser</br>Usbser</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</td>
        <td>Windows 10 では、Usbser を関数ドライバーとして自動的に読み込む新しい INF (Usbser) が追加されました。<p>詳細については、「 <a href="usb-driver-installation-based-on-compatible-ids.md">USB シリアルドライバー (Usbser)</a> 」を参照してください。</p></td>
      </tr>
      <tr>
        <td><strong>内蔵</strong></br>{4D36E96D-E325-11CE-BFC1-08002BE10318}<p>
        <strong>Note @ no__t はサブクラス 02h (ACM) をサポートしています</td>
        <td>Usbser</br>Mdmcpq を参照するカスタム INF</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Windows 8.1 以前のバージョンでは、Usbser は自動的には読み込まれません。 ドライバーを読み込むには、モデム INF (mdmcpq) を参照する INF を作成する必要があります。この INF には、@no__t 0Install @ no__t-1 と \[Needs が必要です。<p>Windows Vista 以降では、「<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md">ワイヤレスモバイル通信デバイスクラスのサポート</a>」で説明されているように、レジストリ値を設定して Cdc および WIRELESS Mobile CDC (wmcdc) のサポートを有効にすることができます。<p>CDC サポートが有効になっている場合、 <a href="usb-common-class-generic-parent-driver.md">USB 共通クラスの汎用親ドライバー</a>は、CDC および Wmcdc 制御モデルに対応するインターフェイスコレクションを列挙し、物理デバイスオブジェクト (PDO) をこれらのコレクションに割り当てます。</td>
      </tr>
      <tr>
        <td><strong>Net</strong></br>{4d36e972-e325-11ce-bfc1-08002be10318}</br><strong>メモ</strong>  サブクラス 0Eh (MBIM) をサポートします。</td>
        <td>wmbclass.sys</br>Netwmbclass .inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</td>
        <td>Windows 8 以降では、モバイルブロードバンドデバイス用の wmbclass .sys ドライバーが Microsoft によって提供されています。 「 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/mb-interface-model">MB インターフェイスモデル</a>」を参照してください。
</td>
      </tr>
      <tr>
        <td>HID (ヒューマンインターフェイスデバイス) (03h)</td>
        <td><strong>HIDClass</strong></br>{745a17a0-74d3-11d0-b6fe-00a0c90f57da}</td>
        <td>Hidclass</br>Hidusb .sys</br>入力 .inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Microsoft は、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=761243">USB Hid 標準</a>に準拠したデバイスを操作するために、hid クラスドライバー (Hidclass) と miniclass ドライバー (hidusb .sys) を提供しています。 詳細については、「 <a href="https://docs.microsoft.com/previous-versions/jj126193(v=vs.85)">Hid Architecture</a> and<a href="https://docs.microsoft.com/windows-hardware/drivers/hid/minidriver-operations">ミニドライバー」と「hid class driver</a>」を参照してください。 入力ハードウェアの Windows サポートの詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=8709">入力と HID のアーキテクチャおよびドライバーのサポート</a>に関する web サイトを参照してください。</td>
      </tr>
      <tr>
        <td>物理 (05h)</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>推奨されるドライバー:<a href="winusb.md">Winusb (winusb .sys)</a>
</td>
      </tr>
    <tr>
      <td>イメージ (06h)</td>
      <td><strong>イメージ</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbscan .sys</br>Sti</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、Windows XP 以降のオペレーティングシステムの USB デジタルカメラとスキャナーを管理する Usbscan .sys ドライバーを提供しています。 このドライバーは、Windows Imaging Architecture (WIA) の USB コンポーネントを実装しています。 WIA の詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers">Windows イメージ取得ドライバー</a> 」および「 <a href="https://go.microsoft.com/fwlink/p/?linkid=8768">windows Imaging Component</a> 」 web サイトを参照してください。 WIA で再生されるロールの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-core-components">Wia コアコンポーネント</a>」を参照してください。</td>
    </tr>
    <tr>
      <td>プリンター (07h)</td>
      <td><strong>USB</strong><p><strong>注</strong>   usbprint は、デバイスセットアップクラスでプリンターデバイスを列挙します。<strong>業者</strong><p> {4d36e979-e325-11ce-bfc1-08002be10318}.</td>
      <td>Usbprint .sys</br>Usbprint .inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft には、USB プリンターを管理する Usbprint .sys クラスドライバーが用意されています。 Windows での printer クラスの実装の詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=8764">印刷-アーキテクチャとドライバーのサポート</a>」 web サイトを参照してください。</td>
    </tr>
    <tr>
      <td rowspan="3">大容量記憶装置 (08h)</td>
        <tr>
          <td><strong>USB</strong></td>
          <td>Usbstor.sys</td>
          <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft は、Microsoft のネイティブストレージクラスドライバーを使用して USB 大容量記憶装置を管理するための Usbstor.sys ポートドライバーを提供しています。 このドライバーによって管理されるデバイススタックの例については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device">USB 大容量記憶装置のデバイスオブジェクトの例</a>」を参照してください。 Windows ストレージサポートの詳細については、「 <a href="https://go.microsoft.com/fwlink/p/?linkid=8766">Storage Technologies</a> 」 web サイトを参照してください。</td>
        </tr>
        <tr>
         <td><strong>SCSIAdapter</strong><p>{4d36e97b-e325-11ce-bfc1-08002be10318}</td>
         <td>サブクラス (06) とプロトコル (62)</br>Uaspstor</br>Uaspstor</td>
         <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</td>
         <td>Uaspstor は、一括ストリームエンドポイントをサポートする SuperSpeed USB デバイス用のクラスドライバーです。 詳しくは、次のトピックをご覧ください。 <ul>
           <li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/design/dn642103(v=vs.85)">XHCI で UASP ストレージドライバーをクラスドライバーとして読み込む</a></li><li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/design/dn642113(v=vs.85)">USB 接続 SCSI (UAS) の Windows 8 のベストプラクティス</li></ul></td>
        </tr>
    </tr>
    <tr>
      <td rowspan="3">Hub (09h)</td>
      <td rowspan="3"><strong>USB</strong><p>{36fc9e60-c465-11cf-8056-444553540000}</td>
      <tr>
      <td>Usbhub</br>Usb .inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft は、USB ハブを管理するための Usbhub ドライバーを提供しています。 ハブクラスドライバーと USB スタックの関係の詳細については、「 <a href="usb-3-0-driver-stack-architecture.md">Windows の usb ホスト側ドライバー</a>」を参照してください。
        </td>
      <tr>
      <td>Usbhub3</br>Usbhub3</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</td>
      <td>Microsoft では、SuperSpeed (USB 3.0) USB ハブを管理するための Usbhub3 ドライバーを提供しています。<p>ドライバーは、SuperSpeed hub が xHCI コントローラーに接続されているときに読み込まれます。 「 <a href="usb-3-0-driver-stack-architecture.md">Windows での USB ホスト側ドライバー」を</a>参照してください。</td>
        </tr>
      </tr>
    </tr>
     <tr>
      <td>CDC-データ (0Ah)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb .sys)</a></td>
    </tr>
     <tr>
      <td rowspan="3">スマートカード (0Bh)</td>
      <td rowspan="3"><strong>SmartCardReader</strong><p>{50dd5230-ba8a-11d1-bf5d-0000f805f530}</td>
        <tr>
          <td>Usbccid .sys (Obsolete)</td>
          <td>Windows 10 デスクトップ エディション</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft は、USB スマートカードリーダーを管理するための Usbccid のミニクラスドライバーを提供しています。 Windows のスマートカードドライバーの詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/smartcard/index">スマートカード設計ガイド</a>」を参照してください。
          <p>Windows Server 2003、Windows XP、および Windows 2000 では、オペレーティングシステムよりも後にリリースされている可能性があるため、このドライバーを読み込むには特別な指示が必要です。<p>
          <strong>Note @ no__t-1 Usbccid. sys ドライバーは、UMDF driver, WUDFUsbccidDriver に置き換えられました。</td>
          </tr>
         <tr>
           <td>WUDFUsbccidDriver</br>WUDFUsbccidDriver</td>
           <td>Windows 8.1</br>Windows 8</td>
           <td>WUDFUsbccidDriver は、USB CCID スマートカードリーダーデバイス用のユーザーモードドライバーです。</td>
         </tr>
       </tr>
       <tr>
      <td>コンテンツセキュリティ (0Dh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="usb-common-class-generic-parent-driver.md">USB 汎用親ドライバー (Usbccgp)</a>。 一部のコンテンツセキュリティ機能は、Usbccgp で実装されています。 「 <a href="content-security-features-in-the-composite-client-generic-parent-drive.md">Usbccgp のコンテンツセキュリティ機能」を</a>参照してください。</td>
        </tr>
    </tr>
     <tr>
      <td>ビデオ (0Eh)</td>
      <td><strong>イメージ</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbvideo. sys<p>
Usbvideo-.inf</td>
      <td>Windows 10 デスクトップ エディション<p>Windows Vista</td>
      <td>Microsoft では、usbvideo ドライバーを使用して USB ビデオクラスサポートを提供しています。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-minidrivers-design-guide">Avstream ミニドライバー</a>」の「USB Video Class Driver」を参照してください。
      <p>Windows XP では、オペレーティングシステムより後にリリースされている可能性があるため、このドライバーを読み込むには特別な指示が必要です。</td>
    </tr>
     <tr>
      <td>個人の医療 (0Fh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb .sys)</a></td>
     </tr>
     <tr>
      <td>オーディオ/ビデオデバイス (10h)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>     <tr>
      <td>診断デバイス (DCh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb .sys)</a></td>
    </tr>     <tr>
      <td>ワイヤレスコントローラー (E0h) <p><strong>注</strong>   ではサブクラス01h とプロトコル01h がサポートされています</td>
      <td>Bluetooth<p>{e0cbf06c-cd8b-4647-bb8a-263b43f0f974}</td>
      <td>Bthusb .sys<p>Bth .inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Microsoft は、USB Bluetooth ラジオを管理するための Bthusb .sys ミニポートドライバーを提供しています。 詳細については、「 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536596(v=vs.85)">Bluetooth 設計ガイド</a>」を参照してください。</td>
    </tr>     <tr>
      <td>その他 (EFh)</td>
      <td><strong>Net</strong><p>
{4d36e972-e325-11ce-bfc1-08002be10318}<p><strong>注</strong>   ではサブクラス04h とプロトコル01h がサポートされています</td>
      <td>Rndismp</br>Rndismp</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Windows Vista より前の場合、CDC のサポートは、ベンダー固有のプロトコル (<strong>Binterfaceprotocol</strong>) 値が0Xff の抽象コントロールモデル (ACM) の RNDIS 固有の実装に限定されます。 RNDIS 施設は、すべての802スタイルのネットワークカードの管理を1つのクラスドライバー Rndismp にセンターで行います。 リモート NDIS の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-remote-ndis--rndis-">リモート ndis の概要</a>」を参照してください。 リモート NDIS から USB へのマッピングは、Usb8023 ドライバーに実装されています。 Windows でのネットワークサポートの詳細については、「<a href="https://go.microsoft.com/fwlink/p/?linkid=8759">ネットワークとワイヤレステクノロジ</a>」 web サイトを参照してください。</td>
    </tr>
    <tr>
      <td>アプリケーション固有 (ファー)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb .sys)</a></td>
    </tr>
     <tr>
      <td>ベンダー固有 (FFh)</td>
      <td>-</td>
      <td>-</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb .sys)</a></td>
    </tr>
  </tbody>
</table>

## <a name="related-topics"></a>関連トピック

[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  

---
Description: このトピックでは、サポートされている USB デバイス クラス用の Microsoft 提供のドライバーをリストします。
title: Windows に含まれる USB デバイス クラス ドライバー
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: ce0646add1764f938ce2931262492afcb2fa03ca
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80998074"
---
# <a name="usb-device-class-drivers-included-in-windows"></a>Windows に含まれる USB デバイス クラス ドライバー

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 USB に関する問題が発生している場合は、「[一般的な USB の問題のトラブルシューティング](https://support.microsoft.com/help/17614/windows-10-troubleshoot-common-usb-problems)」を参照してください

このトピックでは、サポートされている USB デバイス クラス用の Microsoft 提供のドライバーをリストします。

- USB-IF 認定デバイス クラス用の Microsoft 提供のドライバー。
- 複合デバイスの場合は、[USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md) を使用します。これにより、各関数の物理デバイス オブジェクト (PDO) が作成されます。
- 非複合デバイス、または複合デバイスの関数の場合は、[WinUSB (Winusb.sys)](winusb.md) を使用します。

**USB ドライバーをインストールする場合:** USB デバイス クラス ドライバーをダウンロードする必要はありません。 これらは自動的にインストールされます。 これらのドライバーとそのインストール ファイルは、Windows に含まれています。 これらは、\\Windows\\System32\\DriverStore\\FileRepository フォルダーにあります。 ドライバーは Windows Update を通じて更新されます。

**カスタム ドライバーを作成する場合:** USB デバイス用のドライバーを作成する前に、Microsoft 提供のドライバーがデバイス要件を満たしているかどうかを確認します。 デバイスが属する USB デバイス クラスで Microsoft 提供のドライバーを使用できない場合は、汎用ドライバーである Winusb.sys または Usbccgp.sys を使用することを検討してください。 ドライバーは必要な場合にのみ作成してください。 「[USB クライアント ドライバー開発用のドライバー モデルの選択](winusb-considerations.md)」には、さらに多くのガイドラインが含まれています。

## <a name="usb-device-classes"></a>USB デバイス クラス

"*USB デバイス クラス*" は、類似した特性を持ち、共通の関数を実行するデバイスのカテゴリです。 これらのクラスとその仕様は、USB-IF によって定義されます。 各デバイス クラスは USB-IF 認定クラス、サブクラス、プロトコル コードによって識別されます。これらはすべて、ファームウェアのデバイス記述子で IHV によって提供されます。 Microsoft では、"*USB デバイス クラス ドライバー*" と呼ばれる、いくつかのデバイス クラス用のインボックス ドライバーを提供しています。 サポートされているデバイス クラスに属するデバイスがシステムに接続されている場合、Windows ではクラス ドライバーが自動的に読み込まれ、デバイスは追加のドライバーを必要とせずに機能します。

ハードウェア ベンダーが、サポートされているデバイス クラスのドライバーを作成することはできません。 Windows クラス ドライバーでは、クラスの仕様で説明されているすべての機能がサポートされていない場合があります。 デバイスの機能の一部がクラス ドライバーによって実装されていない場合、ベンダーは、デバイスによって提供される機能の範囲全体をサポートするために、クラス ドライバーと連携する補助ドライバーを提供する必要があります。

USB-IF 認定デバイス クラスに関する一般情報については、[ USB テクノロジ](https://www.usb.org/developers/defined_class/)に関する Web サイトを参照してください。

USB クラスの仕様とクラス コードの現在のリストについては、[USB DWG に関する Web サイト](https://www.usb.org/about/dwg_charter/)を参照してください。

## <a name="device-setup-classes"></a>デバイス セットアップ クラス

Windows では、デバイスの機能を示す、"*デバイス セットアップ クラス*" でデバイスを分類します。

Microsoft では、ほとんどのデバイスのセットアップ クラスを定義しています。 IHV と OEM で新しいデバイス セットアップ クラスを定義できますが、既存のクラスが適用されていない場合に限ります。 詳細については、「[システム定義のデバイス セットアップ クラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))」を参照してください。

USB デバイス用の 2 つの重要なデバイス セットアップ クラスは、次のとおりです。

- **USBDevice** {88BAE032-5A81-49f0-BC3D-A4FF138216D6}:IHV では、別のクラスに属していないカスタム デバイスに対して、このクラスを使用する必要があります。 このクラスは、USB ホスト コントローラーおよびハブでは使用されません。

- **USB** {36fc9e60-c465-11cf-8056-444553540000}:IHV では、カスタム デバイスに対して、このクラスを使用することはできません。 これは、USB ホスト コントローラーおよび USB ハブ用に予約されています。

デバイス セットアップ クラスは、前述の USB デバイス クラスとは異なります。 たとえば、オーディオ デバイスでは、その記述子に 01h という USB デバイス クラス コードがあります。 システムに接続されている場合、Windows では、Microsoft 提供のクラス ドライバーである、Usbaudio.sys が読み込まれます。 デバイス マネージャーでは、デバイスが **[サウンド、ビデオ、およびゲーム コントローラー]** に表示されます。これは、デバイス セットアップ クラスが Media であることを示します。

## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供の USB デバイス クラス ドライバー

<table>
  <thead>
    <tr>
      <th>USB-IF クラス コード</th>
      <th>デバイス セットアップ クラス</th>
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
      <td>Usbaudio.sys<p>Wdma\_usb.inf</p></td>
      <td>Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、Usbaudio.sys ドライバーを介して、USB オーディオ デバイス クラスのサポートを提供しています。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/audio/kernel-mode-wdm-audio-components">カーネル モード WDM オーディオ コンポーネント</a>」の USB オーディオ クラス システム ドライバーに関するセクションを参照してください。 Windows のオーディオ サポートの詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=8751">Windows 用のオーディオ デバイス テクノロジ</a>に関する Web サイトを参照してください。</td>
    </tr>
    <tr>
      <td rowspan="4">通信および CDC 制御 (02h)</td>
        <tr>
        <td><strong>Ports</strong></br>{4D36E978-E325-11CE-BFC1-08002BE10318}</td>
        <td>Usbser.sys</br>Usbser.inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</td>
        <td>Windows 10 では、Usbser.sys を関数ドライバーとして自動的に読み込む、新しい INF の Usbser.inf が追加されました。<p>詳細については、「<a href="usb-driver-installation-based-on-compatible-ids.md">USB シリアル ドライバー (Usbser.sys)</a>」を参照してください</p></td>
      </tr>
      <tr>
        <td><strong>Modem</strong></br>{4D36E96D-E325-11CE-BFC1-08002BE10318}<p>
        <strong>注</strong>   サブクラス 02h がサポートされます (ACM)</td>
        <td>Usbser.sys</br>mdmcpq.inf を参照するカスタム INF</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Windows 8.1 以前のバージョンでは、Usbser.sys が自動的には読み込まれません。 ドライバーを読み込むには、モデム INF (mdmcpq.inf) を参照し、\[Install\] および \[Needs\] セクションを含む INF を作成する必要があります。<p>Windows Vista 以降では、「<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md">ワイヤレス モバイル コミュニケーション デバイス クラスのサポート</a>」で説明されているように、レジストリ値を設定して、CDC およびワイヤレス モバイル CDC (WMCDC) のサポートを有効にすることができます。<p>CDC サポートが有効になっている場合、<a href="usb-common-class-generic-parent-driver.md">USB 共通クラスの汎用親ドライバー</a>で、CDC および WMCDC コントロール モデルに対応するインターフェイス コレクションが列挙され、物理デバイス オブジェクト (PDO) がこれらのコレクションに割り当てられます。</td>
      </tr>
      <tr>
        <td><strong>Net</strong></br>{4d36e972-e325-11ce-bfc1-08002be10318}</br><strong>注</strong>   サブクラス 0Eh がサポートされます (MBIM)</td>
        <td>wmbclass.sys</br>Netwmbclass.inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</td>
        <td>Windows 8 以降では、Microsoft で、モバイル ブロードバンド デバイス用の wmbclass.sys ドライバーが提供されています。 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/mb-interface-model">MB インターフェイス モデル</a>に関するページを参照してください。
</td>
      </tr>
      <tr>
        <td>HID (ヒューマン インターフェイス デバイス) (03h)</td>
        <td><strong>HIDClass</strong></br>{745a17a0-74d3-11d0-b6fe-00a0c90f57da}</td>
        <td>Hidclass.sys</br>Hidusb.sys</br>Input.inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Microsoft では、<a href="https://go.microsoft.com/fwlink/p/?LinkId=761243">USB HID 標準</a>に準拠しているデバイスを操作するための、HID クラス ドライバー (Hidclass.sys) とミニクラス ドライバー (Hidusb.sys) を提供しています。 詳細については、「<a href="https://docs.microsoft.com/previous-versions/jj126193(v=vs.85)">HID のアーキテクチャ</a>」と「<a href="https://docs.microsoft.com/windows-hardware/drivers/hid/minidriver-operations">ミニドライバーと HID クラス ドライバー</a>」を参照してください。 入力ハードウェアの Windows でのサポートの詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=8709">入力と HID - アーキテクチャとドライバーのサポート</a>に関する Web サイトを参照してください。</td>
      </tr>
      <tr>
        <td>物理 (05h)</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb.sys)</a>
</td>
      </tr>
    <tr>
      <td>イメージ (06h)</td>
      <td><strong>画像</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbscan.sys</br>Sti.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、Windows XP 以降のオペレーティング システム用の USB デジタル カメラとスキャナーを管理する、Usbscan.sys ドライバーを提供しています。 このドライバーでは、Windows Imaging Architecture (WIA) の USB コンポーネントを実装します。 WIA の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/image/windows-image-acquisition-drivers">Windows イメージ取得ドライバー</a>」および <a href="https://go.microsoft.com/fwlink/p/?linkid=8768">Windows Imaging Component</a> に関する Web サイトを参照してください。 WIA での Usbscan.sys の役割の説明については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/image/wia-core-components">WIA Core コンポーネント</a>」を参照してください。</td>
    </tr>
    <tr>
      <td>プリンター (07h)</td>
      <td><strong>USB</strong><p><strong>注</strong>   Usbprint.sys では、デバイス セットアップ クラスの下にプリンター デバイスを列挙します。<strong>Printer</strong><p> {4d36e979-e325-11ce-bfc1-08002be10318}。</td>
      <td>Usbprint.sys</br>Usbprint.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、USB プリンターを管理する Usbprint.sys クラス ドライバーを提供しています。 Windows でのプリンター クラスの実装については、<a href="https://go.microsoft.com/fwlink/p/?linkid=8764">「印刷」のアーキテクチャとドライバーのサポート</a>に関する Web サイトを参照してください。</td>
    </tr>
    <tr>
      <td rowspan="3">大容量記憶装置 (08h)</td>
        <tr>
          <td><strong>USB</strong></td>
          <td>Usbstor.sys</td>
          <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft では、Microsoft のネイティブ ストレージ クラス ドライバーを使用して USB 大容量記憶装置を管理するための、Usbstor.sys ポート ドライバーを提供しています。 このドライバーによって管理されるデバイス スタックの例については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device">USB 大容量記憶装置のデバイス オブジェクトの例</a>」を参照してください。 Windows 記憶域のサポートについては、<a href="https://go.microsoft.com/fwlink/p/?linkid=8766">記憶域テクノロジ</a>に関する Web サイトを参照してください。</td>
        </tr>
        <tr>
         <td><strong>SCSIAdapter</strong><p>{4d36e97b-e325-11ce-bfc1-08002be10318}</td>
         <td>サブクラス (06) とプロトコル (62)</br>Uaspstor.sys</br>Uaspstor.inf</td>
         <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</td>
         <td>Uaspstor.sys は、一括ストリーム エンドポイントをサポートする SuperSpeed USB デバイス用のクラス ドライバーです。 詳細については、次のトピックを参照してください。 <ul>
           <li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/design/dn642103(v=vs.85)">xHCI へのクラス ドライバーとしての UASP ストレージ ドライバーの読み込み</a></li><li><a href="https://docs.microsoft.com/previous-versions/windows/hardware/design/dn642113(v=vs.85)">Windows 8 用の USB 接続 SCSI (UAS) のベスト プラクティス</a></li></ul></td>
        </tr>
    </tr>
    <tr>
      <td rowspan="3">ハブ (09h)</td>
      <td rowspan="3"><strong>USB</strong><p>{36fc9e60-c465-11cf-8056-444553540000}</td>
      <tr>
      <td>Usbhub.sys</br>Usb.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、USB ハブを管理するための Usbhub.sys ドライバーを提供しています。 ハブ クラス ドライバーと USB スタックの関係の詳細については、「<a href="usb-3-0-driver-stack-architecture.md">Windows の USB ホスト側ドライバー</a>」を参照してください。
        </td>
      <tr>
      <td>Usbhub3.sys</br>Usbhub3.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</td>
      <td>Microsoft では、SuperSpeed (USB 3.0) USB ハブを管理するための Usbhub3.sys ドライバーを提供しています。<p>ドライバーは、SuperSpeed ハブが xHCI コントローラーに接続されているときに読み込まれます。 「<a href="usb-3-0-driver-stack-architecture.md">Windows の USB ホスト側ドライバー</a>」を参照してください。</td>
        </tr>
      </tr>
    </tr>
     <tr>
      <td>CDC データ (0Ah)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td rowspan="3">スマート カード (0Bh)</td>
      <td rowspan="3"><strong>SmartCardReader</strong><p>{50dd5230-ba8a-11d1-bf5d-0000f805f530}</td>
        <tr>
          <td>Usbccid.sys (現在不使用)</td>
          <td>Windows 10 デスクトップ エディション</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft では、USB スマート カード リーダーを管理するための Usbccid.sys のミニクラス ドライバーを提供しています。 Windows のスマート カード ドライバーの詳細については、<a href="https://docs.microsoft.com/windows-hardware/drivers/smartcard/index">スマート カード設計ガイド</a>に関するページを参照してください。
          <p>Windows Server 2003、Windows XP、Windows 2000 では、オペレーティング システムよりも後にリリースされている可能性があるため、このドライバーを読み込む場合は特別な指示が必要であることにご注意ください。<p>
          <strong>注</strong>   Usbccid.sys ドライバーは、UMDF ドライバーの WUDFUsbccidDriver.dll に置き換えられました。</td>
          </tr>
         <tr>
           <td>WUDFUsbccidDriver.dll</br>WUDFUsbccidDriver.inf</td>
           <td>Windows 8.1</br>Windows 8</td>
           <td>WUDFUsbccidDriver.dll は、USB CCID スマート カード リーダー デバイス用のユーザーモード ドライバーです。</td>
         </tr>
       </tr>
       <tr>
      <td>コンテンツ セキュリティ (0Dh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="usb-common-class-generic-parent-driver.md">USB 汎用親ドライバー (Usbccgp.sys)</a>。 一部のコンテンツ セキュリティ機能は、Usbccgp.sys に実装されています。 「<a href="content-security-features-in-the-composite-client-generic-parent-drive.md">Usbccgp.sys のコンテンツ セキュリティ機能</a>」を参照してください。</td>
        </tr>
    </tr>
     <tr>
      <td>ビデオ (0Eh)</td>
      <td><strong>画像</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbvideo.sys<p>
Usbvideo.inf</td>
      <td>Windows 10 デスクトップ エディション<p>Windows Vista</td>
      <td>Microsoft では、Usbvideo.sys ドライバーを介して USB ビデオ クラス サポートを提供しています。 詳細については、<a href="https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-minidrivers-design-guide">AVStream ミニドライバー</a>に関するページの「USB ビデオ クラス ドライバー」を参照してください。
      <p>Windows XP では、オペレーティング システムより後にリリースされている可能性があるため、このドライバーを読み込む場合は特別な指示が必要であることにご注意ください。</td>
    </tr>
     <tr>
      <td>個人の医療 (0Fh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
     </tr>
     <tr>
      <td>オーディオおよびビデオ デバイス (10h)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>     <tr>
      <td>診断デバイス (DCh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>     <tr>
      <td>ワイヤレス コントローラー (E0h) <p><strong>注</strong>   サブクラス 01h とプロトコル 01h がサポートされます</td>
      <td>Bluetooth<p>{e0cbf06c-cd8b-4647-bb8a-263b43f0f974}</td>
      <td>Bthusb.sys<p>Bth.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Microsoft では、USB Bluetooth ラジオを管理するための Bthusb.sys ミニポート ドライバーを提供しています。 詳細については、<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536596(v=vs.85)">Bluetooth 設計ガイド</a>に関するページを参照してください。</td>
    </tr>     <tr>
      <td>その他 (EFh)</td>
      <td><strong>Net</strong><p>
{4d36e972-e325-11ce-bfc1-08002be10318}<p><strong>注</strong>  サブクラス 04h とプロトコル 01h がサポートされます</td>
      <td>Rndismp.sys</br>Rndismp.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Windows Vista より前の場合、CDC のサポートは、ベンダー固有のプロトコル (<strong>bInterfaceProtocol</strong>) 値が 0xFF の抽象コントロール モデル (ACM) の RNDIS 固有の実装に限定されます。 RNDIS 施設では、単一のクラス ドライバー Rndismp.sys ですべての 802 スタイルのネットワーク カードが集中管理されます。 リモート NDIS の詳細については、<a href="https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-remote-ndis--rndis-">リモート NDIS の概要</a>に関するページを参照してください。 リモート NDIS から USB へのマッピングは、Usb8023.sys ドライバーに実装されています。 Windows でのネットワーク サポートの詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=8759">ネットワークとワイヤレス テクノロジ</a>に関する Web サイトを参照してください。</td>
    </tr>
    <tr>
      <td>アプリケーション固有 (FEh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td>ベンダー固有 (FFh)</td>
      <td>-</td>
      <td>-</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</td>
      <td>推奨されるドライバー:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
  </tbody>
</table>

## <a name="related-topics"></a>関連トピック

[Microsoft が提供する USB ドライバー](system-supplied-usb-drivers.md)  

---
Description: このトピックでは、サポートされている USB デバイス クラスの Microsoft が提供するドライバーを使用します。
title: Windows に含まれる USB デバイス クラス ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3de0b27f2483509c395b4e685bded1d91f11a936
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419594"
---
# <a name="usb-device-class-drivers-included-in-windows"></a>Windows に含まれる USB デバイス クラス ドライバー

このトピックでは、サポートされている USB デバイス クラスの Microsoft が提供するドライバーを使用します。

- Microsoft が提供する、usb ドライバーのデバイス クラスを承認された場合。
- 複合のデバイスを使用して[USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)関数ごとに物理デバイス オブジェクト (Pdo) を作成します。
- 非複合デバイス、または複合デバイスの関数を使用して[WinUSB (Winusb.sys)](winusb.md)します。

**USB ドライバーをインストールする: 場合**デバイスの USB クラス ドライバーをダウンロードする必要はありません。 自動的にインストールされます。 Windows では、これらのドライバーと、インストール ファイルが含まれます。 利用できる、 \\Windows\\System32\\DriverStore\\FileRepository フォルダー。 ドライバーは、Windows Update を通じて更新されます。

**カスタム ドライバーを作成する: 場合**USB デバイスのドライバーを記述する前に、Microsoft 提供のドライバーがデバイスの要件を満たしているかどうかを決定します。 Microsoft 提供のドライバーが、デバイスが所属する USB デバイス クラスを使用できない場合、Winusb.sys またはで、Usbccgp.sys の汎用のドライバーを使用し、検討してください。 必要な場合にのみ、ドライバーを記述します。 詳細なガイドラインが含まれている[USB クライアント ドライバーを開発するためのドライバー モデルを選択する](winusb-considerations.md)します。

## <a name="usb-device-classes"></a>USB デバイス クラス

*USB デバイス クラス*のような特性を持つデバイスのカテゴリは、一般的な機能を実行します。 これらのクラスとその仕様が、USB で定義されている-場合。 各デバイスのクラスが USB で識別される、ファームウェア内のデバイス記述子の IHV によって提供される、すべてのクラスやサブクラスでは、プロトコルのコードを承認された場合。 マイクロソフトでは、インボックス ドライバーを提供するという、それらのデバイス クラスのいくつか*デバイスの USB クラス ドライバー*します。 サポートされているデバイスのクラスに属しているデバイスがシステムに接続されている場合、Windows 自動的に読み込まれますクラス ドライバー、およびデバイスの機能に必要な追加ドライバはありません。

ハードウェア ベンダーは、サポート対象のデバイス クラスに対するドライバーを記述しないでください。 Windows クラス ドライバーが可能性がありますクラス仕様で説明されている機能のすべてをサポートしていません。 クラス ドライバーによって実装されていないデバイスの機能の一部である場合、ベンダーは、デバイスによって提供される機能の範囲全体をサポートするために、クラス ドライバーと連携して動作する補助ドライバーを提供する必要があります。

USB に関する一般的な情報の場合はデバイス クラスを承認するを参照してください、 [USB テクノロジ](http://www.usb.org/developers/defined_class/)web サイト。

現在の USB クラス仕様とクラス コードの一覧では、、 [USB DWG web サイト](http://www.usb.org/about/dwg_charter/)を参照してください。

## <a name="device-setup-classes"></a>デバイス セットアップ クラス

Windows でのデバイスを分類して*デバイス セットアップ クラス*デバイスの機能を示します。

Microsoft では、ほとんどのデバイス セットアップ クラスを定義します。 Ihv と Oem は、新しいデバイス セットアップ クラスを定義できますが、場合にのみ、既存のクラスが適用されます。 詳細については、[ベンダーのデバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff553419)を参照してください。

USB デバイスの 2 つの重要なデバイス セットアップ クラスは次のとおりです。

- **USBDevice** {88bae032-5a81-49f0-bc3d-a4ff138216d6}:Ihv は、別のクラスに属していないカスタムのデバイスをこのクラスを使用する必要があります。 このクラスは、USB ホスト コント ローラーとハブは使用されません。

- **USB** 36fc9e60-c465-11cf-8056-444553540000。Ihv は、カスタム デバイスのこのクラスを使用する必要があります。 これは、USB ホスト コント ローラーと USB ハブの予約されています。

デバイス セットアップ クラスは、前に説明した USB デバイス クラスと異なる。 たとえば、オーディオ デバイスでは、その記述子 01 h の USB デバイス クラス コードがあります。 システムに接続しているときに、Windows は、Microsoft 提供のクラス ドライバー、Usbaudio.sys を読み込みます。 デバイス マネージャーで、デバイスが示すようには **サウンド、ビデオ、およびゲーム コント ローラー**、デバイス セットアップ クラスがメディアを示します。

## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供の USB デバイス クラス ドライバー

<table>
  <thead>
    <tr>
      <th>USB の場合にクラス コード</th>
      <th>デバイス セットアップ クラス</th>
      <th>Microsoft 提供のドライバーと INF</th>
      <th>Windows のサポート</th>
     <th>説明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>オーディオ (01 h)</td>
      <td><strong>メディア</strong></br>
{4d36e96c-e325-11ce-bfc1-08002be10318}</td>
      <td>Usbaudio.sys<p>Wdma\_usb.inf</p></td>
      <td>Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、Usbaudio.sys ドライバーを使用して、USB オーディオ デバイス クラスのサポートを提供します。 詳細については、「USBAudio クラスのシステム ドライバー」を参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff537039">カーネル モード WDM オーディオ コンポーネント</a>します。 Windows オーディオ サポートの詳細については、次を参照してください。、<a href="https://go.microsoft.com/fwlink/p/?linkid=8751">オーディオ デバイス テクノロジの Windows</a> web サイト。</td>
    </tr>
    <tr>
      <td rowspan="4">通信および CDC 制御 (02 h)</td>
        <tr>
        <td><strong>ポート</strong></br>{4D36E978-E325-11CE-BFC1-08002BE10318}</td>
        <td>Usbser.sys</br>Usbser.inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</td>
        <td>Windows 10 で新しい INF、Usbser.inf が追加されました Usbser.sys 関数ドライバーとして自動的に読み込まれます。<p>詳細については、次を参照してください<a href="usb-driver-installation-based-on-compatible-ids.md">USB シリアル ドライバー (Usbser.sys)。</a></p></td>
      </tr>
      <tr>
        <td><strong>モデム</strong></br>{4D36E96D-E325-11CE-BFC1-08002BE10318}<p>
        <strong>注</strong>サブクラス 02 h (ACM) をサポートしています</td>
        <td>Usbser.sys</br>カスタム INF mdmcpq.inf を参照します。</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>Windows 8.1 以前のバージョンで Usbser.sys は自動的に読み込まれません。 ドライバーを読み込むには、モデムの INF (mdmcpq.inf) を参照しを含む、INF を記述する必要があります。\[インストール\]と\[必要がある\]セクション。<p>Windows Vista 以降を有効にする CDC とワイヤレス モバイル CDC (WMCDC) のサポート、レジストリ値を設定」の説明に従って<a href="support-for-the-wireless-mobile-communication-device-class--wmcdc-.md">ワイヤレス モバイル通信デバイス クラスに対するサポート</a>します。<p>CDC のサポートが有効にすると、<a href="usb-common-class-generic-parent-driver.md">共通クラス ジェネリック親ドライバーを USB</a> CDC と WMCDC コントロール モデルでは、対応するインターフェイスのコレクションを列挙し、これらのコレクションに物理デバイス オブジェクト (PDO) を割り当てます。</td>
      </tr>
      <tr>
        <td><strong>Net</strong></br>{4d36e972-e325-11ce-bfc1-08002be10318}</br><strong>注</strong>サブクラスが 0 の eh をサポートしています (MBIM)</td>
        <td>wmbclass.sys</br>Netwmbclass.inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</td>
        <td>Windows 8 以降、Microsoft は、モバイル ブロード バンド デバイスの場合、wmbclass.sys ドライバーを提供します。 参照してください、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn265427">MB インターフェイス モデル</a>します。
</td>
      </tr>
      <tr>
        <td>(ヒューマン インターフェイス デバイス) を非表示 (03 h)</td>
        <td><strong>HIDClass</strong></br>{745a17a0-74d3-11d0-b6fe-00a0c90f57da}</td>
        <td>hidclass.sys</br>Hidusb.sys</br>Input.inf</td>
        <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
        <td>マイクロソフトは、HID クラス ドライバー (Hidclass.sys) と miniclass ドライバー (Hidusb.sys) に準拠しているデバイスの操作を提供しています。、 <a href="https://go.microsoft.com/fwlink/p/?LinkId=761243">USB HID 標準</a>します。 詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/jj126193">HID アーキテクチャ</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/jj131708">ミニドライバーと HID クラス ドライバー</a>を参照してください。 入力のハードウェアの Windows のサポートの詳細については、次を参照してください。、<a href="https://go.microsoft.com/fwlink/p/?linkid=8709">入力と HID - アーキテクチャとドライバー サポート</a>web サイト。</td>
      </tr>
      <tr>
        <td>物理 (05 h)</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>推奨されるドライバーは:<a href="winusb.md">WinUSB (Winusb.sys)</a>
</td>
      </tr>
    <tr>
      <td>イメージ (06 h)</td>
      <td><strong>イメージ</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbscan.sys</br>Sti.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、Windows XP およびそれ以降のオペレーティング システムを usb 接続のデジタル カメラおよびスキャナーを管理する Usbscan.sys ドライバーを提供します。 このドライバーは、Windows Imaging アーキテクチャ (WIA) の USB コンポーネントを実装します。 WIA に関する詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff553346">Windows Image Acquisition ドライバー</a>と<a href="https://go.microsoft.com/fwlink/p/?linkid=8768">Windows Imaging Component</a> web サイト。 WIA Usbscan.sys が果たす役割については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff550215">WIA コア コンポーネント</a>を参照してください。</td>
    </tr>
    <tr>
      <td>プリンター (07 h)</td>
      <td><strong>USB</strong><p><strong>注</strong>   Usbprint.sys クラスを設定、デバイスの プリンター デバイスを列挙します。<strong>プリンター</strong><p> {4d36e979-e325-11ce-bfc1-08002be10318}。</td>
      <td>Usbprint.sys</br>Usbprint.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、USB プリンターを管理する Usbprint.sys クラス ドライバーを提供します。 Windows で、printer クラスの実装については、次を参照してください。、<a href="https://go.microsoft.com/fwlink/p/?linkid=8764">印刷のアーキテクチャとドライバー サポート</a>web サイト。</td>
    </tr>
    <tr>
      <td rowspan="3">大容量記憶装置 (08 h)</td>
        <tr>
          <td><strong>USB</strong></td>
          <td>Usbstor.sys</td>
          <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft では、Microsoft のネイティブ ストレージ クラス ドライバーで USB 大容量記憶装置デバイスを管理する Usbstor.sys ポート ドライバーを提供します。 このドライバーで管理されている例デバイス スタックを参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552547">USB 大容量記憶装置のデバイス オブジェクトの例</a>します。 Windows 記憶域のサポートについては、次を参照してください。、<a href="https://go.microsoft.com/fwlink/p/?linkid=8766">記憶域テクノロジ</a>web サイト。</td>
        </tr>
        <tr>
         <td><strong>SCSIAdapter</strong><p>{4d36e97b-e325-11ce-bfc1-08002be10318}</td>
         <td>サブクラス (06) とプロトコル (62)</br>Uaspstor.sys</br>Uaspstor.inf</td>
         <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</td>
         <td>一括ストリームのエンドポイントをサポートしている SuperSpeed USB デバイスのクラス ドライバー Uaspstor.sys です。 します。 詳しくは、次のトピックをご覧ください。 <ul>
           <li><a href="https://msdn.microsoft.com/library/windows/hardware/gg585600.aspx">XHCI のクラス ドライバーとして UASP 記憶装置のドライバーの読み込み</a></li><li><a href="https://msdn.microsoft.com/library/windows/hardware/jj248714.aspx">USB 接続 SCSI (UAS) のベスト プラクティスをされている for Windows 8</li></ul></td>
        </tr>
    </tr>
    <tr>
      <td rowspan="3">Hub (09h)</td>
      <td rowspan="3"><strong>USB</strong><p>36fc9e60-c465-11cf-8056-444553540000</td>
      <tr>
      <td>Usbhub.sys</br>Usb.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
      <td>Microsoft では、USB ハブを管理するため、Usbhub.sys ドライバーを提供します。 ハブ クラス ドライバーと USB スタック間のリレーションシップの詳細については、<a href="usb-3-0-driver-stack-architecture.md">Windows での USB ホスト側ドライバー</a>を参照してください。
        </td>
      <tr>
      <td>Usbhub3.sys</br>Usbhub3.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</td>
      <td>Microsoft SuperSpeed (USB 3.0) USB を管理するため、Usbhub3.sys ドライバーを提供するハブ。<p>SuperSpeed ハブは、xHCI コント ローラーに関連付けられている場合、ドライバーが読み込まれます。 参照してください<a href="usb-3-0-driver-stack-architecture.md">Windows での USB ホスト側ドライバー</a>します。</td>
        </tr>
      </tr>
    </tr>
     <tr>
      <td>CDC データ (0 ah)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバーは:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td rowspan="3">スマート カード (0Bh)</td>
      <td rowspan="3"><strong>SmartCardReader</strong><p>{50dd5230-ba8a-11d1-bf5d-0000f805f530}</td>
        <tr>
          <td>Usbccid.sys (廃止)</td>
          <td>Windows 10 デスクトップ エディション</br>Windows 7</br>Windows Server 2008</br>Windows Vista</td>
          <td>Microsoft では、USB スマート カード リーダーを管理する Usbccid.sys ミニ クラス ドライバーを提供します。 Windows でのスマート カードのドライバーの詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff549003">スマート カードのデザイン ガイド</a>を参照してください。
          <p>Windows Server 2003、Windows XP、および Windows 2000、特別な指示が必要であるため、その可能性がありますがリリースされたオペレーティング システムよりも後で、このドライバーを読み込むために注意してください。<p>
          <strong>注</strong>Usbccid.sys ドライバーは UMDF ドライバー、WUDFUsbccidDriver.dll によって置き換えられました。</td>
          </tr>
         <tr>
           <td>WUDFUsbccidDriver.dll</br>WUDFUsbccidDriver.inf</td>
           <td>Windows 8.1</br>Windows 8</td>
           <td>WUDFUsbccidDriver.dll は、USB CCID スマート カード リーダー デバイスのユーザー モード ドライバーです。</td>
         </tr>
       </tr>
       <tr>
      <td>コンテンツのセキュリティ (0Dh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバーは:<a href="usb-common-class-generic-parent-driver.md">一般的な親の USB ドライバー (Usbccgp.sys)</a>します。 Usbccgp.sys で一部のコンテンツのセキュリティ機能が実装されます。 参照してください<a href="content-security-features-in-the-composite-client-generic-parent-drive.md">コンテンツのセキュリティ機能で、Usbccgp.sys</a>します。</td>
        </tr>
    </tr>
     <tr>
      <td>ビデオ (が 0 eh)</td>
      <td><strong>イメージ</strong></br>{6bdd1fc6-810f-11d0-bec7-08002be2092f}</td>
      <td>Usbvideo.sys<p>
Usbvideo.inf</td>
      <td>Windows 10 デスクトップ エディション<p>Windows Vista</td>
      <td>Usbvideo.sys ドライバーを使用して USB ビデオ クラスのサポートを提供します。 詳細については、下で「USB ビデオ クラス ドライバー」を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554228">AVStream ミニドライバー</a>します。
      <p>Windows xp では、特別な指示が必要であるため、その可能性がありますがリリースされたオペレーティング システムよりも後で、このドライバーを読み込むために注意してください。</td>
    </tr>
     <tr>
      <td>個人の医療 (0 fh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバーは:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
     </tr>
     <tr>
      <td>オーディオ/ビデオ デバイス (10 h)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>     <tr>
      <td>診断のデバイス (DCh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバーは:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>     <tr>
      <td>ワイヤレス コント ローラー (E0h) <p><strong>注</strong>  サブクラス 01 h および 01 h のプロトコルをサポート</td>
      <td>Bluetooth<p>{e0cbf06c-cd8b-4647-bb8a-263b43f0f974}</td>
      <td>Bthusb.sys<p>Bth.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Microsoft では、USB Bluetooth 無線を管理する Bthusb.sys ミニポート ドライバーを提供します。 詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff536596">Bluetooth 設計ガイド</a>を参照してください。</td>
    </tr>     <tr>
      <td>その他 (EFh)</td>
      <td><strong>Net</strong><p>
{4d36e972-e325-11ce-bfc1-08002be10318}<p><strong>注</strong>  サブクラス 04 h および 01 h のプロトコルをサポート</td>
      <td>Rndismp.sys</br>Rndismp.inf</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 8.1</br>Windows 8</br>Windows 7</br>Windows Vista</td>
      <td>Windows Vista では、前にサポート CDC はベンダー固有のプロトコルで抽象コントロール モデル (ACM) の RNDIS 固有の実装に限定されています (<strong>bInterfaceProtocol</strong>) 0 xff までの値。 RNDIS 機能は、1 つのクラスのドライバー、Rndismp.sys 802 スタイルのネットワーク カードをすべての管理を中央揃えします。 リモートの NDIS の詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff569967">リモート NDIS 概要</a>を参照してください。 リモートの NDIS USB へのマッピングは、Usb8023.sys ドライバーに実装されます。 Windows でのネットワークのサポートについては、次を参照してください。、<a href="https://go.microsoft.com/fwlink/p/?linkid=8759">ネットワークおよびワイヤレス テクノロジ</a>web サイト。</td>
    </tr>
    <tr>
      <td>アプリケーション固有 (FEh)</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>推奨されるドライバーは:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
     <tr>
      <td>ベンダー固有 (FFh)</td>
      <td>-</td>
      <td>-</td>
      <td>Windows 10 デスクトップ エディション</br>Windows 10 Mobile</td>
      <td>推奨されるドライバーは:<a href="winusb.md">WinUSB (Winusb.sys)</a></td>
    </tr>
  </tbody>
</table>

## <a name="related-topics"></a>関連トピック

[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  

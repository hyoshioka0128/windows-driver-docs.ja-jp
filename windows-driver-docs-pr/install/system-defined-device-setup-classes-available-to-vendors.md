---
title: ベンダーが使用できるシステム定義のデバイス セットアップ クラス
description: ベンダーが使用できるシステム定義のデバイス セットアップ クラス
ms.assetid: d4b8a964-f843-4960-9077-46746af27a61
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b56335f3c2a136451a7fc698147ae148bfad704f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837359"
---
# <a name="system-defined-device-setup-classes-available-to-vendors"></a>ベンダーが使用できるシステム定義のデバイス セットアップ クラス  
  
  
次のクラスと Guid は、オペレーティングシステムによって定義されます。 特に明記されていない限り、これらのクラスと Guid を使用して、Windows 2000 以降のバージョンの Windows にデバイス (またはドライバー) をインストールすることができます。  
  
**バッテリデバイス**  
クラス = バッテリ  
ClassGuid = {72631e54-78a4-11d0-bcf7-00aa00b7b32a}  
このクラスには、バッテリデバイスと UPS デバイスが含まれます。  
  
**生体認証デバイス**  
クラス = 生体認証  
ClassGuid = {53D29EF7-377C-4D14-864B-EB3A85769359}  
(Windows Server 2003 以降のバージョンの Windows)このクラスには、生体認証ベースの個人識別デバイスがすべて含まれます。  
  
**Bluetooth デバイス**  
クラス = Bluetooth  
ClassGuid = {e0cbf06c-cd8b-4647-bb8a-263b43f0f974}  
(Windows XP SP1 以降のバージョンの Windows)このクラスには、すべての Bluetooth デバイスが含まれます。  
  
**カメラデバイス**  
クラス = カメラ  
ClassGuid = {ca3e7ab9-b4c3-4ae6-8251-579ef933890f}  
(Windows 10 バージョン1709以降のバージョンの Windows)このクラスには、ユニバーサルカメラドライバーが含まれています。  
  
**CD-ROM ドライブ**  
Class = CDROM  
ClassGuid = {4d36e965-e325-11ce-bfc1-08002be10318}  
このクラスには、SCSI CD-ROM ドライブを含む CD-ROM ドライブが含まれています。 既定では、システムによって提供される cd オーディオドライバーと CD-ROM チェンジャードライバーもプラグアンドプレイフィルターとしてインストールされます。  
  
<a href="" id="disk-drives-"></a>**ディスクドライブ**  
Class = DiskDrive  
ClassGuid = {4d36e967-e325-11ce-bfc1-08002be10318}  
このクラスには、ハードディスクドライブが含まれています。 「HDC クラスと SCSIAdapter クラス」も参照してください。  
  
**ディスプレイアダプター**  
Class = 表示  
ClassGuid = {4d36e968-e325-11ce-bfc1-08002be10318}  
このクラスには、ビデオアダプターが含まれています。 このクラスのドライバーには、ディスプレイドライバーとビデオミニポートドライバーが含まれます。  
  
**拡張機能の INF**  
Class = Extension  
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}  
(Windows 10 以降のバージョンの Windows)このクラスには、カスタマイズが必要なすべてのデバイスが含まれます。 詳細については、「[拡張機能の INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」を参照してください。  
  
<a href="" id="floppy-disk-controllers-"></a>**フロッピーディスクコントローラー**  
Class = FDC  
ClassGuid = {4d36e969-e325-11ce-bfc1-08002be10318}  
このクラスには、フロッピーディスクドライブコントローラーが含まれています。  
  
**フロッピーディスクドライブ**  
Class = FloppyDisk  
ClassGuid = {4d36e980-e325-11ce-bfc1-08002be10318}  
このクラスには、フロッピーディスクドライブが含まれています。  
  
<a href="" id="hard-disk-controllers-"></a>**ハードディスクコントローラー**  
Class = HDC  
ClassGuid = {4d36e96a-e325-11ce-bfc1-08002be10318}  
このクラスには、ATA/ATAPI コントローラーを含む、SCSI および RAID ディスクコントローラーではないハードディスクコントローラーが含まれます。  
  
**ヒューマンインターフェイスデバイス (HID)**  
Class = HIDClass  
ClassGuid = {745a17a0-74d3-11d0-b6fe-00a0c90f57da}  
このクラスには、システムによって提供される[HID クラスドライバー](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))によって動作する対話型の入力デバイスが含まれます。 これには、HID ミニドライバーを使用する[USB HID Standard](../hid/hid-over-usb.md)および非 usb デバイスに準拠している usb デバイスが含まれます。 詳細については、「 [HIDClass Device Setup Class](../hid/minidriver-operations.md)」を参照してください。 (この一覧の後半の「キーボードまたはマウスクラス」も参照してください)。  
  
**IEEE 1284.4 デバイス**  
クラス = Dot4  
ClassGuid = {48721b56-6795-11d2-b1a8-0080c72e74a2}  
このクラスには、多機能な IEEE 1284.4 周辺機器の動作を制御するデバイスが含まれます。  
  
**IEEE 1284.4 印刷関数**  
Class = Dot4Print  
ClassGuid = {49ce6ac8-6f86-11d2-b1e5-0080c72e74a2}  
このクラスには、Dot4 印刷関数が含まれています。 Dot4 print 関数は、Dot4 デバイス上の関数であり、プリンターデバイスセットアップクラスのメンバーである子デバイスを1つ持ちます。  
  
**61883プロトコルをサポートする IEEE 1394 デバイス**  
クラス = 61883  
ClassGuid = {7ebefbc0-3200-11d2-b4c2-00a0C9697d07}  
このクラスには、IEC-61883 プロトコルデバイスクラスをサポートする IEEE 1394 デバイスが含まれています。  
  
61883コンポーネントには、1394バス上でさまざまなオーディオおよびビデオデータストリームを送信する*61883*プロトコルドライバーが含まれています。 現時点では、standard/高/低品質の DV、MPEG2、DSS、オーディオが含まれています。 これらのデータストリームは、IEC-61883 仕様で定義されています。  
  
**AVC プロトコルをサポートする IEEE 1394 デバイス**  
Class = AVC  
ClassGuid = {c06ff265-ae09-48f0-812c-16753d7cba83}  
このクラスには、AVC プロトコルデバイスクラスをサポートする IEEE 1394 デバイスが含まれています。  
  
**SBP2 プロトコルをサポートする IEEE 1394 デバイス**  
Class = SBP2  
ClassGuid = {d48179be-ec20-11d1-b6b8-00c04fa372a7}  
このクラスには、SBP2 protocol device クラスをサポートする IEEE 1394 デバイスが含まれています。  
  
<a href="" id="ieee-1394-host-bus-controller-"></a>**IEEE 1394 ホストバスコントローラー**  
クラス = 1394  
ClassGuid = {6bdd1fc1-810f-11d0-bec7-08002be2092f}  
このクラスには、PCI バス上で接続されているが1394周辺機器ではない1394ホストコントローラーが含まれます。 このクラスのドライバーはシステムによって提供されます。  
  
<a href="" id="imaging-device-"></a>**イメージングデバイス**  
クラス = イメージ  
ClassGuid = {6bdd1fc6-810f-11d0-bec7-08002be2092f}  
このクラスには、静止イメージキャプチャデバイス、デジタルカメラ、スキャナーなどが含まれます。  
  
**IrDA デバイス**  
クラス = 赤外線  
ClassGuid = {6bdd1fc5-810f-11d0-bec7-08002be2092f}  
このクラスには、赤外線デバイスが含まれます。 このクラスのドライバーには、シリアル IR と高速 IR NDIS ミニポートが含まれますが、他の NDIS ネットワークアダプターミニポートのネットワークアダプタークラスも参照してください。  
  
**キーボード**  
クラス = キーボード  
ClassGuid = {4d36e96b-e325-11ce-bfc1-08002be10318}  
このクラスには、すべてのキーボードが含まれます。 つまり、列挙された子 HID キーボードデバイスの場合は、(セカンダリ) INF でも指定する必要があります。  
  
**メディアチェンジャー**  
Class = MediumChanger  
ClassGuid = {ce5939ae-ebde-11d0-b181-0000f8753ec4}  
このクラスには、SCSI メディアチェンジャーデバイスが含まれます。  
  
<a href="" id="memory-technology-driver-"></a>**メモリテクノロジドライバー**  
クラス = MTD  
ClassGuid = {4d36e970-e325-11ce-bfc1-08002be10318}  
このクラスには、フラッシュメモリカードなどのメモリデバイスが含まれています。  
  
<a href="" id="modem-"></a>**内蔵**  
クラス = モデム  
ClassGuid = {4d36e96d-e325-11ce-bfc1-08002be10318}  
このクラスには、モデムデバイスまたは*ソフトウェアモデム*が含まれます。 これらのデバイスは、モデムデバイスとデバイスドライバーの間で機能を分割します。 モデムの INF ファイルと Microsoft Windows Driver Model (WDM) モデムデバイスの詳細については、「[モデムの Inf ファイルの概要](https://docs.microsoft.com/previous-versions/windows/hardware/modem/ff542559(v=vs.85))」および「 [wdm モデムサポートの追加](https://docs.microsoft.com/previous-versions/windows/hardware/modem/ff541218(v=vs.85))」を参照してください。  
  
<a href="" id="monitor-"></a>**Monitor**  
クラス = モニター  
ClassGuid = {4d36e96e-e325-11ce-bfc1-08002be10318}  
このクラスには、ディスプレイモニターが含まれています。 このクラスのデバイスの INF はデバイスドライバーをインストールしませんが、代わりに、ビデオアダプターのドライバーで使用するために、特定のモニターの機能をレジストリに格納するように指定します。 (モニターは、ディスプレイアダプターの子デバイスとして列挙されます)。  
  
<a href="" id="mouse-"></a>**マウス**  
クラス = マウス  
ClassGuid = {4d36e96f-e325-11ce-bfc1-08002be10318}  
このクラスには、すべてのマウスデバイスとその他の種類のポインティングデバイス (trackballs など) が含まれています。 つまり、このクラスは、列挙された子 HID マウスデバイスの (セカンダリ) INF でも指定する必要があります。  
  
**多機能デバイス**  
クラス = 多機能  
ClassGuid = {4d36e971-e325-11ce-bfc1-08002be10318}  
このクラスには、PCMCIA モデムやネットカードアダプターなどのコンボカードが含まれています。 このようなプラグアンドプレイ多機能デバイスのドライバーは、このクラスの下にインストールされ、その子デバイスとして、モデムとネットカードを個別に列挙します。  
  
<a href="" id="multimedia-"></a>**マルチ**  
クラス = メディア  
ClassGuid = {4d36e96c-e325-11ce-bfc1-08002be10318}  
このクラスには、オーディオおよび DVD マルチメディアデバイス、ジョイスティックポート、およびフルモーションビデオキャプチャデバイスが含まれています。  
  
**マルチポートシリアルアダプター**  
クラス = MultiportSerial  
ClassGuid = {50906cb8-ba12-11d1-bf5d0000f805f530}  
このクラスにはインテリジェントマルチポートシリアルカードが含まれますが、ポートに接続する周辺機器は含まれません。 非インテリジェント (16550 型) のマルチポートシリアルコントローラーまたは単一ポートのシリアルコントローラー (Ports クラスを参照) は含まれません。  
  
<a href="" id="network-adapter-"></a>**ネットワークアダプター**  
クラス = Net  
ClassGuid = {4d36e972-e325-11ce-bfc1-08002be10318}  
このクラスは、ネットワークアダプタードライバーで構成されます。  これらのドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)または[**NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)を呼び出す必要があります。  NDIS または NetAdapter を使用しないドライバーでは、別のセットアップクラスを使用する必要があります。
  
<a href="" id="network-client-"></a>**ネットワーククライアント**  
クラス = NetClient  
ClassGuid = {4d36e973-e325-11ce-bfc1-08002be10318}  
このクラスには、ネットワークまたは印刷プロバイダーが含まれます。  
  
**注**  **netclient**コンポーネントは Windows 8.1、Windows Server 2012 R2 以降では非推奨とされます。  
  
   
  
**ネットワークサービス**  
クラス = NetService  
ClassGuid = {4d36e974-e325-11ce-bfc1-08002be10318}  
このクラスには、リダイレクターやサーバーなどのネットワークサービスが含まれています。  
  
<a href="" id="network-transport-"></a>**ネットワークトランスポート**  
Class = NetTrans  
ClassGuid = {4d36e975-e325-11ce-bfc1-08002be10318}  
このクラスには、トランスポートスタックの上位レベルのドライバーだけでなく、スタンドアロンの呼び出しマネージャーを含む NDIS プロトコルとクライアントが含まれています。  
  
**PCI SSL アクセラレータ**  
Class = SecurityAccelerator  
ClassGuid = {268c95a1-edfe-11d3-95c3-0010dc4050a5}  
このクラスには、secure sockets layer (SSL) 暗号化処理を高速化するデバイスが含まれます。  
  
<a href="" id="pcmcia-adapters-"></a>**PCMCIA アダプター**  
クラス = PCMCIA  
ClassGuid = {4d36e977-e325-11ce-bfc1-08002be10318}  
このクラスには、pcmcia および cardbus のホストコントローラーが含まれますが、PCMCIA や CardBus の周辺機器は含まれません。 このクラスのドライバーはシステムによって提供されます。  
  
<a href="" id="ports--com---lpt-ports--"></a>**ポート (COM & LPT ポート)**  
クラス = ポート  
ClassGuid = {4d36e978-e325-11ce-bfc1-08002be10318}  
このクラスには、シリアルおよびパラレルポートデバイスが含まれます。 「MultiportSerial クラス」も参照してください。  
  
<a href="" id="printers-"></a>**印刷**  
クラス = プリンター  
ClassGuid = {4d36e979-e325-11ce-bfc1-08002be10318}  
このクラスには、プリンターが含まれています。  
  
**プリンター、バス固有のクラスドライバー**  
Class = PNPPrinters  
ClassGuid = {4658ee7e-f050-11d1-b6bd-00c04fa372a7}  
このクラスには、SCSI/1394 で列挙されたプリンターが含まれます。 このクラスのドライバーは、特定のバスのプリンター通信を提供します。  
  
<a href="" id="processors-"></a>**状況**  
クラス = プロセッサ  
ClassGuid = {50127dc3-0f36-415e-a6cc-4cb3be910b65}  
このクラスには、プロセッサの種類が含まれています。  
  
<a href="" id="scsi-and-raid-controllers-"></a>**SCSI コントローラーと RAID コントローラー**  
Class = SCSIAdapter  
ClassGuid = {4d36e97b-e325-11ce-bfc1-08002be10318}  
このクラスには、SCSI Hba (ホストバスアダプター) とディスクアレイコントローラーが含まれます。  
  
**センサー**  
クラス = センサー  
ClassGuid = {5175d334-c371-4806-b3ba-71fd53c9258d}  
(Windows 7 以降のバージョンの Windows)このクラスには、GPS デバイスなどのセンサーと位置のデバイスが含まれます。  
  
**スマートカードリーダー**  
クラス = SmartCardReader  
ClassGuid = {50dd5230 kb ba8a-11d1-5f530 分 0000 00% 5  
このクラスには、スマートカードリーダーが含まれています。  
  
**ソフトウェアコンポーネント**  
Class = ソフトウェアコンポーネント  
ClassGuid = {5c4c3332-344d-483c-8739-259e934c9cc8}  
(Windows 10 バージョン1703以降のバージョンの Windows)このクラスには、ソフトウェアコンポーネントをカプセル化するための仮想子デバイスが含まれています。 詳細については、「[ソフトウェアコンポーネントを INF ファイルに追加する](https://docs.microsoft.com/windows-hardware/drivers/install/adding-software-components-with-an-inf-file)」を参照してください。  
  
<a href="" id="storage-volumes-"></a>**記憶域ボリューム**  
クラス = ボリューム  
ClassGuid = {71a27cdd30 12a-11d0-o 7-08002be2092f}  
このクラスには、システムによって提供される論理ボリュームマネージャーおよびクラスドライバーによって定義される記憶域ボリュームが含まれます。このクラスは、システムディスククラスドライバーなどの記憶域ボリュームを表すデバイスオブジェクトを作成します。  
  
<a href="" id="system-devices-"></a>**システムデバイス**  
クラス = システム  
ClassGuid = {4d36e97d-e325-11ce-bfc1-08002be10318}  
このクラスには、Hal、システムバス、システムブリッジ、システム ACPI ドライバー、およびシステムボリュームマネージャードライバーが含まれています。  
  
<a href="" id="tape-drives-"></a>**テープドライブ**  
クラス = テープドライブ  
ClassGuid = {6d80788 4-7d21-11cf801c08002be10318}  
このクラスには、すべての tape miniclass ドライバーを含むテープドライブが含まれています。  
  
**USB デバイス**  
クラス = USBDevice  
ClassGuid = {88 Bae032-5a81-49F0-bc3da4ff138216d6}  
USBDevice には、別のクラスに属していないすべての USB デバイスが含まれます。 このクラスは、USB ホストコントローラーおよびハブでは使用されません。  
  
**USB ActiveSync デバイスの Windows CE**  
Class = WCEUSBS  
ClassGuid = {25dbce51-6c8f47 a72-8a6dg-4fc835}  
このクラスには Windows CE ActiveSync デバイスが含まれています。  
  
WCEUSBS セットアップクラスは、パーソナルコンピューターと、USB 経由の Windows CE ActiveSync ドライバー (通常は PocketPC デバイス) と互換性のあるデバイスとの間の通信をサポートしています。  
  
**Windows ポータブルデバイス (WPD)**  
クラス = WPD  
ClassGuid = {eec5ad98-8080-425f-922a-dabf3de3f69a}  
(Windows Vista 以降のバージョンの Windows)このクラスには、WPD デバイスが含まれています。  
  
**Windows SideShow**  
クラス = SideShow  
ClassGuid = {997b5d8d-c442-4f2e-baf3-9c8e671e9e21}  
(Windows Vista 以降のバージョンの Windows)このクラスには、Windows SideShow と互換性のあるすべてのデバイスが含まれます。  
  
   
  
   
  

  
  
  
  

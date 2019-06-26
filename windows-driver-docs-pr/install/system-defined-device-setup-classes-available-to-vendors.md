---
title: ベンダーが使用できるシステム定義のデバイス セットアップ クラス
description: ベンダーが使用できるシステム定義のデバイス セットアップ クラス
ms.assetid: d4b8a964-f843-4960-9077-46746af27a61
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: b1cb2d9ede7ab41b0b01175a68600ef9c4915574
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385861"
---
# <a name="system-defined-device-setup-classes-available-to-vendors"></a>ベンダーが使用できるシステム定義のデバイス セットアップ クラス  
  
  
次のクラスと Guid は、オペレーティング システムによって定義されます。 明記されない限り、これらのクラスと Guid をデバイス (またはドライバー) のインストールを使用して Windows 2000 以降のバージョンの Windows で。  
  
**デバイスのバッテリ**  
クラス バッテリを =  
ClassGuid = {72631e54-78a4-11d0-bcf7-00aa00b7b32a}  
このクラスでは、デバイスのバッテリと UPS デバイスを含みます。  
  
**生体認証デバイス**  
クラス = 生体認証  
ClassGuid = {53D29EF7-377C-4D14-864B-EB3A85769359}  
(Windows Server 2003 および Windows の以降のバージョン)このクラスには、個人識別の生体認証ベースのすべてのデバイスが含まれています。  
  
**Bluetooth デバイス**  
クラス Bluetooth を =  
ClassGuid = {e0cbf06c-cd8b-4647-bb8a-263b43f0f974}  
(Windows XP SP1 と以降のバージョンの Windows)このクラスには、すべての Bluetooth デバイスが含まれています。  
  
**デバイスのカメラ**  
クラスのカメラを =  
ClassGuid = {ca3e7ab9-b4c3-4ae6-8251-579ef933890f}  
(Windows 10 バージョン 1709 および以降のバージョンの Windows)このクラスには、ユニバーサル カメラのドライバーが含まれています。  
  
**CD-ROM ドライブ**  
クラス CDROM を =  
ClassGuid = {4d36e965-e325-11ce-bfc1-08002be10318}  
このクラスには、SCSI CD-ROM ドライブなどの CD-ROM ドライブが含まれています。 既定では、システムの CD-ROM クラスのインストーラーもインストールされますシステム提供の CD オーディオ ドライバーと CD-ROM チェンジャー ドライバー プラグ アンド プレイのフィルターとして。  
  
<a href="" id="disk-drives-"></a>**ディスク ドライブ**  
クラス ディスク ドライブを =  
ClassGuid = {4d36e967-e325-11ce-bfc1-08002be10318}  
このクラスには、ハード ディスク ドライブが含まれています。 HDC と SCSIAdapter クラスを参照してください。  
  
**ディスプレイ アダプター**  
クラスの表示を =  
ClassGuid = {4d36e968-e325-11ce-bfc1-08002be10318}  
このクラスには、ビデオ アダプターが含まれています。 このクラスのドライバーには、ディスプレイ ドライバーやビデオのミニポート ドライバーが含まれます。  
  
**拡張子 INF**  
クラスの拡張機能を =  
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}  
(Windows 10 および Windows の以降のバージョン)このクラスには、カスタマイズを必要とするすべてのデバイスが含まれています。 詳細については、次を参照してください。[拡張子 INF ファイルを使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)します。  
  
<a href="" id="floppy-disk-controllers-"></a>**フロッピー ディスク コント ローラー**  
クラス FDC を =  
ClassGuid = {4d36e969-e325-11ce-bfc1-08002be10318}  
このクラスには、フロッピー ディスク ドライブ コント ローラーが含まれています。  
  
**フロッピー ディスク ドライブ**  
クラス = フロッピー ディスク  
ClassGuid = {4d36e980-e325-11ce-bfc1-08002be10318}  
このクラスには、フロッピー ディスク ドライブが含まれています。  
  
<a href="" id="hard-disk-controllers-"></a>**ハード ディスク コント ローラー**  
クラス HDC を =  
ClassGuid = {4d36e96a-e325-11ce-bfc1-08002be10318}  
このクラスには、ハード ディスク コント ローラー含む ATA/ATAPI コント ローラーがない SCSI と RAID ディスク コント ローラーにはが含まれています。  
  
**ヒューマン インターフェイス デバイス (HID)**  
クラス HIDClass を =  
ClassGuid = {745a17a0-74d3-11d0-b6fe-00a0c90f57da}  
このクラスには、システムが提供することによって運用される対話型の入力デバイスが含まれています。 [HID クラス ドライバー](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))します。 これは、に準拠している USB デバイスが含まれています、 [USB HID 標準](../hid/hid-over-usb.md)と HID ミニドライバーを使用するデバイスを USB 以外。 詳細については、次を参照してください。 [HIDClass デバイス セットアップ クラス](../hid/minidriver-operations.md)します。 (この一覧の後半で、キーボードまたはマウス クラスも参照)。  
  
**IEEE 1284.4 デバイス**  
クラス Dot4 を =  
ClassGuid = {48721b56-6795-11d2-b1a8-0080c72e74a2}  
このクラスには、多機能の IEEE 1284.4 周辺機器の操作を制御するデバイスが含まれています。  
  
**IEEE 1284.4 印刷機能**  
クラス Dot4Print を =  
ClassGuid = {49ce6ac8-6f86-11d2-b1e5-0080c72e74a2}  
このクラスには、Dot4 印刷機能が含まれています。 Dot4 の印刷機能は Dot4 デバイス上の関数であり、プリンター デバイス セットアップ クラスのメンバーである 1 つの子デバイスです。  
  
**61883 プロトコルをサポートする IEEE 1394 デバイス**  
クラス 61883 を =  
ClassGuid = {7ebefbc0-3200-11d2-b4c2-00a0C9697d07}  
このクラスには、IEC 61883 プロトコルのデバイス クラスをサポートする IEEE 1394 デバイスが含まれています。  
  
61883 コンポーネントが含まれています、 *61883.sys* 1394 バス経由でのさまざまなオーディオおよびビデオのデータ ストリームの転送プロトコル ドライバー。 これらは現在、標準/高/低品質 DV、MPEG2、DSS、およびオーディオが含まれます。 これらのデータ ストリームは、IEC 61883 仕様によって定義されます。  
  
**AVC プロトコルをサポートする IEEE 1394 デバイス**  
クラス AVC を =  
ClassGuid = {c06ff265-ae09-48f0-812c-16753d7cba83}  
このクラスには、AVC プロトコルのデバイス クラスをサポートする IEEE 1394 デバイスが含まれています。  
  
**SBP2 プロトコルをサポートする IEEE 1394 デバイス**  
クラス SBP2 を =  
ClassGuid = {d48179be-ec20-11d1-b6b8-00c04fa372a7}  
このクラスには、SBP2 プロトコルのデバイス クラスをサポートする IEEE 1394 デバイスが含まれています。  
  
<a href="" id="ieee-1394-host-bus-controller-"></a>**IEEE 1394 ホスト バス コント ローラー**  
クラス 1394 を =  
ClassGuid = {6bdd1fc1-810f-11d0-bec7-08002be2092f}  
このクラスには、PCI バスがない 1394 周辺機器に接続している 1394 のホスト コント ローラーが含まれています。 このクラスのドライバーは、システムが提供します。  
  
<a href="" id="imaging-device-"></a>**イメージング デバイス**  
クラスのイメージを =  
ClassGuid = {6bdd1fc6-810f-11d0-bec7-08002be2092f}  
このクラスには、まだイメージのキャプチャ デバイスやデジタル カメラ、スキャナーが含まれています。  
  
**デバイスの IrDA**  
クラス赤外線を =  
ClassGuid = {6bdd1fc5-810f-11d0-bec7-08002be2092f}  
このクラスには、赤外線デバイスが含まれています。 このクラスのドライバーでは、シリアル IR と高速 IR NDIS ミニポートが含まれますも他の NDIS ネットワーク アダプターのミニポートのネットワーク アダプター クラスを参照してください。  
  
**[キーボード]**  
クラス キーボードを =  
ClassGuid = {4d36e96b-e325-11ce-bfc1-08002be10318}  
このクラスには、すべてのキーボードが含まれています。 つまり、する必要がありますも指定する必要が列挙子 HID キーボード デバイスの (セカンダリ) の INF にします。  
  
**メディア チェンジャー**  
クラス MediumChanger を =  
ClassGuid = {ce5939ae-ebde-11d0-b181-0000f8753ec4}  
このクラスには、メディア チェンジャーの SCSI デバイスが含まれています。  
  
<a href="" id="memory-technology-driver-"></a>**メモリのテクノロジのドライバー**  
クラス MTD を =  
ClassGuid = {4d36e970-e325-11ce-bfc1-08002be10318}  
このクラスには、フラッシュ メモリ カードなどのメモリ デバイスが含まれています。  
  
<a href="" id="modem-"></a>**モデム**  
クラス モデムを =  
ClassGuid = {4d36e96d-e325-11ce-bfc1-08002be10318}  
このクラスには、モデム デバイスが含まれています。 または、*ソフトウェア モデム*します。 これらのデバイスでは、モデム デバイスとデバイス ドライバーの機能を分割します。 モデムの INF ファイル、および Microsoft Windows Driver Model (WDM) モデム デバイスの詳細については、次を参照してください。[モデム INF ファイルの概要](https://docs.microsoft.com/previous-versions/windows/hardware/modem/ff542559(v=vs.85))と[WDM モデム サポートの追加](https://docs.microsoft.com/previous-versions/windows/hardware/modem/ff541218(v=vs.85))します。  
  
<a href="" id="monitor-"></a>**モニター**  
クラス モニターを =  
ClassGuid = {4d36e96e-e325-11ce-bfc1-08002be10318}  
このクラスには、ディスプレイ モニターが含まれています。 このクラスのデバイスに対して、INF では、デバイスのドライバーをインストールしないが、代わりに、ビデオ アダプターのドライバーで使用するためのレジストリに格納される特定のモニタの機能を指定します。 (モニターは、ディスプレイ アダプターの子デバイスとして列挙されます)。  
  
<a href="" id="mouse-"></a>**マウス**  
クラス マウスを =  
ClassGuid = {4d36e96f-e325-11ce-bfc1-08002be10318}  
このクラスには、すべてのマウス デバイスとその他のトラック ボールなどのポインティング デバイスが含まれています。 つまり、このクラスは、HID マウス デバイスの列挙子 (セカンダリ) の INF にも指定する必要があります。  
  
**多機能デバイス**  
クラス多機能を =  
ClassGuid = {4d36e971-e325-11ce-bfc1-08002be10318}  
このクラスには、コンボ カード PCMCIA のモデムとネットワーク カードのアダプターなどが含まれています。 このようなプラグ アンド プレイ多機能デバイスのドライバーでは、このクラスがインストールされているし、その子デバイスとして、モデムとネットワーク カードを個別に列挙します。  
  
<a href="" id="multimedia-"></a>**マルチ メディア**  
クラス メディアを =  
ClassGuid = {4d36e96c-e325-11ce-bfc1-08002be10318}  
このクラスには、オーディオおよび DVD のマルチ メディア デバイス、ジョイスティックのポート、およびフルモーション ビデオ キャプチャ デバイスが含まれています。  
  
**マルチポート シリアル アダプター**  
クラス MultiportSerial を =  
ClassGuid = {50906cb8-ba12-11d1-bf5d-0000f805f530}  
このクラスには、インテリジェントのマルチポート シリアル カードですがそのポートに接続しない周辺機器のデバイスが含まれています。 これは、高性能でない (16550 型) マルチポート シリアル コント ローラーまたは単一ポート (ポートのクラスを参照してください) シリアル コント ローラーには含まれません。  
  
<a href="" id="network-adapter-"></a>**ネットワーク アダプター**  
クラス = Net  
ClassGuid = {4d36e972-e325-11ce-bfc1-08002be10318}  
このクラスは、ネットワーク アダプターのドライバーで構成されます。  これらのドライバーには、いずれかの呼び出しが必要があります[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)または[ **NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)します。  NDIS または NetAdapter を使用しないドライバーには、別のセットアップ クラスを使用する必要があります。
  
<a href="" id="network-client-"></a>**ネットワーク クライアント**  
クラス NetClient を =  
ClassGuid = {4d36e973-e325-11ce-bfc1-08002be10318}  
このクラスには、ネットワークや印刷プロバイダーが含まれています。  
  
**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。  
  
   
  
**Network Service**  
クラス NetService を =  
ClassGuid = {4d36e974-e325-11ce-bfc1-08002be10318}  
このクラスには、リダイレクターやサーバーなどのネットワーク サービスが含まれています。  
  
<a href="" id="network-transport-"></a>**ネットワーク トランスポート**  
クラス NetTrans を =  
ClassGuid = {4d36e975-e325-11ce-bfc1-08002be10318}  
このクラスには、NDIS プロトコルいる CoNDIS スタンドアロン コール マネージャー、およびトランスポート スタックでより高いレベルのドライバーだけでなく、いる CoNDIS クライアントが含まれます。  
  
**PCI SSL アクセラレータ**  
クラス SecurityAccelerator を =  
ClassGuid = {268c95a1-edfe-11d3-95c3-0010dc4050a5}  
このクラスには、セキュア ソケット レイヤー (SSL) 暗号化処理を高速化するデバイスが含まれています。  
  
<a href="" id="pcmcia-adapters-"></a>**PCMCIA アダプター**  
クラス PCMCIA を =  
ClassGuid = {4d36e977-e325-11ce-bfc1-08002be10318}  
このクラスには、PCMCIA および CardBus のホスト コント ローラーはいないの PCMCIA または CardBus 周辺機器が含まれます。 このクラスのドライバーは、システムが提供します。  
  
<a href="" id="ports--com---lpt-ports--"></a>**ポート (COM と LPT ポート)**  
クラスのポートを =  
ClassGuid = {4d36e978-e325-11ce-bfc1-08002be10318}  
このクラスには、デバイス シリアルおよびパラレル ポートにはが含まれています。 MultiportSerial クラスを参照してください。  
  
<a href="" id="printers-"></a>**プリンター**  
クラス プリンターを =  
ClassGuid = {4d36e979-e325-11ce-bfc1-08002be10318}  
このクラスには、プリンターが含まれています。  
  
**プリンター、Bus 固有のクラス ドライバー**  
クラス PNPPrinters を =  
ClassGuid = {4658ee7e-f050-11d1-b6bd-00c04fa372a7}  
このクラスには、プリンター SCSI/1394 列挙にはが含まれています。 このクラスのドライバーでは、特定のバスのプリンターとの通信を提供します。  
  
<a href="" id="processors-"></a>**プロセッサ**  
クラスのプロセッサを =  
ClassGuid = {50127dc3-0f36-415e-a6cc-4cb3be910b65}  
このクラスには、プロセッサの種類が含まれています。  
  
<a href="" id="scsi-and-raid-controllers-"></a>**SCSI と RAID コント ローラー**  
クラス SCSIAdapter を =  
ClassGuid = {4d36e97b-e325-11ce-bfc1-08002be10318}  
このクラスには、SCSI Hba (ホスト バス アダプター)、ディスク アレイ コント ローラーが含まれています。  
  
**センサー**  
クラス センサーを =  
ClassGuid = {5175d334-c371-4806-b3ba-71fd53c9258d}  
(Windows 7 および Windows の以降のバージョン)このクラスには、GPS デバイスなどのセンサーと場所のデバイスが含まれています。  
  
**スマート カード リーダー**  
クラス SmartCardReader を =  
ClassGuid = {50dd5230-ba8a-11d1-bf5d-0000f805f530}  
このクラスには、スマート カード リーダーが含まれています。  
  
**ソフトウェアのコンポーネント**  
クラス SoftwareComponent を =  
ClassGuid = {5c4c3332-344d-483c-8739-259e934c9cc8}  
(Windows 10 バージョン 1703 および以降のバージョンの Windows)このクラスには、ソフトウェア コンポーネントをカプセル化するデバイス仮想の子にはが含まれています。 詳細については、次を参照してください。 [INF ファイルを使用したソフトウェア コンポーネントを追加する](https://docs.microsoft.com/windows-hardware/drivers/install/adding-software-components-with-an-inf-file)します。  
  
<a href="" id="storage-volumes-"></a>**記憶域ボリューム**  
クラスのボリュームを =  
ClassGuid = {71a27cdd-812a-11d0-bec7-08002be2092f}  
このクラスには、システム提供の論理ボリューム マネージャーとシステムのディスクのクラス ドライバーなどの記憶域ボリュームを表すデバイス オブジェクトを作成するクラス ドライバーで定義されている記憶域ボリュームが含まれています。  
  
<a href="" id="system-devices-"></a>**システム デバイス**  
クラス システムを =  
ClassGuid = {4d36e97d-e325-11ce-bfc1-08002be10318}  
このクラスには、Hal、システム バス、ブリッジのシステム、システム ACPI ドライバー、およびシステム ボリューム マネージャー ドライバーが含まれています。  
  
<a href="" id="tape-drives-"></a>**テープ ドライブ**  
クラス = テープ  
ClassGuid = {6d807884-7d21-11cf-801c-08002be10318}  
このクラスには、すべてのテープ miniclass ドライバーなどのテープ ドライブが含まれています。  
  
**USB デバイス**  
クラス USBDevice を =  
ClassGuid = {88bae032-5a81-49f0-bc3d-a4ff138216d6}  
USBDevice には、別のクラスに属していないすべての USB デバイスが含まれています。 このクラスは、USB ホスト コント ローラーとハブは使用されません。  
  
**Windows CE USB ActiveSync デバイス**  
クラス WCEUSBS を =  
ClassGuid = {25dbce51-6c8f-4a72-8a6d-b54c2b4fc835}  
このクラスには、Windows CE ActiveSync デバイスが含まれています。  
  
WCEUSBS セットアップ クラスは、パーソナル コンピューターと USB 経由で Windows CE ActiveSync ドライバー (一般的には、PocketPC デバイス) を使用した互換性のあるデバイス間の通信をサポートします。  
  
**Windows ポータブル デバイス (WPD)**  
クラス WPD を =  
ClassGuid = {eec5ad98-8080-425f-922a-dabf3de3f69a}  
(Windows Vista および Windows の以降のバージョン)このクラスには、WPD デバイスが含まれています。  
  
**Windows SideShow**  
クラス SideShow を =  
ClassGuid = {997b5d8d-c442-4f2e-baf3-9c8e671e9e21}  
(Windows Vista および Windows の以降のバージョン)このクラスには、Windows SideShow と互換性があるすべてのデバイスが含まれています。  
  
   
  
   
  

  
  
  
  

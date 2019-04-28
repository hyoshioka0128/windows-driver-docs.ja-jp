---
Description: ワイヤレス モバイル コミュニケーション デバイス クラスのサポート
title: ワイヤレス モバイル コミュニケーション デバイス クラスのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1402c9bbfafbba24753cf76539ee406b1c00bfb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379927"
---
# <a name="support-for-the-wireless-mobile-communication-device-class"></a>ワイヤレス モバイル コミュニケーション デバイス クラスのサポート


Windows Vista では、 [USB 汎用親ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)ユニバーサル シリアル バス (USB) 通信デバイス クラス (CDC) USB ワイヤレス モバイル通信デバイス クラス (に含まれているデバイスのサポートを提供します。WMCDC)。

USB ワイヤレス モバイル通信デバイス クラス (WMCDC) 仕様の接続、制御、およびホストとワイヤレス モバイル デバイス (携帯電話など) の間のコンテンツの交換のための標準の確立、デバイスが USB ポートに接続されています。 WMCDC は、さまざまな通信とネットワーク デバイスが含まれています、通信デバイス クラス (CDC) の拡張です。 このセクションでは、Windows オペレーティング システムで CDC と WMCDC のデバイスをサポートするアーキテクチャについて説明します。

WMCDC デバイスに分類される複数の関数から成る*論理ハンドセット*します。 ほとんどの WMCDC デバイスは 1 つの論理ハンドセットが、デバイスは、複数の論理電話機を必要があります。 通常、論理電話機には、データ、fax モデムやオブジェクト ストアでは、呼び出しの制御機能などの関数が含まれます。 論理ハンドセットは、USB オーディオ クラス仕様、USB ヒューマン入力デバイス (HID) クラスの指定、および USB ビデオ クラス仕様などの他の USB 仕様で定義されている関数をサポートしているにもあります。

Windows WMCDC アーキテクチャでは、ネイティブの Windows ドライバーを使用して、WMCDC デバイスの機能を管理します。 たとえば、Windows テレフォニー アプリケーション プログラム インターフェイス (TAPI) サブシステムを使用して、デバイスとデバイスのイーサネットを管理する Windows ネットワーク ドライバー インターフェイス specification (NDIS) サブシステムの音声およびデータ、fax モデムの機能を管理することができます。LAN 関数。 さらに、オブジェクト交換プロトコル (OBEX) 関数、ユーザー モードのソフトウェアの支援など、一部の関数を管理できる、 [WinUSB](winusb.md) (Winusb.sys)。

次の図は、WMCDC デバイスのドライバー スタックの例を示します。

![デバイスの構成とドライバー スタックのサンプル](images/wmcdc-architecture.png)

WMCDC デバイスには上の図には 1 つの論理ハンドセットが含まれています。 OBEX 関数およびモデム関数。 ベンダーから提供された INF ファイルでは、モデムを管理するネイティブの Windows ドライバーを読み込みます。 OBEX 関数がマネージ関数で実行されているベンダーから提供されたユーザー モード ドライバーによって、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff561365)(UMDF)。 ユーザー モード ドライバーでは、Windows ポータブル デバイス (WPD) プロトコルを使用してユーザーのアプリケーションとのインターフェイスと通信する、 [WinUSB](winusb.md) USB スタックとの通信にエクスポートします。 一般に、ベンダーから提供された INF ファイル Winusb.sys の Winusb.sys を使用するインターフェイスのコレクションごとに個別のインスタンスが読み込まれます。

### <a name="registry-settings"></a>レジストリの設定

USB スタックは、WMCDC を自動的にサポートしていません。 Usbccgp.sys のインスタンスをロードする INF ファイルを提供する必要があります。 INF ファイルを含める必要があります、 **AddReg**設定セクション、 **EnumeratorClass**に 21 で、Usbccgp.sys に関連付けられているソフトウェア キーのレジストリ値\_はバイナリ値3 つの数値から構築します。0x02, 0x00, 0x00 とします。 サンプル INF ファイルから次のコード例は、設定する方法を示しています。 **EnumeratorClass**適切な値。

```cpp
[CCGPDriverInstall.NT]
Include=usb.inf
Needs=Composite.Dev.NT
AddReg=CCGPDriverInstall.AddReg

[CCGPDriverInstall.NT.Services]
Include=usb.inf
Needs=Composite.Dev.NT.Services

[CCGPDriverInstall.AddReg]
HKR,,EnumeratorClass, 0x00000001,02,00,00
```

値を割り当てる必要がある**EnumeratorClass** INF ファイルで 16 進数の組によって表される 3 つの 1 バイトのバイナリ値から構成されます。02、00 および 00 です。 これら 3 つの数値は、USB Implementers Forum がそれぞれの CDC デバイス クラス、CDC デバイス サブクラスおよび CDC デバイス プロトコルに割り当てられている値に対応します。

正しく WMCDC デバイスを列挙するためにレジストリを構成する方法の詳細については、次を参照してください。[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)します。

さらに、次のトピックには、WMCDC について説明します。


## <a name="related-topics"></a>関連トピック
[一般的な親の USB ドライバー (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  




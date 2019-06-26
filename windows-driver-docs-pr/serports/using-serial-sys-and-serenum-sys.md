---
title: Serial.sys および Serenum.sys の使用
description: Serial.sys および Serenum.sys の使用
ms.assetid: 2dcf22c8-0666-4b58-8fd3-97a4d17eaa2a
keywords:
- WDK のシリアル ポート
- WDK のシリアル デバイス
- WDK のシリアル ポート
- ユニバーサル非同期の受信側の送信機 WDK シリアル デバイス
- UART WDK シリアル デバイス
- 機能ドライバー WDK シリアル ポート
- シリアル ドライバー WDK
- 16550 UART と互換性のあるインターフェイス WDK シリアル デバイス
- 低レベル デバイス フィルター ドライバー WDK シリアル デバイス
- 高度なデバイス フィルター ドライバー WDK シリアル デバイス
- フィルター ドライバー WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52da4849e530cf99f3d463ebfcae6cc739f0900d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378573"
---
# <a name="using-serialsys-and-serenumsys"></a>Serial.sys および Serenum.sys の使用

次のシステム コンポーネント、16550 ユニバーサル非同期受信側の送信元 (UART) と互換性のあるハードウェア インターフェイスをコント ローラーのシリアル デバイスで使用可能なのとおりです。

-   シリアルおよび Serenum ドライバー

    スタック (シリアル) は、シリアル デバイスのシステムによって提供される関数のドライバーです。 16550 UART と互換性のあるインターフェイスを必要とするプラグ アンド プレイ デバイスの種類にかかわらずシリアル低レベル デバイス フィルター ドライバーとして使用することもできます。

    Serenum.sys (Serenum) は、rs-232 ポートのプラグ アンド プレイのバス ドライバーの機能を提供するシリアル (または関数のベンダーから提供されたドライバー) と組み合わせて使用できる上位レベルのシステム提供されているデバイス フィルター ドライバーです。

    シリアルおよび Serenum の操作に関する詳細については、次のトピックを参照してください。

    - [シリアル コントローラー ドライバーの概要](serial-drivers-overview.md)
    - [シリアルおよび Serenum の機能](features-of-serial-and-serenum.md)
    - [シリアル デバイスとドライバーの構成](configuration-of-serial-devices-and-drivers.md)
    - [Serenum およびシリアルの操作](operation-of-serenum-and-serial.md)
    - [シリアルのレジストリ設定](registry-settings-for-serial.md)
    - [Serenum のレジストリ設定](registry-settings-for-serenum.md)
    - [シリアル ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
    - [Serenum ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
    - WDK で Ntddser.h ヘッダー ファイル内のデータ定義します。

<!-- -->

- ポート[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)

    ポート クラスが含まれています*シリアル ポート*と*COM ポート*します。 シリアル ポートは、16550 UART または互換性のあるデバイスのシリアル通信ハードウェア インターフェイスです。 コンピューターで、rs-232 ポートは、DB ~ 9 または電気 UART のシリアル ポートに接続されている DB 25 コネクタでは通常。 COM ポートは、追加の Windows に固有の要件に準拠するシリアル ポートです。 詳細については、次を参照してください。 [COM ポートの構成](configuration-of-com-ports.md)します。

- COM ポート[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)

    COM ポートのデバイスのインターフェイスを使用して、COM ポートにアクセスする必要があります。 (COM ポートのデバイスのインターフェイス クラスの GUID は[ **GUID\_DEVINTERFACE\_com ポート**](https://docs.microsoft.com/windows-hardware/drivers/install/guid-devinterface-comport))。

- [COM ポート データベース](com-port-database.md)と[COM ポート データベース サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

    COM ポートのデータベースを介し COM ポートでの COM ポート番号を使用します。

シリアル デバイスをインストールする方法の詳細については、次を参照してください。[シリアル デバイスのインストール](installing-serial-devices.md)します。

シリアル デバイスの高度な操作については、Microsoft Windows SDK の Windows ベースのサービスでサポートされている通信リソースに関する情報を参照してください。

## <a name="serial-driver-samples"></a>シリアル ドライバーのサンプル

これらのサンプルでは、シリアル ドライバーについて説明します。

- [シリアル](https://go.microsoft.com/fwlink/p/?LinkId=617962)サンプルは、シリアル デバイスの機能のドライバーをビルドします。
- [Serenum](https://go.microsoft.com/fwlink/p/?LinkId=617961)サンプルは、ポートの rs-232 バス ドライバーのプラグ アンド プレイの機能を提供します。
- 単純な仮想シリアル ドライバー (人) とコント ローラーのないモデム ドライバー (FakeModem)。
    -   [仮想シリアル ドライバーのサンプル (UMDF 1.0)](https://go.microsoft.com/fwlink/p/?LinkId=617963)
    -   [仮想 serial2 ドライバー サンプル (KMDF)](https://go.microsoft.com/fwlink/p/?LinkId=722209)

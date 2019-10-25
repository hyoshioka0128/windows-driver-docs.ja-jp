---
title: Serial.sys および Serenum.sys の使用
description: Serial.sys および Serenum.sys の使用
ms.assetid: 2dcf22c8-0666-4b58-8fd3-97a4d17eaa2a
keywords:
- シリアルポート WDK
- シリアルデバイス WDK
- ポート WDK、シリアル
- ユニバーサル非同期受信側-送信機 WDK シリアルデバイス
- UART WDK シリアルデバイス
- 関数ドライバー WDK シリアルポート
- シリアルドライバー WDK
- 16550 UART 互換インターフェイス WDK シリアルデバイス
- 低レベルのデバイスフィルタードライバー WDK シリアルデバイス
- 高レベルのデバイスフィルタードライバー WDK シリアルデバイス
- フィルタードライバー WDK シリアルデバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d0f5889c868b8a0221e268204008a08b49f14c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845385"
---
# <a name="using-serialsys-and-serenumsys"></a>Serial.sys および Serenum.sys の使用

次のシステムコンポーネントは、16550 universal 非同期受信機 (UART) と互換性のあるハードウェアインターフェイスを持つシリアルコントローラーデバイスで使用できます。

-   シリアルおよび Serenum.sys ドライバー

    Serial .sys (シリアル) は、システムによって提供されるシリアルデバイス用の関数ドライバーです。 また、16550 UART 互換インターフェイスを必要とする任意の種類のプラグアンドプレイデバイスに対して、シリアルを下位レベルのデバイスフィルタードライバーとして使用することもできます。

    Serenum.sys (Serenum.sys) は、システムによって提供される上位レベルのデバイスフィルタードライバーであり、Serial (またはベンダーが提供する関数ドライバー) と組み合わせて使用して、RS-232 ポート用のプラグアンドプレイバスドライバーの機能を提供できます。

    シリアルおよび Serenum.sys の操作の詳細については、次のトピックを参照してください。

    - [シリアル コントローラー ドライバーの概要](serial-drivers-overview.md)
    - [Serial および Serenum.sys の機能](features-of-serial-and-serenum.md)
    - [シリアルデバイスとドライバーの構成](configuration-of-serial-devices-and-drivers.md)
    - [Serenum.sys とシリアルの操作](operation-of-serenum-and-serial.md)
    - [シリアルのレジストリ設定](registry-settings-for-serial.md)
    - [Serenum.sys のレジストリ設定](registry-settings-for-serenum.md)
    - [シリアルドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
    - [Serenum.sys ドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
    - WDK の Ntddser ヘッダーファイル内のデータ定義。

<!-- -->

- ポート[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)

    Ports クラスには、*シリアルポート*と*COM ポート*が含まれています。 シリアルポートは、16550 UART または互換性のあるデバイスのシリアル通信ハードウェアインターフェイスです。 コンピューターの RS-232 ポートは、通常、UART のシリアルポートに電気的に接続されている DB-9 または DB-25 コネクタです。 COM ポートは、追加の Windows 固有の要件に準拠するシリアルポートです。 詳細については、「 [COM ポートの構成](configuration-of-com-ports.md)」を参照してください。

- COM ポート[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)

    Com ポートにアクセスするには、COM ポートのデバイスインターフェイスを使用する必要があります。 (COM ポートデバイスインターフェイスクラスの GUID は、 [**guid\_DEVINTERFACE\_COMPORT**](https://docs.microsoft.com/windows-hardware/drivers/install/guid-devinterface-comport)です)。

- [Com ポートデータベース](com-port-database.md)と[com ポートデータベースのサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

    Com ポートデータベースは、com ポートによる COM ポート番号の使用を判別します。

シリアルデバイスのインストールの詳細については、「[シリアルデバイスのインストール](installing-serial-devices.md)」を参照してください。

シリアルデバイスの高レベル操作に関する一般的な情報については、Microsoft Windows SDK で Windows ベースサービスによってサポートされている通信リソースに関する情報を参照してください。

## <a name="serial-driver-samples"></a>シリアル ドライバーのサンプル

これらのサンプルはシリアルドライバーを示しています。

- [シリアル](https://go.microsoft.com/fwlink/p/?LinkId=617962)サンプルでは、シリアルデバイス用の関数ドライバーをビルドします。
- この[serenum.sys](https://go.microsoft.com/fwlink/p/?LinkId=617961)サンプルには、RS-232 ポート用のバスドライバーのプラグアンドプレイ機能が用意されています。
- 単純な仮想シリアルドライバー (ComPort) とコントローラーレスモデムドライバー (FakeModem)。
    -   [仮想シリアルドライバーのサンプル (UMDF 1.0)](https://go.microsoft.com/fwlink/p/?LinkId=617963)
    -   [Virtual serial2 driver サンプル (KMDF)](https://go.microsoft.com/fwlink/p/?LinkId=722209)

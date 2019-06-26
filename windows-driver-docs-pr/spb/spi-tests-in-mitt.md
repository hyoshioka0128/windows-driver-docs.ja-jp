---
title: MITT の SPI テスト
description: SPI は、ミット ソフトウェア パッケージに含まれているモジュールをテストします。
ms.assetid: 8240841C-FFA0-48EC-AB7E-4E15E262C23D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8aa57f7d98267fede6aa847a28ed84410bb7ff8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376902"
---
# <a name="spi-tests-in-mitt"></a>MITT の SPI テスト


**最終更新日**

-   2015 年 1 月

**適用対象:**

-   Windows 8.1

ミット ソフトウェア パッケージに含まれている SPI テスト モジュールを使用して、SPI コント ローラーとそのドライバーのテスト対象のシステム上のデータ転送をテストできます。 ミット ボードは、SPI バスに接続されているクライアント デバイスとして機能します。

## <a name="before-you-begin"></a>開始する前にしています.


-   ミット ボードおよび SPI または UART アダプター ボードを取得します。 参照してください[ミットを使用するためのハードウェアを購入](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)します。
-   [ミット ソフトウェア パッケージをダウンロード](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))します。 テスト対象のシステムにインストールします。
-   ミット ボード ミット ファームウェアをインストールします。 参照してください[ミット概要](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)します。

## <a name="hardware-setup"></a>ハードウェアのセットアップ


![spi ミット テスト](images/spi.jpg)

| バスのインターフェイス | 暗証番号 (pin)-不足                                      | ACPI と概略図 | 接続ソリューション                  |
|---------------|----------------------------------------------|---------------------|--------------------------------------|
| SPI           | (SCLK、MISO、MOSI、SS、GND) に必要なすべての行 | ACPI テーブル          | 単純なブロック ヘッダー (デバッグ ボード) |



1.  SPI アダプターを接続**JC1**ミット ボード。
2.  SPI アダプター ボード上、ジャンパー線を使用すると、適切な SPI 電圧を選択します。 ジャンパーは 3.3 v と 1.8 v を選択できます。
3.  テスト対象のシステムに SCLK、MOSI、MISO、SS、GND を接続します。

    ![spi 配線](images/spiwiring.png)

4.  スイッチを設定してミット ボード**SW1**位置にします。 この位置では、SPI の既定のモードができるように、ミットを利用したときにします。 シグナルが 3.3 v にある場合は、SPI アダプター ボード) (なし、ボード直接接続できます。

    ![spi 電源](images/spi-power.png)

## <a name="test-driver-and-acpi-configuration"></a>ドライバーのテストと ACPI の構成


I²C コント ローラーがテスト対象システムで次の手順に従います。

1.  このコマンドを実行して、ミット ソフトウェア パッケージに含まれる WITTTest ドライバーをインストールします。

    **pnputil –a witttest.inf**

    ![ミット ボード用インストール witt ドライバー](images/mitt-install-witt.png)

    **注**PnpUtil.exe が %systemroot% 内に含まれる\\System32 します。



2.  ACPI システムを変更し、この ASL テーブルが含まれます。 使用することができます、 [Microsoft ASL コンパイラ](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)します。

    **注**変更"\\\\\_SB\_します。SPI1"を次に示すようにテストする SPI コント ローラーの ACPI エントリ名にします。 SPI 頻度 1 Mhz、5 Mhz、および 20 Mhz で 3 つのテスト ターゲットを定義します。




``` syntax
Device(TP1) {
    Name (_HID, "SPT0001") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
          SpiSerialBus (0x0000, PolarityLow, FourWireMode, 0x08,ControllerInitiated, 0x000F4240, ClockPolarityLow,ClockPhaseFirst, "\\_SB.SPI1", 0x00, ResourceConsumer, , )
      })
      Return(RBUF)
    }
}
Device(TP2) {
    Name (_HID, "SPT0002") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
          SpiSerialBus (0x0000, PolarityLow, FourWireMode, 0x08,ControllerInitiated, 0x004c4b40, ClockPolarityLow,ClockPhaseFirst, "\\_SB.SPI1", 0x00, ResourceConsumer, , )
      })
      Return(RBUF)
    }
}
Device(TP3) {
    Name (_HID, "SPT0003") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
          SpiSerialBus (0x0000, PolarityLow, FourWireMode, 0x08,ControllerInitiated, 0x01312d00, ClockPolarityLow,ClockPhaseFirst, "\\_SB.SPI1", 0x00, ResourceConsumer, , )
      })
      Return(RBUF)
    }
}

```


## <a name="spi-automation-tests"></a>SPI オートメーションのテスト


1.  テスト対象システム上のフォルダーを作成します。
2.  TAEF バイナリ フォルダーをコピーし、PATH 環境変数に追加します。 必要な TAEF バイナリは %programfiles (x86) %\\Windows キット\\8.1\\テスト\\ランタイム\\TAEF します。
3.  ミット ソフトウェア パッケージから Muttutil.dll と Mittspitest.dll をフォルダーにコピーします。
4.  使用してすべてのミット SPI テストを表示、 **/list**オプション。

SPI テストを実行する準備が整いました。 すべてのテストを一度に 1 つのテストを実行したり、手動でテストを実行できます。

- 使用して 1 つのテストを実行、 **/name: *&lt;テスト名&gt;** * オプション。 このコマンドは、BasicIORead テストを実行します。
- このコマンドを使用して、すべてのテストを実行します。
- ミット ソフトウェア パッケージに含まれている SPBCmd.exe ツールを使用して手動でテストを実行します。

## <a name="spi-adapter-schematic"></a>SPI アダプターの概略図


![spi 概略図](images/spi-schematic.png)









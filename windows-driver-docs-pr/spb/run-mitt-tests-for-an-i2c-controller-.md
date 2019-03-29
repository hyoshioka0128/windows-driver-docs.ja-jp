---
title: MITT の I2C コントローラー テスト
description: ミット ソフトウェア パッケージに含まれている I²C テスト モジュールを使用して、I²C のコント ローラーとそのドライバーのデータ転送をテストできます。 ミット ボードは、I²C バスに接続されているクライアント デバイスとして機能します。
ms.assetid: E40B9ABB-B119-4EC1-A383-EB96CC350A25
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c75ff728d0ec8fa36aac492c746e039fde3c61db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578564"
---
# <a name="i2c-controller-tests-in-mitt"></a>MITT の I2C コントローラー テスト


**最終更新日**

-   2015 年 1 月

**適用対象します。**

-   Windows 8.1

ミット ソフトウェア パッケージに含まれている I²C テスト モジュールを使用して、I²C のコント ローラーとそのドライバーのデータ転送をテストできます。 ミット ボードは、I²C バスに接続されているクライアント デバイスとして機能します。

## <a name="before-you-begin"></a>開始する前にしています.


-   ミット ボードと I²C アダプターのボードを取得します。 参照してください[ミットを使用するためのハードウェアを購入](https://msdn.microsoft.com/library/windows/hardware/dn919811)します。
-   [ミット ソフトウェア パッケージをダウンロード](https://msdn.microsoft.com/library/windows/hardware/dn919810)します。 テスト対象のシステムにインストールします。
-   ミット ボード ミット ファームウェアをインストールします。 参照してください[ミット概要](https://msdn.microsoft.com/library/windows/hardware/dn919779)します。

## <a name="hardware-setup"></a>ハードウェアのセットアップ


![ミット i2c ハードウェアの設定](images/i2csetup.png)

| バスのインターフェイス | 暗証番号 (pin)-不足                             | ACPI と概略図 | 接続ソリューション                |
|---------------|-------------------------------------|---------------------|------------------------------------|
| I²C           | (SCL、SDA および GND) に必要なすべての行 | ACPI テーブル          | (デバッグ ボード) 単純な男性のブロック |



1.  I²C アダプターを接続**JB1**ミット ボード。

    ![ミット i2c ヘッダー](images/i2cheader.png)

2.  I²C ヘッダーにジャンパー線を使用して (上記**JB1**) 1.8 v と 3.3 v の間で適切な I²C 電圧を選択します。 このイメージに 1.8 v が選択されます。
3.  テスト対象システム上で公開されている SCL や SDA、GND 行には、アダプターの掲示板の SCL や SDA、GND ピンを接続します。

    ![i2c アダプター](images/i2c-power.png)

4.  I2C アダプター ボードのジャンパーを使用すると、適切な I2C 電圧 3.3 v と 1.8 v を選択します。 このイメージには、1.8 v が選択されています。
5.  スイッチを設定してミット ボード**SW0**位置にします。 この位置では、ミットを利用したときに、I²C の既定モードを有効します。

    ![ミット ボード sw0](images/sw0.png)

6.  使用して、**リセット**ミット基板に電源を入れボタンします。 I²C コント ローラーにネットワーク接続が正しい場合**LD7** (SDA インジケーター) と**LD6** (SCL インジケーター) を有効にします。 いずれかの LED がオンにならない場合、SDA または、SCL、またはその両方を低に取得されたために配線の問題があります。

## <a name="test-driver-and-acpi-configuration"></a>ドライバーのテストと ACPI の構成


I²C コント ローラーがテスト対象システムで次の手順に従います。

1.  このコマンドを実行して、ミット ソフトウェア パッケージに含まれる WITTTest ドライバーをインストールします。

    **pnputil –a witttest.inf**

    ![ミット ボード用インストール witt ドライバー](images/mitt-install-witt.png)

    **注**PnpUtil.exe が %systemroot% 内に含まれる\\System32 します。



2.  ACPI システムを変更し、この ASL テーブルが含まれます。 使用することができます、 [Microsoft ASL コンパイラ](https://msdn.microsoft.com/library/windows/hardware/dn551195)します。

    **注**変更"\\\\\_SB\_します。I2C2"I²C コント ローラーからテストの ACPI エントリ名にします。




``` syntax
//TP1 100Khz Standard Target Device(TP1) 
Device(TP1) {
    Name (_HID, "STK0001") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x11, ControllerInitiated, 100000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}

//TP2 400Khz  Fast Target
Device(TP2) {
    Name (_HID, "STK0002") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x12, ControllerInitiated, 400000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}

//TP3 1 Mhz  FastPlus Target
Device(TP3) {
    Name (_HID, "STK0003") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x13, ControllerInitiated, 1000000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
  }
}

//TP4 1.4 Mhz High Speed, optional target
Device(TP4) {
    Name (_HID, "STK0004") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x14, ControllerInitiated, 1400000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}

//TP5 3.4 Mhz High Speed, optional target
Device(TP5) {
    Name (_HID, "STK0005") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x15, ControllerInitiated, 3400000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}
```

**注**ミット I²C テストを実行する TP1 3 のみが必要です。 TP4 および TP5 も、省略可能な対象です。




## <a name="ic-automation-tests"></a>I²C オートメーションのテスト


1.  テスト対象システム上のフォルダーを作成します。
2.  TAEF バイナリ フォルダーをコピーし、PATH 環境変数に追加します。 必要な TAEF バイナリは %programfiles (x86) %\\Windows キット\\8.1\\テスト\\ランタイム\\TAEF します。
3.  ミット ソフトウェア パッケージから Muttutil.dll と Mitti2ctest.dll をフォルダーにコピーします。
4.  使用してすべてのミット I²C テストを表示、 **/list**オプション。

    ![ミット i2c コマンド](images/mitt-i2c-cmds.png)

I²C テストを実行する準備が整いました。 すべてのテストを一度に 1 つのテストを実行したり、手動でテストを実行できます。

- 使用して 1 つのテストを実行、 **/name: *&lt;テスト名&gt;*** オプション。 このコマンドは、BasicIORead テストを実行します。

  ![ミット i2c コマンド](images/mitt-i2c-cmds1.png)

- このコマンドを使用して、すべてのテストを実行します。

  ![ミット i2c コマンド](images/mitt-i2c-cmds2.png)

- ミット ソフトウェア パッケージに含まれている SPBCmd.exe ツールを使用して手動でテストを実行します。

## <a name="ic-adapter-schematic"></a>概略 I²C アダプター


![i2c 概略図](images/i2c-schematic.png)

## <a name="related-topics"></a>関連トピック
[複数のインターフェイスのテスト ツール (ミット) でのテスト](https://msdn.microsoft.com/library/windows/hardware/dn919874)  




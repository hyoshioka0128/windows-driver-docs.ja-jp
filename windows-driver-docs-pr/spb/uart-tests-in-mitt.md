---
title: MITT の UART テスト
description: ミット ソフトウェア パッケージには、UART コント ローラーとそのドライバーへのデータ転送を検証するためのテストが含まれています。 ミット board's UART インターフェイスは、UART ループバック デバイスとして機能します。
ms.assetid: 239F131C-5416-4E86-B0EE-E3156CDA11CF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d10f5806800bae881ad640cc97b5d7a06335a6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383517"
---
# <a name="uart-tests-in-mitt"></a>MITT の UART テスト


**最終更新日**

-   2015 年 1 月

**適用対象:**

-   Windows 8.1

ミット ソフトウェア パッケージには、UART コント ローラーとそのドライバーへのデータ転送を検証するためのテストが含まれています。 ミット board's UART インターフェイスは、UART ループバック デバイスとして機能します。

## <a name="before-you-begin"></a>開始する前にしています.


-   ミット ボードと UART アダプターのボードを取得します。 参照してください[ミットを使用するためのハードウェアを購入](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)します。
-   [ミット ソフトウェア パッケージをダウンロード](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))します。 テスト対象のシステムにインストールします。
-   ミット ボード ミット ファームウェアをインストールします。 参照してください[ミット概要](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)します。

## <a name="hardware-setup"></a>ハードウェアのセットアップ


![ミット uart ハードウェアの設定](images/mitt-uart.jpg)

1.  外部 PIN アウト ミット ボード UART インターフェイスをテスト対象システムの UART コント ローラーに接続する必要があります。 UART コント ローラーは、暗証番号 (pin) の完全な詳細を公開する場合に直接接続**JB1**掲示板の。
2.  これらの行を接続します。

    | ミット ボード UART インターフェイス | テスト対象システムで UART コント ローラー |
    |----------------------------------|------------------------------------------|
    | テキサス州                               | RX                                       |
    | RTS                              | テクニカル サポート                                      |
    | RX                               | テキサス州                                       |
    | テクニカル サポート                              | RTS                                      |

     

3.  UART アダプター ボードは、正しい電圧を選択するためのジャンパーを提供します。 3\.3 v のみシグナルが直接サポートされているアダプター ボード) を含めずに接続します。

    ![uart 配線](images/uart-wiring.png)

## <a name="test-driver-and-acpi-configuration"></a>ドライバーのテストと ACPI の構成


ACPI テーブルを変更するには、Windows ハードウェア認定キット (HCK) 8.1 をインストールします。 UART コント ローラーがテスト対象システムで次の手順に従います。

1.  Device.BusController.UART.HCKTestability 要件で説明されているシステムの変更を実行します。
2.  ACPI テーブルの下で提供されているテンプレートに基づく UART テスト ドライバーを更新\\ \\ &lt;hckcontrollername&gt;\\テスト\\&lt;アーキテクチャ&gt;\\UART\\サンプル UART.asl またはこの例を使用します。 使用することができます、 [Microsoft ASL コンパイラ](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)します。

    ``` syntax
    Device(UART) {
        Name (_HID, "UTK0001")
        Name (_CID, "UARTTest")
        Name (_UID,0)
        Method (_CRS, 0x0, NotSerialized) {
            Name (
                RBUF,
                ResourceTemplate () {
                    UARTSerialBus (
                        115200, // Baud Rate = 115200
                        DataBitsEight,
                        StopBitsOne,
                        0xC0,
                        LittleEndian,
                        ParityTypeNone,
                        FlowControlHardware, 
                        32,
                        32,
                        "\\_SB.UAR4",,,,
                    )
                }
            )
        Return(RBUF)
        }
    }
    ```

3.  UARTTest テスト周辺ドライバーをインストールする\\ \\ &lt;hckcontrollername&gt;\\テスト\\&lt;アーキテクチャ&gt;\\によって UARTこのコマンドを実行します。

    **pnputil – a UARTTest.inf**

## <a name="uart-automation-tests"></a>UART オートメーションのテスト


1.  ドライバーのテストと ACPI の構成」に記載の手順に従います。
2.  テスト対象システム上のフォルダーを作成します。
3.  これらのファイルを %programfiles (x86) % からコピー\\Windows キット\\8.1\\テスト\\ランタイム\\TAEF フォルダーにします。
    -   Wex.Common.dll
    -   Wex.Communication.dll
    -   Wex.Logger.dll

4.  ミット ソフトウェア パッケージから UtsSanity.exe と muttutil.dll をコピーします。
5.  使用可能なすべてのコマンドを表示、UtsSanity.exe - を起動しますか。 使用可能なコマンド ライン オプションを参照してください。**注**  、 **– ミット**オプションはミット ボードが接続されているテストの実行に必要です。

     

例 1:115200 bps (既定値) でテストを実行するには

**C:\\uart&gt; UtsSanity.exe – ミット**

例 2:3 mbps でテストを実行します。

**C:\\uart&gt; UtsSanity.exe-ミット – baudRate 3000000**

## <a name="uart-adapter-schematic"></a>概略 UART アダプター


![spi 概略図](images/spi-schematic.png)

 

 





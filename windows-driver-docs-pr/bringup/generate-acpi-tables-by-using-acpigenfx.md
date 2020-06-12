---
title: AcpiGenFx を使用して ACPI テーブルを生成する
description: Acpi 生成フレームワーク (AcpiGenFx) ライブラリを使用して、ACPI テーブルを生成するアプリを作成します。
ms.assetid: 46A725C3-609E-45B9-A4BD-033656208E92
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: faa0b01c0a5f019876a7a44f193524c7a1943d65
ms.sourcegitcommit: 6bd546fea677833fc20cd802256d030633ac562e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84717447"
---
# <a name="generate-acpi-tables-by-using-acpigenfx"></a>AcpiGenFx を使用して ACPI テーブルを生成する

## <a name="summary"></a>まとめ

- AcpiGenFx を使用して ACPI テーブルを生成する .NET アプリを作成する

## <a name="applies-to"></a>適用対象

- Windows 10

- Windows SoC および platform の導入

## <a name="important-apis"></a>重要な API

- オブジェクトブラウザーで AcpiGenFx を開く

- Visual Studio の IntelliSense 機能を使用して、メソッドとプロパティを決定する

Acpi 生成フレームワーク (AcpiGenFx) ライブラリを使用して、ACPI テーブルを生成するアプリを作成します。

Windows 10 では、新しい C# ライブラリである AcpiGenFx を使用すると、ハードウェアデバイスとプラットフォーム上のリソース (割り込みコントローラー、SD ホストコントローラー、GPIO、I ² C デバイスなど) を記述する ACPI テーブルを作成するアプリを簡単に作成できます。 フレームワークオブジェクトによって公開されているメソッドとプロパティを使用して、デバイス、リソース、および依存関係を記述できます。 ACPI テーブルの正確な構文や、ACPI 仕様を知る必要はありません。 AcpiGenFx は、OS に依存しない ACPI 機械言語 (ASL) コードを生成するだけでなく、Windows 固有の要件も認識しています。

アプリは、これらの説明に基づいて、関連する ACPI テーブルファイル ( \* aslc と asl) を生成し \* ます。 ビルド時に、AcpiGenFx はプラットフォームの説明を静的に分析し、循環または未解決の依存関係、デバイスの名前付けと UUID の競合、リソースからコントローラーへのマッピングなどのエラーを検出します。 結果として、生成された ASL コードのデバッグが容易になります。これは、AcpiGenFx が最も一般的な誤りを確認し、固有の ACPI 実装の詳細を抽象化するためです。

AcpiGenFx は本質的に宣言されています。出力は静的データのみであり、動的なランタイムメソッドを生成するようには設計されていません。 高度な非 SoC 周辺機器の電源管理など、ユースケースがフレームワークでカバーされていない場合、メソッドは Windows プラットフォーム拡張機能ドライバーで実装するか、AcpiGenFx によって生成される ASL コードに手動で追加する必要があります。

## <a name="before-you-begin"></a>開始する前に

WDK インストールの**AcpiGenFx**フォルダーにある次のファイルを見つけます。

> [!NOTE]
> AcpiGenFx.dll と関連付けられているサンプルは、WDK の Tools フォルダーにあります。 Tools ディレクトリで、ターゲットアーキテクチャフォルダーに移動し、次に AcpiGenFx フォルダーに移動します。 たとえば、x86 バージョンは C:\Program Files (x86) \Windows Kits\10\Tools\x86\ACPIGenFx. にあります。

- AcpiGenFx.dll

    ACPIGenFx を使用するために必要です。

- DSDTSamples

    このプロジェクトは、プラットフォーム全体の ACPI ファームウェアを設計するための出発点として使用します。 出力は、DSDT、FADT、MADT を含む ACPI テーブルの完全なセットです。

- SSDTSamples

    このプロジェクトを出発点として使用して、既存のシステムに周辺機器を追加します。 このサンプルでは、センサーデバイスとそのリソースを記述する方法を示します。 出力は、ASL の ACPI SSDT テーブルです。

Windows 10 キット、ツール、およびコードサンプルをダウンロードします。

- [Microsoft Visual Studio](https://visualstudio.microsoft.com/)

- [Windows 10 用 windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)

- [Windows Driver Kit (WDK) のサンプル](https://github.com/Microsoft/Windows-driver-samples)

## <a name="create-a-platform"></a>プラットフォームを作成する

1. Visual Studio で、新しい C# コンソールプロジェクトを開きます。

1. AutoAcpi.dll アセンブリへの参照を追加します。 [**プロジェクト**] メニューの [**参照の追加**] をクリックします。 [**参照**] をクリックし、AutoAcpi.dll の場所に移動します。 **[OK]** をクリックします。

1. **ソリューションエクスプローラー**で、[**参照**] を展開し、[ **acpigenfx**] を選択します。 オブジェクトブラウザーのオブジェクトを表示します (** &gt; オブジェクトブラウザーの表示**)。

1. ターゲット .NET Framework 4.5 以降。 プロジェクトのプロパティを開きます。 [**アプリケーション**] ページで、[**ターゲットフレームワーク**] が **.NET Framework 4.5**に設定されていることを確認します。

1. `Using`アプリケーションのコードの先頭に AutoAcpi オブジェクトのディレクティブを追加します。

1. Platform オブジェクトを作成します。 アーキテクチャに応じて、 **CreateArmPlatform**または**Createx86Platform**を呼び出して**platform**オブジェクトをインスタンス化します。 *OEMID*、 *oemtableid*、 *Creator*、 *Revision*、および*FileName*を指定します。

1. ファイルに書き込むには、 **Platform. WriteAsl**を呼び出します。

    この例では、プラットフォームをインスタンス化する方法を示します。

    ```cs
    using AutoAcpi;

    namespace ACPI
    {
        class Program
        {
            static void Main(string[] args)
            {
                ArmPlatform myPlatform = Platforms.CreateArmPlatform(
                    OEMID: "MSFT",
                    OEMTableID: "EDK2",
                    CreatorID: "MSFT",
                    Revision: 1,
                    FileName: "Platform");

                myPlatform.WriteAsl();
            }
        }
    }
    ```

1. [**開始**] をクリックして、アプリをビルドして実行します。 Visual Studio の [**出力**] ウィンドウにビルドの進行状況が表示されます。 (**出力**ウィンドウが表示されていない場合は、[**表示**] メニューの [**出力**] をクリックします)。

1. [*プロジェクト* \\ bin \\ *デバッグ] または [リリース*出力] の下にあるという名前のフォルダーを開き \\ ます。 出力フォルダーには、アプリによって生成されるファイルが含まれています。 SSDT の内容を表示します。 asl

    前の例の出力を次に示します。

    ```console
    DefinitionBlock ("Platform.aml", "DSDT", 5, "MSFT", "EDK2", 1)
    {
        Scope (\_SB_)
        {
        }

    }
    ```

このアプリでは、Aslc と Bin という2つの追加フォルダーが生成されます。 Aslc には、aslc 形式のすべてのファームウェアテーブルが含まれています。 Bin には、バイナリ blob 形式のすべてのファームウェアテーブルが含まれています。

WDK に用意されている asl.exe コンパイラを使用して、ASL コードファイルを ACPI 機械語 (AML) バイナリにコンパイルします。

## <a name="add-devices-and-resources-in-the-dsdt"></a>DSDT にデバイスとリソースを追加する

コンポーネントをプラットフォームに追加できます。 通常、これらのコンポーネントには、プロセッサ、バスコントローラー、電源リソースなどが含まれます。 ここでは、DSDTSamples で使用されるコンポーネントをいくつか紹介します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>オブジェクトの種類</th>
<th>作成方法</th>
<th>コンポーネント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ACAdapter</strong></td>
<td><strong>Platform. AddACAdapter</strong></td>
<td>AC アダプターを追加します。</td>
</tr>
<tr class="even">
<td><strong>BatteryDevice</strong></td>
<td><p><strong>AddBatteryDevice</strong></p>
<p><strong>BatteryDevice の制限</strong></p></td>
<td>バッテリデバイスを追加し、その温度制限を指定します。</td>
</tr>
<tr class="odd">
<td><strong>ButtonArrayDevice</strong></td>
<td><p><strong>Platform. AddButtonArrayDevice</strong></p>
<p><strong>ButtonArrayDevice. AddBackButton</strong></p>
<p><strong>AddCameraShutterButton</strong></p>
<p><strong>AddCameraAutofocusButton</strong></p>
<p><strong>ButtonArrayDevice. AddGenericButton</strong></p>
<p><strong>ButtonArrayDevice. AddPowerButton</strong></p>
<p><strong>AddRotationLockButton</strong></p>
<p><strong>ButtonArrayDevice. AddSearchButton</strong></p>
<p><strong>ButtonArrayDevice. AddVolumeDownButton</strong></p>
<p><strong>ButtonArrayDevice. AddVolumeUpButton</strong></p>
<p><strong>ButtonArrayDevice. AddWindowsHomeButton</strong></p></td>
<td>Windows Home、Back、Volume +/-、Power、Rotation Lock、Search などのボタンを追加します。</td>
</tr>
<tr class="even">
<td><strong>DisplaySensor</strong></td>
<td><strong>Platform. AddDisplaySensor</strong></td>
<td>ディスプレイセンサーを追加します。</td>
</tr>
<tr class="odd">
<td><strong>GenericDevice</strong></td>
<td><strong>Platform. AddGenericDevice</strong></td>
<td>フレームワークで内部でサポートされている任意の種類のデバイスを置き換えるために使用できる汎用デバイスを追加します。</td>
</tr>
<tr class="even">
<td><strong>GpioController</strong></td>
<td><strong>Platform. AddGpioController</strong></td>
<td>GPIO コントローラーと、割り込み、i/o、イベントなどの関連リソースを追加します。</td>
</tr>
<tr class="odd">
<td><strong>HidOverI2C</strong></td>
<td><strong>AddHidI2CDevice</strong></td>
<td>I ² C バスに接続されている HID デバイスを追加します。</td>
</tr>
<tr class="even">
<td><strong>I2CController</strong></td>
<td><strong>AddI2CController</strong></td>
<td>I ² C コントローラーと、割り込み、i/o、イベントなどの関連リソースを追加します。</td>
</tr>
<tr class="odd">
<td><strong>KDNet2Usb</strong></td>
<td><strong>AddKDNet2Usb</strong></td>
<td>USB 経由で Kdnet を使用して、カーネルデバッグのサポートを追加します。</td>
</tr>
<tr class="even">
<td><strong>PEPDevice</strong></td>
<td><strong>AddPepDevice</strong></td>
<td>PEP デバイスとそのリソース、およびパッケージと静的な型を返すメソッドを追加します。</td>
</tr>
<tr class="odd">
<td><p><strong>プロセッサ</strong></p>
<p><strong>ProcessorAggregator</strong></p></td>
<td><p><strong>Platform. AddProcessor</strong></p>
<p><strong>Platform. AddProcessorAggregator</strong></p></td>
<td>プロセッサとプロセッサアグリゲーターを追加します。</td>
</tr>
<tr class="even">
<td><strong>RTCDevice</strong></td>
<td><strong>プラットフォーム. AddRTCDevice</strong></td>
<td>ACPI 時間とアラームデバイスを追加します。</td>
</tr>
<tr class="odd">
<td><strong>SdHostController</strong></td>
<td><strong>AddSdHostController</strong></td>
<td>SD ホストコントローラーを追加します。</td>
</tr>
<tr class="even">
<td><strong>SerialPort</strong></td>
<td><strong>AddSerialPort</strong></td>
<td>シリアルおよび UART デバイスのサポートを追加します。</td>
</tr>
<tr class="odd">
<td><strong>悪意のあるゾーン</strong></td>
<td><strong>Platform.object ゾーン</strong></td>
<td>サーマルゾーンと関連付けられているサンプリング間隔とポーリング期間を追加します。</td>
</tr>
<tr class="even">
<td><p><strong>XhciUsbController</strong></p>
<p><strong>EhciUsbController</strong></p>
<p><strong>UsbDevice</strong></p></td>
<td><p><strong>Platform. AddEhciUsbController</strong></p>
<p><strong>AddXhciUsbController</strong></p>
<p><strong>EhciUsbController. AddUsbDevice</strong></p>
<p><strong>XhciUsbController. AddUsbDevice</strong></p>
<p><strong>UsbDevice. AddUsbDevice</strong></p></td>
<td>USB ホストコントローラーと子デバイス (ハブを含む) を追加します。</td>
</tr>
</tbody>
</table>

完全な一覧を表示するには、**オブジェクトブラウザー**で AcpiGenFx を開きます。 IntelliSense を使用して、オブジェクトによって公開されているメソッド (およびパラメーター) とプロパティを決定します。 クラスを追加し、前の表に示したプロパティを設定する方法を示すコード例については、DSDTSamples プロジェクトを参照してください。

## <a name="add-debug-support"></a>デバッグサポートの追加

ポートをデバッグ可能として設定するには、オブジェクトの**DebugEnabled**プロパティを "true" に設定します。

たとえば、USB デバッグポートを使用して xHCI ホストコントローラーを記述することができます。 アプリで、 **AddXhciUsbController**を呼び出して**XhciUsbController**オブジェクトを取得し、 **DebugEnabled**プロパティを "true" に設定します。 AcpiGenFx は、アプリの出力 aslc フォルダーに自動的に含まれる Microsoft DBG2 テーブルを生成し \\ ます。

XHCI ホストコントローラーを追加し、デバッグ可能として宣言する方法の例を次に示します。

```cs

XhciUsbController usb1 = Platform.AddXhciUsbController("USB1", "XHCICONT", 0);
usb1.Description = "USB Controller with Debug Support";

Memory32Fixed mem = usb1.AddMemory32Fixed(true, 0xf9000000, 0xfffff, "");
usb1.AddMemory32Fixed(true, 0xf7000000, 0xfffff, "");
usb1.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Shared, 0x8);
usb1.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Shared, 0x9);

usb1.DebugEnabled = true;
mem.DebugAccessSize = DebugAccessSize.DWordAccess;
```

前のスニペットでは、xHCI ホストコントローラーに割り込みリソースがあり、デバッグがサポートされています。 PEP デバイスと GPIO コントローラーに依存関係があります。 これらのデバイスの説明については、「DSDTSamples」を参照してください。

この例では、I ² C コントローラーを DSDT に追加する方法を示します。

```cs
I2CController i2c = Platform.AddI2CController("I2C1", "I2CCONTR", 0);
i2c.AddMemory32Fixed(true, 0xf9999000, 0x400, "");
i2c.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Exclusive, 40);
```

ここでは、xHCI host と I ² C コントローラーの前の定義を使用したコンソールアプリの出力を示します。

```console

DefinitionBlock ("Platform.aml", "DSDT", 5, "MSFT", "EDK2", 1)
{
    Scope (\_SB_)
    {
        //
        // Description: USB Controller with Debug Support
        //

        Device (USB1)
        {
            Name (_HID, "XHCICONT")
            Name (_CID, "PNP0D10")
            Name (_UID, 0x0)
            Method (_STA)
            {
                Return(0xf)
            }
            Method (_CRS, 0x0, NotSerialized) {
                Name (RBUF, ResourceTemplate () {
                    MEMORY32FIXED(ReadWrite, 0xF9000000, 0xFFFFF, )
                    MEMORY32FIXED(ReadWrite, 0xF7000000, 0xFFFFF, )
                    Interrupt(ResourceConsumer, Level, ActiveHigh, Shared) { 0x8 }
                    Interrupt(ResourceConsumer, Level, ActiveHigh, Shared) { 0x9 }
                })
                Return(RBUF)
            }
        }

        //
        // Description: This is an i2cController.
        //

        Device (I2C1)
        {
            Name (_HID, "I2CCONTR")
            Name (_CID, "")
            Name (_UID, 0x0)
            Method (_STA)
            {
                Return(0xf)
            }
            Method (_CRS, 0x0, NotSerialized) {
                Name (RBUF, ResourceTemplate () {
                    MEMORY32FIXED(ReadWrite, 0xF9999000, 0x400, )
                    Interrupt(ResourceConsumer, Level, ActiveHigh, Exclusive) { 0x28 }
                })
                Return(RBUF)
            }
        }

    }

}  
```

プロジェクトをビルドした後、プロジェクトディレクトリで [出力 \\ aslc] に移動します。 Dbg2 ファイルには、次に示す DB2 テーブルが含まれています。

```asl

// Debug Port Table (DBG2)
// Automatically generated by AutoAcpi

#include "AutoACPI.h"
char DBG2[112] = {
    0x44, 0x42, 0x47, 0x32, 0x70, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x4D, 0x53, 0x46, 0x54, 0x20, 0x20, 0x45, 0x44, 0x4B, 0x32,
    0x20, 0x20, 0x20, 0x20, 0x01, 0x00, 0x00, 0x00, 0x4D, 0x53,
    0x46, 0x54, 0x01, 0x00, 0x00, 0x00, 0x2C, 0x00, 0x00, 0x00,
    0x01, 0x00, 0x00, 0x00, 0x00, 0x44, 0x00, 0x02, 0x0E, 0x00,
    0x36, 0x00, 0x00, 0x00, 0x44, 0x00, 0x02, 0x80, 0x00, 0x00,
    0x00, 0x00, 0x16, 0x00, 0x2E, 0x00, 0x00, 0x00, 0x00, 0x03,
    0x00, 0x00, 0x00, 0xF9, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01, 0x00, 0x00, 0x00, 0xF7, 0x00, 0x00, 0x00, 0x00,
    0xFF, 0xFF, 0x0F, 0x00, 0xFF, 0xFF, 0x0F, 0x00, 0x22, 0x5C,
    0x5C, 0x5F, 0x53, 0x42, 0x5F, 0x2E, 0x55, 0x53, 0x42, 0x31,
    0x22, 0x00
};

void * ReferenceDBG2Table(void) {
    return (void *) &DBG2;
}
```

## <a name="add-an-acpi-description-for-a-peripheral-device-in-the-ssdt"></a>SSDT で周辺機器の ACPI の説明を追加する

1. **CreateArmPlatform**または**Createx86Platform**を呼び出して、platform オブジェクトを作成します。

1. **SSDT**プロパティを true に設定します。 これは、このテーブルが SSDT であることをフレームワークに示します。

1. デバイスを作成し、リソースを割り当てます。 たとえば、ここに示されているセンサーデバイスの場合、このサンプルでは、 **Platform. AddGenericDevice**を呼び出し、デバイス名、ハードウェア ID、および一意のインスタンスを指定します。 DSDT で説明されている I ² C serial bus, I2C1 に接続するセンサーデバイス。

> [!NOTE]
> Microsoft は、多様で inclusionary な環境をサポートしています。 このドキュメント内には、"スレーブ" という語への参照があります。 Microsoft の[バイアスフリー通信](https://docs.microsoft.com/style-guide/bias-free-communication)用スタイルガイドでは、これを exclusionary 語として認識しています。 この表現は、現在ソフトウェア内で使用されている用語として使用されています。

```asl
namespace SSDTSample
{
    class Program
    {
        static void Main(string[] args)
        {

          ArmPlatform Platform = Platforms.CreateArmPlatform(
                OEMID: "MSFT",
                OEMTableID: "EDK2",
                CreatorID: "MSFT",
                Revision: 1,
                FileName: "SSDT"
                );

            platform.SSDT = true;

            var sensor = platform.AddGenericDevice("ADXL", "ACPI\\ADXL345Acc", 1);

            sensor.AddI2CSerialBus(
                SlaveAddress: 0x1d,
                Mode: SlaveMode.ControllerInitiated,
                ConnectionSpeed: 400000,
                addressmode: AddressMode._7Bit,
                controllername: "I2C1"
                );

            platform.WriteAsl();

        }
    }
}
```

前の例の出力を次に示します。

```console
DefinitionBlock ("SSDT.aml", "SSDT", 5, "MSFT", "EDK2", 1)
{
    Scope (\_SB_)
    {

        Device (ADXL)
        {
            Name (_HID, "ACPI\ADXL345Acc")
            Name (_UID, 0x1)
            Method (_STA)
            {
                Return(0xf)
            }
            Method (_CRS, 0x0, NotSerialized) {
                Name (RBUF, ResourceTemplate () {
                    I2CSerialBus(0x1D, ControllerInitiated, 0x61A80, AddressingMode7Bit, "I2C1", 0, ResourceConsumer, , RawDataBuffer() { 0 })
                })
                Return(RBUF)
            }
        }

    }

}
```

## <a name="replacing-acpi-firmware-during-development-and-testing"></a>開発およびテスト中の ACPI ファームウェアの置換

開発とテストのシナリオでは、デバイスの asl.exe コンパイラから生成された AML バイナリを置き換えることができます。 これを行うには、AML バイナリの名前を acpitabl に変更し、% windir% system32 に移動し \\ ます。 ブート時に、Windows は、ACPI ファームウェアに存在するテーブルを acpitabl のテーブルに置き換えます。

次のコマンドを使用して、テスト署名が有効になっていることを確認します。

```console
bcdedit /set testsigning on
```

## <a name="related-topics"></a>関連トピック

[ACPI システム記述テーブル](acpi-system-description-tables.md)  

---
title: AcpiGenFx を使用して ACPI テーブルを生成する
description: ACPI テーブルを生成するアプリを記述するのにには、ACPI 生成フレームワーク (AcpiGenFx) ライブラリを使用します。
ms.assetid: 46A725C3-609E-45B9-A4BD-033656208E92
ms.date: 06/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7efa87cc6abe752b1692adcc88b62426aeca797e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581974"
---
# <a name="generate-acpi-tables-by-using-acpigenfx"></a>AcpiGenFx を使用して ACPI テーブルを生成する


**概要**

-   ACPI テーブルを生成する AcpiGenFx を使用する .NET アプリを作成します。

**適用対象**

-   Windows 10
-   Windows SoC やプラットフォーム bring アップ

**重要な API**

-   オブジェクト ブラウザーで開く AcpiGenFx
-   Visual Studio での IntelliSense 機能を使用して、メソッドとプロパティを確認するには

ACPI テーブルを生成するアプリを記述するのにには、ACPI 生成フレームワーク (AcpiGenFx) ライブラリを使用します。

Windows 10 で、新しいC#AcpiGenFx、ライブラリを簡単に割り込みコント ローラー、SD ホスト コント ローラー、GPIO など、プラットフォームのハードウェア デバイスとリソースを説明する ACPI テーブルを作成するアプリを作成して I²C デバイス。 メソッドと framework オブジェクトによって公開されるプロパティを使用すると、ACPI テーブルの正確な構文を知ることや、ACPI 仕様を参照するには、デバイス、リソース、および依存関係を記述できます。 AcpiGenFx は OS に依存しない、ACPI 機械語 (ASL) コードを生成するだけでなくも Windows 固有の要件に注意してください。

アプリには、ACPI テーブルの関連するファイルが生成されます (\*.aslc と\*.asl) これらの説明に基づいて。 ビルド時に、AcpiGenFx 静的に分析プラットフォームの説明 cyclical または未解決の依存関係、デバイスの名前付けと UUID の競合、リソースからコント ローラーへのマッピング、および多くのようなエラーを検出します。 その結果、生成された ASL コードが AcpiGenFx を調べて、最も一般的な誤り、および一意の ACPI 実装の詳細を抽象化するため、デバッグに簡単です。

AcpiGenFx では、本質的に宣言します。 その出力は静的データのみ、および動的ランタイム メソッドを生成するものではありません。 ユース ケースは、SoC をオフの高度な周辺機器の電源管理など、フレームワークでは対応できない場合、メソッドする必要があります Windows プラットフォームの拡張機能ドライバーに実装されてか AcpiGenFx 生成 ASL コードに手動で追加します。

## <a name="before-you-begin"></a>開始する前にしています.

次のファイルを検索、 **AcpiGenFx** WDK インストールのフォルダー。

> [!NOTE]
> AcpiGenFx.dll と関連付けられているサンプルは、WDK の Tools フォルダーでは利用できます。 ツールのディレクトリでは、ターゲット アーキテクチャ フォルダーで、AcpiGenFx フォルダーを移動します。 たとえば、x86 バージョンは C:\Program Files (x86) \Windows Kits\10\Tools\x86\ACPIGenFx があります。

-   AcpiGenFx.dll

    ACPIGenFx を使用する場合に必要です。

-   DSDTSamples

    開始点としてこのプロジェクトを使用すると、プラットフォーム全体の ACPI ファームウェアをデザインできます。 出力は、ACPI テーブルがあります、FADT、MADT などの完全なセットです。

-   SSDTSamples

    開始点としてこのプロジェクトを使用すると、既存のシステムに周辺機器を追加できます。 このサンプルでは、センサー デバイスとそのリソースを記述する方法を示します。 出力は、ASL で ACPI SSDT テーブルです。

Windows 10 のキット、ツール、およびコード サンプルをダウンロードします。

-   [Microsoft Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=533470)
-   [Windows 10 用 Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?LinkId=733614)

## <a name="create-a-platform"></a>プラットフォームを作成します。


1.  Visual Studio で開く新しいC#コンソール プロジェクト。
2.  AutoAcpi.dll アセンブリへの参照を追加します。 で、**プロジェクト** メニューのをクリックして**参照の追加**します。 クリックして**参照**AutoAcpi.dll の場所に移動します。 **[OK]** をクリックします。
3.  **ソリューション エクスプ ローラー**、展開**参照**選択**acpigenfx**します。 オブジェクト ブラウザーのオブジェクトを表示 (**ビュー&gt;オブジェクト ブラウザー**)。
4.  ターゲット .NET Framework 4.5 またはそれ以降。 プロジェクトのプロパティを開きます。 **アプリケーション** ページで確認**ターゲット フレームワーク**に設定されている **.NET Framework 4.5**します。
5.  追加、`Using`ディレクティブをアプリケーションのコードの先頭にある AutoAcpi オブジェクト。
6.  プラットフォームのオブジェクトを作成します。 アーキテクチャに基づき、インスタンス化、**プラットフォーム**オブジェクトを呼び出すことによって**Platform.CreateArmPlatform**または**Platform.Createx86Platform**します。 指定*OEMID*、 *OEMTableID*、*作成者*、*リビジョン*、および*FileName*します。
7.  呼び出す**Platform.WriteAsl**ファイルに書き込めません。

    この例では、プラットフォームのインスタンスを作成する方法を示します。

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

8.  クリックして**開始**アプリをビルドして実行します。 Visual Studio に表示されるビルドの進行状況、**出力**ウィンドウ。 (場合、**出力**ウィンドウが表示されていない、選択**出力**から、**ビュー**メニュー。)。
9.  という名前のフォルダーを開く*プロジェクト*\\bin\\*デバッグまたはリリース*\\出力します。 出力フォルダーには、アプリによって生成されたファイルが含まれています。 SSDT.asl の内容を表示します。

    前の例の出力を次に示します。

    ```console
    DefinitionBlock ("Platform.aml", "DSDT", 5, "MSFT", "EDK2", 1)
    { 
        Scope (\_SB_)
        {
        }

    } 
    ```

アプリには、2 つの追加フォルダーが生成されます。Aslc と Bin です。 Aslc には aslc 形式ですべてのファームウェア テーブルが含まれています。 箱には、バイナリの blob の形式ですべてのファームウェア テーブルが含まれています。

WDK で提供される asl.exe コンパイラを使用して ASL コード ファイルに、ACPI 機械語 (AML) バイナリをコンパイルします。

## <a name="add-devices-and-resources-in-the-dsdt"></a>デバイスとリソースを追加で、します。


プラットフォーム コンポーネントを追加することができます。 通常、これらのコンポーネントには、プロセッサ、バス コント ローラー、電源のリソースおよびなどが含まれます。 DSDTSamples で使用されている一部のコンポーネントを次に示します。

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
<td><strong>Platform.AddACAdapter</strong></td>
<td>AC アダプターを追加します。</td>
</tr>
<tr class="even">
<td><strong>BatteryDevice</strong></td>
<td><p><strong>Platform.AddBatteryDevice</strong></p>
<p><strong>BatteryDevice.ThermalLimit</strong></p></td>
<td>バッテリのデバイスを追加し、その温度の上限を指定します。</td>
</tr>
<tr class="odd">
<td><strong>ButtonArrayDevice</strong></td>
<td><p><strong>Platform.AddButtonArrayDevice</strong></p>
<p><strong>ButtonArrayDevice.AddBackButton</strong></p>
<p><strong>ButtonArrayDevice.AddCameraShutterButton</strong></p>
<p><strong>ButtonArrayDevice.AddCameraAutofocusButton</strong></p>
<p><strong>ButtonArrayDevice.AddGenericButton</strong></p>
<p><strong>ButtonArrayDevice.AddPowerButton</strong></p>
<p><strong>ButtonArrayDevice.AddRotationLockButton</strong></p>
<p><strong>ButtonArrayDevice.AddSearchButton</strong></p>
<p><strong>ButtonArrayDevice.AddVolumeDownButton</strong></p>
<p><strong>ButtonArrayDevice.AddVolumeUpButton</strong></p>
<p><strong>ButtonArrayDevice.AddWindowsHomeButton</strong></p></td>
<td>Windows Home、戻る、+/-、電源、回転ロック、および検索ボリュームなどのボタンを追加します。</td>
</tr>
<tr class="even">
<td><strong>DisplaySensor</strong></td>
<td><strong>Platform.AddDisplaySensor</strong></td>
<td>表示のセンサーを追加します。</td>
</tr>
<tr class="odd">
<td><strong>GenericDevice</strong></td>
<td><strong>Platform.AddGenericDevice</strong></td>
<td>フレームワークで内部的にサポートされているデバイスの任意の型を置き換えに使用できる汎用的なデバイスを追加します。</td>
</tr>
<tr class="even">
<td><strong>GpioController</strong></td>
<td><strong>Platform.AddGpioController</strong></td>
<td>GPIO コント ローラーと割り込み、I/O、およびイベントなどの関連リソースを追加します。</td>
</tr>
<tr class="odd">
<td><strong>HidOverI2C</strong></td>
<td><strong>Platform.AddHidI2CDevice</strong></td>
<td>I²C バスに接続された HID デバイスを追加します。</td>
</tr>
<tr class="even">
<td><strong>I2CController</strong></td>
<td><strong>Platform.AddI2CController</strong></td>
<td>I²C コント ローラーと割り込み、I/O、およびイベントなどの関連リソースを追加します。</td>
</tr>
<tr class="odd">
<td><strong>KDNet2Usb</strong></td>
<td><strong>Platform.AddKDNet2Usb</strong></td>
<td>USB 経由で Kdnet を使用してカーネル デバッグのサポートを追加します。</td>
</tr>
<tr class="even">
<td><strong>PEPDevice</strong></td>
<td><strong>Platform.AddPepDevice</strong></td>
<td>PEP デバイスとそれらのリソースとパッケージと静的な型を返すメソッドを追加します。</td>
</tr>
<tr class="odd">
<td><p><strong>プロセッサ</strong></p>
<p><strong>ProcessorAggregator</strong></p></td>
<td><p><strong>Platform.AddProcessor</strong></p>
<p><strong>Platform.AddProcessorAggregator</strong></p></td>
<td>プロセッサとプロセッサ アグリゲーターを追加します。</td>
</tr>
<tr class="even">
<td><strong>RTCDevice</strong></td>
<td><strong>Platform.AddRTCDevice</strong></td>
<td>ACPI の時間とアラームのデバイスを追加します。</td>
</tr>
<tr class="odd">
<td><strong>SdHostController</strong></td>
<td><strong>Platform.AddSdHostController</strong></td>
<td>SD ホスト コント ローラーを追加します。</td>
</tr>
<tr class="even">
<td><strong>シリアル ポート</strong></td>
<td><strong>Platform.AddSerialPort</strong></td>
<td>シリアルおよび UART デバイスのサポートを追加します。</td>
</tr>
<tr class="odd">
<td><strong>ThermalZone</strong></td>
<td><strong>Platform.AddThermalZone</strong></td>
<td>温度のゾーンと関連付けられているサンプリングのポーリング期間を追加します。</td>
</tr>
<tr class="even">
<td><p><strong>XhciUsbController</strong></p>
<p><strong>EhciUsbController</strong></p>
<p><strong>UsbDevice</strong></p></td>
<td><p><strong>Platform.AddEhciUsbController</strong></p>
<p><strong>Platform.AddXhciUsbController</strong></p>
<p><strong>EhciUsbController.AddUsbDevice</strong></p>
<p><strong>XhciUsbController.AddUsbDevice</strong></p>
<p><strong>UsbDevice.AddUsbDevice</strong></p></td>
<td>USB ホスト コント ローラーと子デバイス (ハブを含む) を追加します。</td>
</tr>
</tbody>
</table>



完全な一覧を表示する開いてで AcpiGenFx**オブジェクト ブラウザー**します。 IntelliSense を使用して、メソッド (およびパラメーター) を判断して、オブジェクトによって公開されるプロパティ。 たとえばクラスを追加し、上記の表に記載されているプロパティを設定する方法を示すコードは、DSDTSamples プロジェクトを参照してください。
## <a name="add-debug-support"></a>デバッグのサポートを追加します。


デバッグ可能としてポートを設定するには、設定、 **DebugEnabled** "true"にオブジェクトのプロパティ。

たとえば、USB デバッグ ポートと xHCI ホスト コント ローラーを説明します。 アプリでは、呼び出す**Platform.AddXhciUsbController**を取得する、 **XhciUsbController**オブジェクトし、設定、 **DebugEnabled**プロパティを"true"にします。 AcpiGenFx アプリの出力に自動的に含まれている Microsoft DBG2 テーブルを生成する\\Aslc フォルダー。

XHCI ホスト コント ローラーを追加してデバッグ可能として宣言する方法の例を示します。

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

上記のスニペットでは、xHCI ホスト コント ローラーは、割り込みのリソースとデバッグのサポートがあります。 PEP デバイスおよび GPIO コント ローラーの依存関係があります。 これらのデバイスの説明については、DSDTSamples を参照してください。

この例に、します。 I²C のコント ローラーを追加する方法を示します。

```cs
I2CController i2c = Platform.AddI2CController("I2C1", "I2CCONTR", 0);
i2c.AddMemory32Fixed(true, 0xf9999000, 0x400, "");
i2c.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Exclusive, 40);
```

XHCI ホストと I²C コント ローラーの前の定義によるコンソール アプリの出力を次に示します。

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

プロジェクトをビルドした後で、プロジェクト ディレクトリに移動します出力\\Aslc します。 Dbg2.aslc ファイルには、次のとおり、DB2 テーブルが含まれています。

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

## <a name="add-an-acpi-description-for-a-peripheral-device-in-the-ssdt"></a>SSDT の周辺機器の ACPI 記述を追加します。


1.  呼び出すことによってプラットフォーム オブジェクトを作成する**Platform.CreateArmPlatform**または**Platform.Createx86Platform**します。
2.  設定、 **SSDT**プロパティを true にします。 これを示します、フレームワークに次の表に、SSDT があります。
3.  デバイスを作成し、リソースを割り当てます。 たとえば、ここでは、サンプルの呼び出しを示すセンサー デバイス**Platform.AddGenericDevice**し、デバイス名、ハードウェア ID、および一意のインスタンスを指定します。 センサー デバイス、あります記載されている、I2C1 I²C シリアル バスに接続します。

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

## <a name="replacing-acpi-firmware-during-development-and-testing"></a>ACPI のファームウェアを開発およびテスト中に置き換える

開発およびテストのシナリオでは、デバイス上の asl.exe コンパイラから生成される AML バイナリを置き換えることができます。 これを行うには、acpitabl.dat を AML バイナリの名前を変更し、%windir% に移動\\system32 します。 ブート時に、Windows は acpitabl.dat と ACPI ファームウェアに存在するテーブルを置き換えます。

**注**テスト署名が有効になっていることを確認します。
**bcdedit で testsigning を設定/**

## <a name="related-topics"></a>関連トピック

[説明の ACPI システム テーブル](acpi-system-description-tables.md)  

---
title: GUID_DEVICE_RESET_INTERFACE_STANDARD の操作
description: GUID_DEVICE_RESET_INTERFACE_STANDARD の操作
keywords:
- GUID_DEVICE_RESET_INTERFACE_STANDARD
ms.date: 11/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61bbadf3bfb675452887a40345984406a2da2882
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835629"
---
# <a name="working-with-the-guid_device_reset_interface_standard"></a>GUID_DEVICE_RESET_INTERFACE_STANDARD の操作

GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスは、正常に機能していないデバイスのリセットと回復を試行するための、関数ドライバーの標準的な方法を定義します。

このインターフェイスでは、次の2種類のデバイスリセットを使用できます。

- 関数レベルのデバイスのリセット。 この場合、リセット操作は特定のデバイスに制限され、他のデバイスからは表示されません。 デバイスはリセット中にバスに接続されたままになり、リセット後の有効な状態 (初期状態) に戻ります。 この種類のリセットは、システムへの影響が最小限になります。 

- この種類のリセットは、バスドライバーまたは ACPI ファームウェアによって実装できます。 バスドライバーでは、要件を満たす帯域内リセット機構がバス仕様によって定義されている場合に、関数レベルのリセットを実装できます。 ACPI ファームウェアでは、必要に応じて、独自の実装でバスドライバーで定義された関数レベルのリセットをオーバーライドできます。

プラットフォームレベルのデバイスのリセット。 この場合、リセット操作によって、バスからデバイスが不足していると報告されます。 リセット操作は、特定のデバイスと、それに接続されている他のすべてのデバイスに、同じ電源レールまたはリセットラインを使用して影響を及ぼします。 この種類のリセットは、システムに最も影響を与えます。 すべてが空の状態から再開されるように、OS は影響を受けるすべてのデバイスのスタックを破棄して再構築します。

Windows 10 以降では、`HKLM\SYSTEM\CurrentControlSet\Control\Pnp` キーの下にあるこれらのレジストリエントリによって、リセット操作が構成されます。 

- DeviceResetRetryInterval: リセット操作が開始されるまでの期間。 既定値は3秒です。 最小値は100ミリ秒です。最大値は30秒です。 

- DeviceResetMaximumRetries: リセット操作が試行された回数。 

> [!NOTE]
>  GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスは、Windows 10 以降で使用できます。
 

## <a name="using-the-device-reset-interface"></a>デバイスリセットインターフェイスの使用

デバイスが正常に機能していないことが関数ドライバーによって検出された場合は、まず関数レベルのリセットを試行します。 関数レベルのリセットによって問題が解決されない場合、ドライバーはプラットフォームレベルのリセットを試行することができます。 ただし、プラットフォームレベルのリセットは、最後のオプションとしてのみ使用する必要があります。

このインターフェイスを照会するために、デバイスドライバーは IRP_MN_QUERY_INTERFACE IRP をドライバースタックに送信します。 この IRP の場合、ドライバーは InterfaceType 入力パラメーターを GUID_DEVICE_RESET_INTERFACE_STANDARD に設定します。 IRP が正常に完了すると、インターフェイスの出力パラメーターは DEVICE_RESET_INTERFACE_STANDARD 構造体へのポインターになります。 この構造体には、DeviceReset ルーチンへのポインターが含まれています。このルーチンを使用して、関数レベルまたはプラットフォームレベルのリセットを要求できます。

## <a name="supporting-the-device-reset-interface-in-function-drivers"></a>関数ドライバーでのデバイスリセットインターフェイスのサポート

デバイスのリセットインターフェイスをサポートするには、デバイススタックが次の要件を満たしている必要があります。

関数ドライバーは、IRP_MN_QUERY_REMOVE_DEVICE、IRP_MN_REMOVE_DEVICE、および IRP_MN_SURPRISE_REMOVAL を正しく処理する必要があります。 

ほとんどの場合、ドライバーは IRP_MN_QUERY_REMOVE_DEVICE を受信すると、デバイスを安全に削除できるように、成功を返します。 ただし、デバイスがメモリバッファーへの書き込みループでスタックしているなど、デバイスを安全に停止できない場合もあります。 このような場合、ドライバーは STATUS_DEVICE_HUNG を IRP_MN_QUERY_REMOVE_DEVICE に返す必要があります。 PnP マネージャーは IRP_MN_QUERY_REMOVE_DEVICE および IRP_MN_REMOVE_DEVICE プロセスを続行しますが、その特定のスタックは IRP_MN_REMOVE_DEVICE を受け取りません。 代わりに、デバイススタックは、デバイスがリセットされた後に IRP_MN_SURPRISE_REMOVAL を受信します。

これらの Irp の詳細については、以下を参照してください。 

[IRP_MN_QUERY_REMOVE_DEVICE 要求の処理](handling-an-irp-mn-query-remove-device-request.md)

[IRP_MN_REMOVE_DEVICE 要求の処理](handling-an-irp-mn-remove-device-request.md)

[IRP_MN_SURPRISE_REMOVAL 要求の処理](handling-an-irp-mn-surprise-removal-request.md)

## <a name="supporting-the-device-reset-interface-in-filter-drivers"></a>フィルタードライバーでのデバイスリセットインターフェイスのサポート

フィルタードライバーは、GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイス型の IRP_MN_QUERY_INTERFACE Irp をインターセプトする場合があります。 そうすることで、GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスへの委任を続行できますが、リセット操作の前または後にデバイス固有の操作を実行できます。 または、バスドライバーによって返された GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスを独自のインターフェイスでオーバーライドして、独自のリセット操作を提供することもできます。

## <a name="supporting-the-device-reset-interface-in-bus-drivers"></a>バスドライバーでのデバイスリセットインターフェイスのサポート

デバイスのリセットプロセスに参加するバスドライバー (つまり、リセット要求に応答しているデバイスに関連付けられているリセットおよびバスドライバーを要求しているデバイスに関連付けられているバスドライバー) は、次のいずれかを満たしている必要があります。必要性

- ホットプラグ対応。 バスドライバーは、バスから削除されるデバイスと、バスに接続されているデバイスを検出できなければなりません。

- または、GUID_REENUMERATE_SELF_INTERFACE_STANDARD インターフェイスを実装する必要があります。 これは、バスからプルされ、接続されているデバイスをシミュレートします。 組み込みのバスドライバー (PCI や SDBUS など) は、このインターフェイスをサポートしています。 そのため、リセットするデバイスでこれらのバスのいずれかを使用している場合は、バスドライバーを変更する必要はありません。

WDF ベースのバスドライバーでは、WDF フレームワークによって、ドライバーの代わりに GUID_REENUMERATE_SELF_INTERFACE_STANDARD インターフェイスが登録されます。 そのため、これらのドライバーには、このインターフェイスの登録は必要ありません。 バスドライバーが、子デバイスを再列挙する前に何らかの操作を実行する必要がある場合は、EvtChildListDeviceReenumerated コールバックルーチンに登録し、そのルーチンで操作を実行する必要があります。 このコールバックルーチンはすべての PDO に対して並列で呼び出される可能性があるため、ルーチン内のコードは競合状態から保護する必要がある場合があります。

## <a name="acpi-firmware-function-level-reset"></a>ACPI ファームウェア: 関数レベルのリセット

関数レベルのデバイスのリセットをサポートするには、デバイススコープ内で定義された RST メソッドが必要です。 このメソッドが存在する場合、このメソッドは、そのデバイスに対する関数レベルのデバイスリセット (存在する場合) のバスドライバーの実装をオーバーライドします。 実行時に、RST メソッドはそのデバイスのみをリセットする必要があり、他のデバイスには影響を与えません。 また、デバイスはバス上で接続された状態を維持する必要があります。

## <a name="acpi-firmware-platform-level-reset"></a>ACPI ファームウェア: プラットフォームレベルのリセット

プラットフォームレベルのデバイスのリセットをサポートするには、次の2つのオプションがあります。

- ACPI ファームウェアは、RST メソッドを実装する PowerResource を定義できます。このリセット方法の影響を受けるすべてのデバイスは、デバイススコープで定義された PRR オブジェクトを使用して、この PowerResource を参照できます。

- デバイスでは、オブジェクトを宣言できます。 この場合、ACPI ドライバーでは D3cold 電源サイクルを使用してリセットを実行し、デバイス間の依存関係をリセットすると、デバイス間の依存関係が決定されます。

デバイススコープに PRR オブジェクトが存在する場合、ACPI ドライバーは参照された PowerResource の RST メソッドを使用してリセットを実行します。 [PRR] オブジェクトが定義されていないにもかかわらず、"PR3" オブジェクトが定義されている場合、ACPI ドライバーは D3cold 電源サイクルを使用してリセットを実行します。 オブジェクトが定義されていない場合、デバイスはプラットフォームレベルのリセットをサポートしていません。また、ACPI ドライバーは、プラットフォームレベルのリセットが使用できないことを報告します。

### <a name="verifying-acpi-firmware-on-the-test-system"></a>テストシステムで ACPI ファームウェアを検証しています
デバイスのリセットと回復をサポートするドライバーをテストするには、次の手順に従います。 この手順では、この例の ASL ファイルを使用していることを前提としています。 

 ```asl
DefinitionBlock("SSDT.AML", "SSDT", 0x01, "XyzOEM", "TestTabl", 0x00001000)
{
    Scope(\_SB_)
       {
        PowerResource(PWFR, 0x5, 0x0)
        {
            Method(_RST, 0x0, NotSerialized)    { }
            
            // Placeholder methods as power resources need _ON, _OFF, _STA.
            Method(_STA, 0x0, NotSerialized)
            {
                Return(0xF)
            }

            Method(_ON_, 0x0, NotSerialized)    { }

            Method(_OFF, 0x0, NotSerialized)    { }

        } // PowerResource()
    } // Scope (\_SB_)

    // Assumes WiFi device is declared under \_SB.XYZ.
    Scope(\_SB_.XYZ.WIFI)
        {

        // Declare PWFR as WiFi reset power rail
        Name(_PRR, Package(One)
            {
                \_SB_.PWFR
            })
        } // Scope (\_SB)
}
```
 


1. Asl などの ASL コンパイラを使用して、テスト ASL ファイルを AML にコンパイルします。 Windows Driver Kit (WDK) に含まれているの実行可能ファイル。 

```console
Asl <test>.asl
```

上記のコマンドは、SSDT を生成します。

2. SSDT の名前を acpitabl に変更します。 

3. テストシステムで acpitabl を保存します。 

4. テストシステムでテスト署名を有効にします。 

```console
bcdedit /set GUID_DEVICE_RESET_INTERFACE_STANDARD testsigning on
```

5. テストシステムを再起動します。 

6. テーブルが読み込まれていることを確認します。 Windows デバッガーでは、次のコマンドを使用します。 

- !acpicache 
- SSDT テーブルの dt ヘッダーアドレス (_l) 

```dbgcmd
0: kd> !acpicache
Dumping cached ACPI tables...
  SSDT @(ffffffffffd03018) Rev: 0x1 Len: 0x000043 TableID: TestTabl
  XSDT @(ffffffffffd05018) Rev: 0x1 Len: 0x000114 TableID: HSW-FFRD
       ...
       ...
 
0: kd> dt _DESCRIPTION_HEADER ffffffffffd03018
ACPI!_DESCRIPTION_HEADER
   +0x000 Signature        : 0x54445353
   +0x004 Length           : 0x43
   +0x008 Revision         : 0x1 ''
   +0x009 Checksum         : 0x37 '7'
   +0x00a OEMID            : [6]  "XyzOEM"
   +0x010 OEMTableID       : [8]  "TestTabl"
   +0x018 OEMRevision      : 0x1000
   +0x01c CreatorID        : [4]  "MSFT"
   +0x020 CreatorRev       : 0x5000000
```

## <a name="see-also"></a>参照

[デバイス標準 (_C)](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_reset_interface_standard) 


---
title: デバイスのリセットと回復
description: GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスは、関数のドライバーをリセットし、正しく機能しないデバイスを回復しようとする標準的な方法を定義します。
ms.assetid: 507192FF-77BB-4446-AAA0-3F44E1CB2E72
keywords:
- GUID_DEVICE_RESET_INTERFACE_STANDARD
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b15d9fdbc5c1690d62bc2cd461a1959fda064aec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324550"
---
# <a name="resetting-and-recovering-a-device"></a>デバイスのリセットと回復

GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスは、関数のドライバーをリセットし、正しく機能しないデバイスを回復しようとする標準的な方法を定義します。

2 種類のデバイスのリセットは、このインターフェイスを介して利用します。

-    関数レベルのデバイスのリセット。 ここでは、リセット操作では、特定のデバイスには制限され、他のデバイスには表示されません。 デバイスは、全体にわたってリセット バスに接続されたまま、リセット後に有効な状態 (初期の状態) を返します。 この種類のリセットは、システムの最小の影響を及ぼします。 

        この種類のリセットは、バス ドライバーまたはファームウェアの ACPI のいずれかに実装できます。 バス ドライバーには、関数レベル バス仕様には、要件を満たす帯域内リセット メカニズムが定義されている場合のリセットを実装できます。 ACPI のファームウェアは、バス ドライバーの定義済み関数レベルの独自の実装でリセットを必要に応じて上書きできます。

-    プラットフォーム レベルのデバイスのリセット。 この場合、リセット操作には、バスから不足するいると報告されることをデバイスが原因です。 リセット操作では、特定のデバイスと同じ power レールを使用して接続されているか、行をリセットするその他のすべてのデバイスに影響します。 この種類のリセットでは、システムで最も影響を及ぼします。 OS では、破棄し、空の状態から再開されるすべてのものを確実に影響を受けるすべてのデバイスのスタックを再構築します。

        Windows 10 以降、HKLM\SYSTEM\CurrentControlSet\Control\Pnp キーの下でこれらのレジストリ エントリは、リセット操作を構成します。 

        -    DeviceResetRetryInterval:期間をリセットする前に操作を開始します。 既定値は、3 秒です。 最小値は 100 ミリ秒です。最大値は 30 秒です。 
        -    DeviceResetMaximumRetries:リセット操作が試行された回数。 

注、GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスでは、Windows 10 以降使用できます。
 

## <a name="using-the-device-reset-interface"></a>インターフェイスをリセットするデバイスを使用します。

関数ドライバー検出した場合、デバイスが正しく機能していない、関数レベルのリセットを最初にしようとする必要があります。 関数レベルのリセットで問題が解決しない場合、ドライバーは、プラットフォーム レベルのリセットを試みる選択可能性があります。 ただし、プラットフォーム レベルのリセットは、最後のオプションとしてのみ使用する必要があります。

このインターフェイスを照会するには、デバイス ドライバーはドライバー スタック ダウン IRP_MN_QUERY_INTERFACE IRP を送信します。 この IRP では、ドライバーは GUID_DEVICE_RESET_INTERFACE_STANDARD に InterfaceType 入力パラメーターを設定します。 IRP の正常終了時に、インターフェイスの出力パラメーターは、DEVICE_RESET_INTERFACE_STANDARD 構造体へのポインターです。 この構造体には、関数レベルまたはプラットフォーム レベルのリセットを依頼するために使用できる DeviceReset ルーチンへのポインターが含まれています。


## <a name="supporting-the-device-reset-interface-in-function-drivers"></a>関数のドライバー インターフェイスをリセットするデバイスをサポートしています。

デバイスのリセットのインターフェイスをサポートするには、デバイス スタックは、次の要件を満たす必要があります。

関数のドライバーでは、IRP_MN_QUERY_REMOVE_DEVICE、IRP_MN_REMOVE_DEVICE および IRP_MN_SURPRISE_REMOVAL を正しく処理する必要があります。 

ほとんどの場合、ドライバーは、IRP_MN_QUERY_REMOVE_DEVICE を受信するとが返されます成功、デバイスを安全に削除できるようにします。 ただし、場所、デバイス安全に停止できませんなど、デバイスは、メモリ バッファーに書き込むループでスタックしている場合、ケースがあります。 このような場合、ドライバーは IRP_MN_QUERY_REMOVE_DEVICE に STATUS_DEVICE_HUNG を返す必要があります。 PnP マネージャーは、IRP_MN_QUERY_REMOVE_DEVICE と IRP_MN_REMOVE_DEVICE プロセスを続行しますが、その特定のスタックは IRP_MN_REMOVE_DEVICE を受信しません。 代わりに、デバイス スタックであっても、デバイスがリセットされた後、IRP_MN_SURPRISE_REMOVAL が表示されます。

これらの Irp の詳細についてを参照してください。 

[IRP_MN_QUERY_REMOVE_DEVICE 要求の処理](handling-an-irp-mn-query-remove-device-request.md)

[IRP_MN_REMOVE_DEVICE 要求の処理](handling-an-irp-mn-remove-device-request.md)

[IRP_MN_SURPRISE_REMOVAL 要求の処理](handling-an-irp-mn-surprise-removal-request.md)

## <a name="supporting-the-device-reset-interface-in-filter-drivers"></a>フィルター ドライバーのインターフェイスをリセットするデバイスをサポートしています。

フィルター ドライバーは、GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスの型を持つ IRP_MN_QUERY_INTERFACE Irp をインターセプト可能性があります。 これにより、GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスにデリゲートしますが、リセット操作の前後にデバイスに固有の操作は実行を継続できます。 または、独自のリセット操作を提供するために、独自のインターフェイスを持つバス ドライバーによって返される GUID_DEVICE_RESET_INTERFACE_STANDARD インターフェイスをオーバーライドできます。

## <a name="supporting-the-device-reset-interface-in-bus-drivers"></a>バス ドライバーのインターフェイスをリセットするデバイスをサポートしています。

デバイスのリセット プロセス (つまり、リセットを要求しているデバイスに関連付けられたバス ドライバー) と、リセット要求に応答しているデバイスに関連付けられているバス ドライバーに参加するバス ドライバーは、次のいずれかを満たす必要があります。要件:

-    ホット プラグができます。 バス ドライバーは、予告なしバスから削除されているデバイスと、バスに接続されているデバイスを検出できる必要があります。

-    または、GUID_REENUMERATE_SELF_INTERFACE_STANDARD インターフェイスを実装にする必要があります。 これは、バスに接続されているから取得されるデバイスをシミュレートします。 組み込みのバス ドライバー (PCI SDBUS など) は、このインターフェイスをサポートします。 そのため、リセットされているデバイスには、これらのバスの 1 つが使用されている場合は、バス ドライバーの変更する必要があるためはありません。

        WDF ベース バス ドライバーについては、WDF フレームワークは、ドライバーに代わって GUID_REENUMERATE_SELF_INTERFACE_STANDARD インターフェイスを登録します。 そのため、このインターフェイスを登録するはそれらのドライバーに必要ではありません。 をバス ドライバーがその子デバイスが再列挙される前にいくつかの操作を実行する必要がある場合は EvtChildListDeviceReenumerated コールバック ルーチンを登録する必要があり、ルーチンで操作を実行します。 このコールバック ルーチンが呼び出されるため、並列ですべて pdo のルーチンで、コードは、競合状態から保護する必要があります。

## <a name="acpi-firmware-function-level-reset"></a>ACPI ファームウェア:関数レベルのリセット

関数レベルのデバイスをサポートするためには、リセット、_RST メソッドは、デバイスのスコープ内で定義されている必要があります。 存在する場合、このメソッドは関数レベルのデバイス (ある場合) をそのデバイスのリセットのバス ドライバーの実装をオーバーライドします。 実行すると、_RST メソッドはそのデバイスのみをリセットする必要があり、その他のデバイスには影響する必要があります。 さらに、デバイスは、バスに接続されている維持する必要があります。

## <a name="acpi-firmware-platform-level-reset"></a>ACPI ファームウェア:プラットフォーム レベルのリセット
プラットフォーム レベルのデバイスをサポートするために次のようにリセットします。 は、2 つのオプションがあります。

-    ACPI のファームウェアが、_RST メソッドを実装する PowerResource を定義し、このリセット方法が影響を受けるすべてのデバイスは、デバイスのスコープで定義されている _PRR オブジェクトを通じてこの PowerResource を参照してください。

-    デバイスは、_PR3 オブジェクトを宣言できます。 ここでは、ACPI ドライバーが D3cold の電源を入れ、リセットの実行を使用し、デバイス間の依存関係のリセットは _PR3 オブジェクトから決定されます。

_PRR オブジェクトが、デバイスのスコープ内に存在する場合、ACPI ドライバーは _RST メソッドをリセットを実行する参照先の PowerResource で使用します。 _PRR オブジェクトが定義されていない _PR3 オブジェクトが定義されている場合は、ACPI ドライバーは D3cold の電源を入れ、リセットの実行を使用します。 _PRR も _PR3 オブジェクトを定義し、デバイスがプラットフォーム レベルのリセットをサポートしていない ACPI ドライバーを報告する場合は、プラットフォーム レベルのリセットは使用できません。

## <a name="verifying-acpi-firmware-on-the-test-system"></a>テスト システムで ACPI ファームウェアを検証します。
デバイスのリセットと回復をサポートするドライバーをテストして、次の手順を実行します。 この手順では、このサンプルの ASL ファイルを使用している前提としています。 

```cpp
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
 


1. Asl.exe などの ASL コンパイラを使用して、AML テスト ASL ファイルをコンパイルします。 実行可能ファイルには、Windows Driver Kit (WDK) で含まれています。 Asl <test>.asl

    上記のコマンドは、SSDT.aml を生成します。

2. Acpitabl.dat SSDT.aml に変更します。 
3. テスト システムで %systemroot%\system32 acpitabl.dat にコピーします。 
4. テストのテスト システムの署名を有効にします。 
      Bcdedit で GUID_DEVICE_RESET_INTERFACE_STANDARD testsigning を設定/

5. テスト システムを再起動します。 
6. テーブルが読み込まれていることを確認します。 Windows デバッガーでは、これらのコマンドを使用します。 

```cpp
!acpicache 
dt _DESCRIPTION_HEADER address of the SSDT table 

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

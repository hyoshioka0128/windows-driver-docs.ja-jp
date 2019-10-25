---
title: MB デバイスベースのリセットと回復
description: MB デバイスベースのリセットと回復
ms.assetid: CA75B63B-53EE-41BF-B2B6-E008F5598399
keywords:
- MB デバイスベースのリセットと回復、モバイルブロードバンドデバイスベースのリセットと回復、モバイルブロードバンドミニポートドライバーのデバイスベースのリセットと回復
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4259888ce0c23525b0ef6147c88cd5e7691611d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844297"
---
# <a name="mb-device-based-reset-and-recovery"></a>MB デバイスベースのリセットと回復

モバイルブロードバンド (MB または MBB) デバイスベースのリセットと回復は、Windows 10 バージョン1809以降のテクノロジであり、デバイスとドライバーを MBB するための堅牢なリセット回復メカニズムが導入されています。 このメカニズムにより、MBB デバイスは、誤動作、接続の切断、操作コマンドへの無応答などの障害を防ぐことができます。最終的に、エラーが発生した場合にユーザーがシームレスに動作し、system. 

デバイスベースのリセットと回復は、ファームウェアの依存関係の有無にかかわらず実装できます。 IHV または OEM パートナーは、サポートされているデバイスまたはファームウェアレベルのリセットメカニズムを使用して、すべての Windows Pc で利用可能なソフトウェアベースのリセットメカニズムを拡張し、回復の成功率を高めることができます。

## <a name="mb-device-based-reset-and-recovery-architecture-overview"></a>MB デバイスベースのリセットと復旧のアーキテクチャの概要

Windows MBB サービスは、USB トランスポート上に構築された標準の[Mobile ブロードバンドインターフェイスモデル](https://www.usb.org/developers/docs/devclass_docs/MBIM10Errata1_073013.zip "MBIM 仕様")(mbim) インターフェイスを使用して、携帯ネットワークデバイスを初期化して制御します。このインターフェイスは、ncm 仕様を拡張したものです。 IHV デバイスに送信された各コマンドは、受信トレイ Windows MBB クラスドライバーを使用して MBIM コマンドとして送信されます。 通信モデムを MBIM プロトコル交換を使用して初期化すると、ホスト、モデム、およびネットワークの間でデータパスを開始できます。 携帯ネットワークデバイスに送信されるその他のコントロールは、MBIM プロトコル交換を使用して並列で続行されます。 

MBIM 制御パスとデータパスの両方で発生する可能性があるエラーは多数あります。 Windows 10 バージョン1809より前のバージョンの Windows では、単純なエラー処理メカニズムが組み込まれています。 MBIM コマンドが送信され、デバイスが応答しなくなった場合は、MBIM reset コマンドを送信することによって、このメカニズムによってデバイスのリセットが試行されます。 ただし、エラーは、最初に応答していない MBIM インターフェイスが原因で発生することが多いため、このリセットは必ずしも機能しません。 さらに、このメカニズムでは、データパスの障害による接続の切断など、発生する可能性がある他のエラーに対処しません。 

MB デバイスベースのリセットと回復では、大量のエラーを検出し、段階的にインパクトリセットのセットを使用して復旧を調整するための一元化されたフレームワークが導入されています。 デバイスでデバイスレベルのリセットがサポートされている場合、すべてのソフトウェアベースのリセットが終了した後、デバイスベースのリセットと回復によってデバイスレベルのリセットが組み込まれます。 リセットと復旧フレームワークは、MBIM コマンドの応答性に基づいて既存のリセットメカニズムを再定義し、置き換えます。  

MB デバイスベースのリセットと回復では、次の種類のエラーを検出して解決しようとします。

| 障害の領域        | エラーの説明                                         |
|------------------------|-------------------------------------------------------------|
| 制御パス           | <ul><li>MBIM プロトコルパスでハング状態が検出されました。 ハング検出の詳細については、「 [MB ハング検出](mb-hang-detection.md)」を参照してください。</li><li>MBB reponding が原因でエラーが発生し、状態や情報が正しくない。</li></ul> |
| データパス              | <ul><li>デバイス側の障害により、データパスの障害が発生しています。 たとえば、エンドポイントがデータトラフィックに reponding されたり、PHY からデータが破損したりする場合などです。</li><li>モデム/ネットワーク側の障害。 たとえば、ネットワークが IP トラフィック、DNS エラー、パケット損失などを repsonding していないとします。</li></ul> |

一部の障害は、回復の観点からは実行できませんが、次のような場合もあります。

- COSA 設定の欠如や、MO によって開始されたサービス拒否などの、プロビジョニングまたはアクティブ化に関連する問題
- ドライバーの初期化エラー (電源またはハードウェアに関連する) またはソフトウェアのバグによるパスの問題の制御

ただし、実行可能なエラーが検出されると、デバイスベースのリセットと回復は、次のリセットメカニズムを試行します。 リセットオプションは、Windows が実行する順序 (少なくともインパクト) に一覧表示されます。 

次の表に示すソフトウェアベースのリセットオプションは、すべての Windows 10 バージョン 1809 MBB デバイスで使用でき、OEM patners によって無効にしたり、構成したりすることができます。

| シーケンスのリセット | 種類のリセット    | リセットメカニズム |
| ---------------|-------------- | --------------- |
| 1              | ソフトウェアのみ | PDP コンテキストを非アクティブ化してアクティブ化する |
| 2              | ソフトウェアのみ | 航空機モード (APM) のオン/オフの切り替え |
| 3              | ソフトウェアのみ  | デバイスをプラグアンドプレイ (PnP) レベルで有効/無効にする |

Oem は、デバイスとファームウェアの MBB 機能を使用して、次のデバイスベースのリセットオプションを有効にします。 

| シーケンスのリセット | 種類のリセット   | リセットメカニズム |
| -------------- |------------- | --------------- |
| ホーム フォルダーが置かれているコンピューターにアクセスできない              | デバイスベース | 機能レベルデバイスのリセット (FLDR) |
| 5              | デバイスベース | プラットフォームレベルのデバイスリセット (PLDR) |

復旧の順序は変更されますが、特定の種類の障害に対して特定のリセットメカニズムが完全にバイパスされる場合もあります。 たとえば、航空機モードの切り替え中にコマンドタイムアウトが発生した場合、OS では、航空機モードを修正するように切り替えられません。 MBB デバイスが MBIM コマンドに応答しない場合、OS はデバイスベースのリセットメカニズムに直接関与します。

MBIM 関数を有効にする UDE クライアントドライバーでは、Windows 10 バージョン1809に新しい API が含まれています。この API を使用すると、UDECx クライアントドライバーがエラーを検出したときにリセットを要求できます。 次のセクションでは、これらの新しいデバイスベースのリセット mechanims について説明します。これには、PCI の FLDR、PLDR、UDECx reset が含まれます。

## <a name="device-based-resets"></a>デバイスベースのリセット

### <a name="function-level-device-reset-fldr"></a>関数レベルのデバイスのリセット (FLDR)

関数レベルのデバイスリセットは、システムへの影響の観点から、デバイスベースの最も軽いリセットです。 デバイス内部で発生し、他のデバイスからは認識されず、デバイスはリセット中にバスに接続されたままになり、プロセスの後に有効な状態 (つまり初期状態) に戻ります。 これは、バスドライバーまたはファームウェアによって提供されます。 バスドライバーは、要件を満たす帯域内リセットメカニズムをバス仕様で定義している場合に、FLDR ハンドラーを実装します。 ファームウェアライターは、FLDR の要件に従っている場合でも、ラインのリセットや電源の切り替えなど、帯域外の信号を使用する独自の FLDR 実装でバス定義の FLDR をオーバーライドする可能性があります。 

### <a name="platform-level-device-reset-pldr"></a>プラットフォームレベルのデバイスリセット (PLDR)  

プラットフォームレベルのデバイスリセットは、FLDR を使用できない場合や、FLDR に対する最終手段として使用される場合に使用します。 このリセットメカニズムを使用すると、デバイスがバスから (たとえば電源サイクル中に) 見つからないと報告されるか、複数のデバイスに影響を与えることになります。 Reset メソッドは、ACPI テーブルで指定されています。これは、専用のリセットラインの切り替え、または D3 電源リソースの電源を切り替えるとして実装される場合があります。 PLDR を実行すると、OS は、すべての影響を受けるデバイスのスタックを破棄して再構築し、すべてが不自然状態から開始されるようにします。

### <a name="reset-recovery-for-ude-devices"></a>UDE デバイスの回復をリセットする 

MBIM 関数を有効にする UDE クライアントドライバーの場合、Windows 10 バージョン1809には、UDECx クライアントドライバーでエラーが検出されたときにリセットを要求するために使用できる API が含まれています。 クライアントドライバーは、新しいメソッド[**UdecxWdfDeviceNeedsReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)を呼び出してリセットを要求します。このメソッドは、UDECx がデバイスに対して試行するリセットの種類を指定します (サポートされている場合)。 これらのリセット型は**PlatformLevelDeviceReset**と**FunctionLevelDeviceReset**で、 [**UDECX_WDF_DEVICE_RESET_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)列挙体の値です。 リセットが開始されると、UDECx はドライバーの[*EVT_UDECX_WDF_DEVICE_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset) callback 関数を呼び出し、このプロセス中に他のコールバックが呼び出されないようにします。 クライアントドライバーは、リソースの解放などのリセット関連の操作を実行し、 [**UdecxWdfDeviceResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)を呼び出すことによってシグナルリセットが完了したことを前提としています。

次のフロー図は、UDE デバイスのリセットプロセスを示しています。

![UDECx クライアントドライバーの復旧フローをリセットするためのフロー](images/mb-self-healing-udecx-reset.png "UDECx クライアントドライバーのリセット回復の呼び出しフロー。")


## <a name="requirements-for-mb-device-based-reset-and-recovery"></a>デバイスベースのリセットと回復のための要件 (MB)

### <a name="requirements-for-fldr"></a>FLDR の要件

デバイスで FLDR をサポートするには、デバイス () スコープ内で、`_RST` メソッドが定義されている必要があります。 このメソッドを実行すると、そのデバイスのみをリセットする必要があり、別のデバイスには触れることができません。 また、デバイスはバスに接続された状態で維持する必要があります。 

```cpp
Device(PCI0)  
{  
Device(USB0)  
{  
    Name(_ADR, 0x1d0000)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Method(_RST, 0x0, NotSerialized)  
    {  
            //  
            // Perform reset of the USB0 device  
            //  
    } 
} 
} 
```

### <a name="requirements-for-pldr"></a>PLDR の要件

PLDR では、他のデバイスのリセットによって影響を受けるデバイスは、リセット用に `PowerResource` を共有するように表されます。 デバイスは、リセットのために `PowerResource` に対する依存関係を宣言し、`PowerResource` `_RST` メソッドを実装します。 

```cpp
Device(PCI0)  
{  
PowerResource(URST, 0x5, 0x0)  
{  
    //  
    // Dummy _ON and _OFF methods. All power resources must have these  
    // two defined.  
    // Method(_ON, 0x0, NotSerialized)  
    {  
    }  
    Method(_OFF, 0x0, NotSerialized)  
    {  
    }  
    Method(_RST, 0x0, NotSerialized)  
    {  
            //  
            // Perform reset of the USB0 and USB1 devices  
            //  
    } 
}  
Device(USB0)  
{  
    Name(_ADR, 0x1d0000)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Name(_PRR, Package(0x1) { ^URST })  
}  
Device(USB1)  
{  
    Name(_ADR, 0x1d0001)  
    Name(_S4D, 0x2)  
    Name(_S3D, 0x2)  
    …  
    Name(_PRR, Package(0x1) { ^URST })  
} 
} 
```

または、デバイスを D3Cold の電源状態にし、D0 に戻すことで PLDR を実現し、基本的にデバイスの電源をオンにすることができます。 この場合、デバイススコープで `_PR3` を宣言するだけで PLDR をサポートできます。 デバイススコープで `_PRR` が参照されていない場合、ACPI は `_PR3` を使用してデバイス間の依存関係をリセットします。 詳細については、「[デバイスのリセットと回復](../kernel/resetting-and-recovering-a-device.md)」を参照してください。 

## <a name="related-links"></a>関連リンク

[MB ハング検出](mb-hang-detection.md)

[**UDECX_WDF_DEVICE_RESET_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)

[**UdecxWdfDeviceNeedsReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

[*EVT_UDECX_WDF_DEVICE_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)

[**UdecxWdfDeviceResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)

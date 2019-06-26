---
title: MB デバイスベースのリセットと回復
description: MB デバイスベースのリセットと回復
ms.assetid: CA75B63B-53EE-41BF-B2B6-E008F5598399
keywords:
- MB デバイス ベースのリセットと回復、モバイル ブロード バンド デバイス ベースのリセットと回復、モバイル ブロード バンド ミニポート ドライバー デバイス ベースのリセット、および回復
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: fbe6c439d90d6aa13192eb60a3d38cf3a78291c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360273"
---
# <a name="mb-device-based-reset-and-recovery"></a>MB デバイスベースのリセットと回復

デバイス ベースのモバイル ブロード バンド (MB または MBB) のリセットと復旧は、Windows 10、MBB デバイスとドライバーの堅牢なリセット復旧メカニズムを導入するバージョン 1809 以降でのテクノロジです。 このメカニズムでは、MBB デバイス障害、接続、または、最終的に使用できるようにしてシームレスなエラーが発生した場合、再起動する必要がある可能性が低くなりますの運用上のコマンドに無応答の損失が発生するエラーを回避するために、システム。 

ファームウェアの依存関係の有無は、デバイス ベースのリセットと復旧を実装できます。 IHV および OEM のパートナーがサポートされているデバイスですべての Windows Pc で使用可能なソフトウェア ベースのリセットのメカニズムを拡張できます。 またはファームウェア レベルが正常に復元の速度を向上させるメカニズムにリセットします。

## <a name="mb-device-based-reset-and-recovery-architecture-overview"></a>MB デバイス ベースのリセットと復旧のアーキテクチャの概要

Windows MBB サービスを初期化し、標準を使用して携帯電話のデバイスを制御[モバイル ブロード バンド インターフェイス モデル](https://www.usb.org/developers/docs/devclass_docs/MBIM10Errata1_073013.zip "MBIM 仕様")USB トランスポート拡張上に構築された (MBIM) インターフェイスNCM の仕様。 IHV デバイスに送信される各コマンドは、受信トレイ Windows MBB クラス ドライバーを経由して、MBIM コマンドとして送信されます。 MBIM プロトコルの交換を使用して携帯電話のモデムが初期化されると、ホスト、モデム、およびネットワークの間でデータのパスを開始できます。 携帯電話のデバイスに送信されるすべての他のコントロールは、並列で MBIM プロトコル exchange を使用して続行します。 

MBIM コントロールのパスと、データ パスの両方で発生するエラーを数多くあります。 バージョンの Windows 10、バージョンは 1809 より前に、の Windows、単純なエラー処理メカニズムが組み込まれています。 MBIM コマンドが送信され、デバイスが応答しなくなったをされるたびに、メカニズム、MBIM リセット コマンドを送信することによって、デバイスをリセットしようとします。 ただし、障害が多いため、応答していない MBIM インターフェイスにより、最初に、このリセットが機能しません。 さらに、データ パスの障害による接続の喪失などが発生するその他の失敗、メカニズムは取り扱いません。 

MB デバイス ベースのリセットと復旧には、リセットの段階的にインパクトのある一連の座標の障害復旧の大規模なセットを検出するために一元的なフレームワークが導入されています。 デバイスは、デバイス レベルのリセットをサポートする場合は、MB デバイス ベースのリセットと回復とすべてのソフトウェア ベースのリセットが使い果たされるデバイス レベルのリセットが組み込まれます。 リセットと回復のフレームワークを再定義し、置き換える既存 MBIM コマンドの応答性に基づくメカニズムをリセットします。  

MB デバイス ベースのリセットと回復を検出し、次の種類の障害を解決しようとしています。

| 障害の領域        | エラーの説明                                         |
|------------------------|-------------------------------------------------------------|
| コントロールのパス           | <ul><li>MBIM プロトコル パス上で検出されたハング条件です。 ハング検出の詳細については、次を参照してください。 [MB ハング検出](mb-hang-detection.md)します。</li><li>無効な状態および情報に MBB reponding によるエラー。</li></ul> |
| データ パス              | <ul><li>デバイス側のデータ パスの障害の結果に失敗しました。 例では、エンドポイントのデータ トラフィックに reponding いない PHY などからデータを破損しています。</li><li>モデム/ネットワーク側に失敗しました。 たとえば、ネットワークの IP トラフィックに、DNS エラー、パケット損失、repsonding しないなどです。</li></ul> |

いくつかのエラーは、これらに限定されませんが、回復の観点からは実用的ではないです。

- COSA 設定または MO によるサービス拒否が不足しているなどのプロビジョニングまたはアクティブ化に関連の問題
- ドライバーの初期化エラー (電源またはハードウェアに関連) またはソフトウェアのバグのためコントロール パスの問題

ただしで実用的なエラーが検出されると、MB デバイス ベースのリセットと復旧は試行、次のリセット メカニズム。 リセット オプションは、Windows は、最低限の実行の順序で並んでいるほとんど影響力の強いにします。 

次の表に、ソフトウェア ベースのリセットのオプションはすべての Windows 10、バージョンは 1809 MBB デバイスで使用可能なと、無効になっているまたは OEM patners によって構成ができます。

| シーケンスをリセットします。 | 種類をリセットします。    | メカニズムをリセットします。 |
| ---------------|-------------- | --------------- |
| 1              | ソフトウェアのみ | 非アクティブ化し、PDP コンテキストをアクティブ化 |
| 2              | ソフトウェアのみ | 切り替え機内モード (APM) オン/オフ |
| 3              | ソフトウェアのみ  | プラグ アンド プレイ (PnP) レベルでデバイスを有効/無効にします。 |

次のデバイス ベースのリセット オプションは Oem によって MBB/デバイスのファームウェアの機能を有効になっています。 

| シーケンスをリセットします。 | 種類をリセットします。   | メカニズムをリセットします。 |
| -------------- |------------- | --------------- |
| 4              | デバイス ベース | 機能レベルのデバイスのリセット (FLDR) |
| 5              | デバイス ベース | プラットフォーム レベルのデバイスのリセット (PLDR) |

復旧の順序を変更すると、および場合によっては特定のリセットのメカニズムをバイパス、特定の種類の障害。 たとえば、機内モードの切り替え中にコマンドのタイムアウトが発生した場合、OS 切り替えることはできません修正機内モード。 MBB デバイス、MBIM コマンドに応答しない場合、OS がはまってデバイス ベースのリセット メカニズム直接。

Windows 10、MBIM 関数を有効にする UDE クライアント ドライバーにはバージョンには 1809 UDECx クライアント ドライバーにエラーが検出されるたびにリセットを要求するために使用できる新しい API が含まれます。 次のセクションでは、FLDR、PLDR、pci リセット UDECx などこれら新しいデバイス ベースのリセット機構について説明します。

## <a name="device-based-resets"></a>デバイス ベースのリセット

### <a name="function-level-device-reset-fldr"></a>関数レベルのデバイスのリセット (FLDR)

システムへの影響の観点から最も明るいデバイス ベースのリセットは、関数レベルのデバイスをリセットします。 デバイス内で発生し、その他のデバイスには表示されませんし、デバイス全体にわたってリセット バスに接続されたままし、プロセスの後に有効な状態 (つまり、初期状態) を返します。 これは、バス ドライバーまたはファームウェアに提供できます。 バスの仕様には、要件に合ったインバンド リセット メカニズムが定義されている場合、バス ドライバーは、FLDR ハンドラーを実装します。 ファームウェアのライターの FLDR リセット線や FLDR の要件をまだ実行中に、電源の切り替えなどの帯域外の信号を使用する独自の実装で bus によって定義された FLDR 方が優先されます。 

### <a name="platform-level-device-reset-pldr"></a>プラットフォーム レベルのデバイスのリセット (PLDR)  

FLDR を使用できない場合に、または補足 FLDR 最後の手段としては、プラットフォーム レベルのデバイスをリセットします。 これは、デバイスをリセットしてメカニズムの原因 (中に電源を入れ、たとえば) バスまたは影響から不足するいると報告されることを複数のデバイス (共有 power など鉄道またはデバイス間で行をリセット) します。 Reset メソッドは、専用のリセットの行を切り替えることや、D3 power リソースの電源を入れ直すとして実装する場合があります、ACPI テーブルで指定されます。 PLDR が実行されると、OS を破棄し、きれいな状態から開始すべて確実に影響を受けるすべてのデバイスのスタックを再構築します。

### <a name="reset-recovery-for-ude-devices"></a>UDE デバイスのリセットの回復 

Windows 10、MBIM 関数を有効にする UDE クライアント ドライバーにはバージョンには 1809 UDECx クライアント ドライバーにエラーが検出されるたびにリセットを要求するために使用できる API が含まれます。 クライアント ドライバーは、新しいメソッドを呼び出すことでリセットを要求[ **UdecxWdfDeviceNeedsReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)、(サポートされている) 場合、デバイスに対して試行する UDECx がリセット型を指定します。 これらの種類はリセットされて**PlatformLevelDeviceReset**と**FunctionLevelDeviceReset**の値と、 [ **UDECX_WDF_DEVICE_RESET_TYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)列挙体。 UDECx がドライバーを呼び出すのリセットが開始されると、 [ *EVT_UDECX_WDF_DEVICE_RESET* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)コールバック関数により、このプロセス中に他のコールバックが呼び出されませんこととします。 クライアント ドライバーを実行することは、いずれかの関連するすべてのリソースを解放などの操作をリセットし、シグナルを呼び出すことによって完了をリセットする[ **UdecxWdfDeviceResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)します。

次のフロー図は、UDE デバイス リセット プロセスを示しています。

![UDECx クライアント ドライバーのリセットの復旧フローのフロー](images/mb-self-healing-udecx-reset.png "ドライバーのリセット復旧 UDECx クライアントにフローを呼び出します。")


## <a name="requirements-for-mb-device-based-reset-and-recovery"></a>MB デバイス ベースのリセットと復旧のための要件

### <a name="requirements-for-fldr"></a>FLDR の要件

必要があります、Device() スコープ内でのデバイスで FLDR をサポートするために、`_RST`メソッドを定義します。 実行すると、このメソッドはそのデバイスのみをリセットする必要があり、別のデバイスに接触する必要があります。 デバイス接続バス上維持する必要もあります。 

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

PLDR、その他のデバイスのリセットの影響を受けるデバイスが共有として表されます、`PowerResource`リセットします。 デバイスでの依存関係を宣言する、`PowerResource`のリセット、およびを`PowerResource`実装、`_RST`メソッド。 

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

また、PLDR は D3Cold 電源の状態にして再度 D0 にデバイスを配置することで実現できる、サイクリング、デバイスの電源を本質的に。 この場合は、発生`_PR3`宣言されているデバイスのスコープは PLDR をサポートするための十分な。 ACPI は使用`_PR3`いない場合は、デバイス間でのリセットの依存関係を判断する`_PRR`デバイスのスコープで参照されています。 詳細については、次を参照してください。[リセットおよびデバイスを回復する](../kernel/resetting-and-recovering-a-device.md)します。 

## <a name="related-links"></a>関連リンク

[ハング検出の MB](mb-hang-detection.md)

[**UDECX_WDF_DEVICE_RESET_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/ne-udecxwdfdevice-_udecx_wdf_device_reset_type)

[**UdecxWdfDeviceNeedsReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

[*EVT_UDECX_WDF_DEVICE_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)

[**UdecxWdfDeviceResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceresetcomplete)

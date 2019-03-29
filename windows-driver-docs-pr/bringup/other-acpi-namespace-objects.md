---
title: その他の ACPI 名前空間オブジェクト
description: デバイスの特定のクラスがいくつか、追加の ACPI 名前空間オブジェクトがそれらのデバイスで、名前空間の下に表示するための要件があります。
ms.assetid: 41EA8C3D-F2C9-4BA9-A839-FCB66F271E3C
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1c713953375df3baa245161244141325ac59261c
ms.sourcegitcommit: 3cdabbe0af52459e484e093a9e11da8f5312daf6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2019
ms.locfileid: "58441932"
---
# <a name="other-acpi-namespace-objects"></a>その他の ACPI 名前空間オブジェクト

デバイスの特定のクラスがいくつか、それらのデバイスで、名前空間の下に表示する追加の Advanced Configuration and Power Interface (ACPI) 名前空間のオブジェクトの要件があります。 このセクションでは、SoC ベースのプラットフォームに必要なその他のオブジェクトが一覧表示します。

## <a name="processor-identification-objects"></a>プロセッサの id オブジェクト

ACPI 名前空間では、プロセッサを列挙する必要があります。 プロセッサが宣言されている\\ \_SB、プラットフォームの他のデバイスと同様、"Device"ステートメントを使用します。 デバイスのプロセッサでは、次のオブジェクトを含める必要があります。

- \_非表示にします。ACPI0007
- \_UID:MADT でプロセッサのエントリと一致する一意の番号。

## <a name="display-specific-objects"></a>表示に固有のオブジェクト

表示に固有のオブジェクトに関する詳細については、の Appendix B「ビデオの拡張機能」を参照してください、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

### <a name="display-specific-object-requirements"></a>オブジェクトの表示に固有の要件

| メソッド | 説明                                        | 要件                                                                      |
|--------|----------------------------------------------------|----------------------------------------------------------------------------------|
| \_DOS  | 出力の切り替えを有効または無効にします。                   | システムが、表示の切り替えや LCD の明るさのレベルをサポートしているかが必要です。          |
| \_DOD  | ディスプレイ アダプターにアタッチされているすべてのデバイスを列挙します。 | 統合されたコント ローラーが出力の切り替えをサポートしているかが必要です。                     |
| \_ROM  | ROM のデータを取得します。                                      | ROM イメージが独自の形式で格納されているかどうかに必要です。                           |
| \_GPD  | 投稿のデバイスを取得します。                                   | 場合に、必ず\_VPO が実装されます。                                                |
| \_SPD  | 投稿のデバイスを設定します。                                   | 場合に、必ず\_VPO が実装されます。                                                |
| \_VPO  | ビデオの POST オプション。                                | システムが変化する post VGA のデバイスをサポートしているかが必要です。                            |
| \_ADR  | このデバイスの一意の ID を返します。              | 必須。                                                                        |
| \_BCL  | サポートされる明るさコントロール レベルのクエリのリスト。 | 埋め込みの LCD が輝度をサポートしているかが必要です。                            |
| \_BCM  | 明るさのレベルを設定します。                          | 場合に、必ず\_BCL が実装されます。                                                |
| \_DDC  | このデバイスには EDID を返します。                   | 必須埋め込まれている場合は、LCD は標準のインターフェイスを使用して EDID の戻り値をサポートしていません。 |
| \_DC  | 出力デバイスの状態を返します。                    | システムが (ホット キー) を使用して切り替える表示をサポートしているかが必要です。                  |
| \_配布グループ  | グラフィックスの状態を照会します。                              | システムが (ホット キー) を使用して切り替える表示をサポートしているかが必要です。                  |
| \_DSS  | デバイスの状態のセット。                                  | システムが (ホット キー) を使用して切り替える表示をサポートしているかが必要です。                  |

## <a name="usb-host-controllers-and-devices"></a>USB ホスト コント ローラーとデバイス

USB ホスト コント ローラーは、内部および外部のデバイスを接続するため、SoC プラットフォームで使用されます。 Windows には、EHCI または XHCI の仕様に準拠している標準的な USB ホスト コント ローラーの受信トレイのドライバーが含まれています。

SoC ベースのプラットフォームでは、ACPI に USB ホスト コント ローラーを列挙できます。 Windows では、次の ACPI 名前空間オブジェクトを列挙すると、USB の互換性のあるハードウェアの構成を使用します。

- ベンダーが割り当てた ACPI に準拠したハードウェア ID (\_HID)。
- 一意の ID (\_UID) オブジェクト、名前空間 (つまり、2 つまたは複数のノードを同一のデバイスの id オブジェクトを持つ) の USB コント ローラーの 1 つ以上のインスタンスがある場合。
- 互換性のある ID (\_CID) の EHCI または XHCI 標準に準拠した USB ホスト コント ローラー (EHCI:PNP0D20)、(XHCI:PNP0D10)。
- 現在のリソースの設定 (\_CRS) USB コント ローラーに割り当てられます。 適切なハードウェア インターフェイスの仕様 (EHCI または XHCI) は、コント ローラーのリソースを説明します。

### <a name="usb-device-specific-method-dsm"></a>USB デバイスに固有のメソッド (\_DSM)

Windows デバイスに固有のメソッドを定義します (\_DSM) USB サブシステムのデバイス クラス固有の構成をサポートします。 詳細については、次を参照してください。 [USB デバイスに固有のメソッド](usb-device-specific-method---dsm-.md)します。

### <a name="usb-integrated-transaction-translator-tt-support-hrv"></a>USB translator (TT) のトランザクションのサポートを統合する (\_HRV)

標準 EHCI ホスト コント ローラーは、高速の USB デバイスのみをサポートします。 SoC のプラットフォームでは、Windows は、低速およびフル スピードの USB デバイス用の統合されたトランザクション変換実装を EHCI 対応のホスト コント ローラーの 2 つの一般的な設計をサポートします。 ハードウェアのリビジョン (\_HRV) オブジェクトが、USB ホスト コント ローラーのドライバーを統合する TT サポートの種類を示します。

\_HRV は、次の条件に基づいて設定されます。

- **NoIntegratedTT - \_HRV = 0**

    標準 EHCI ホスト コント ローラーが統合されたトランザクションの翻訳者を実装しないと、 \_HRV 値 0 はのみにこれらのコント ローラー有効です。 含める必要はありません、\_これらのコント ローラー HRV オブジェクト。

- **IntegratedTTSpeedInPortSc - \_HRV = 1**

    TT の統合のサポートを有効にします。 このフレーバーのインターフェイスは、速度低下を含み、PORTSC HiSpeed ビットが自身を登録します。 これらのビットは 26 および、27 ビットのオフセット位置に、それぞれします。 速度を決定するときに EHCI ドライバーは、PORTSC を読み取るし、これらのビットから速度の情報を抽出します。

- **IntegratedTTSpeedInHostPc - \_HRV = 2**

    TT の統合のサポートを有効にします。 インターフェイスのこのフレーバーには、個別 HOSTPC レジスタに速度低下と HiSpeed bits が含まれています。 EHCI ドライバーは、ポート速度を決定する必要がありますは目的のポートに対応する HOSTPC レジスタを読み取り、速度の情報を抽出します。

### <a name="usb-xhci-d3cold-support"></a>USB XHCI D3cold サポート

選択的に加え、中断、内部の USB デバイスが XHCI コント ローラーに接続されているを D3cold 状態にし、電源オフ時が使用されていません。 詳細については、次を参照してください。[デバイスの電源管理](device-power-management.md)します。 すべての USB デバイス関数ドライバーする必要がありますにオプトイン D3cold します。

### <a name="usb-port-specific-objects"></a>USB ポートに固有のオブジェクト

Windows では、可視性と、システム上の の USB ポートの接続-機能を把握する必要があります。 これは、ポートやデバイスについてユーザーに正確な情報を提供するために必要です。 2 つのオブジェクト、デバイスの物理的な場所 (\_PLD) および USB ポートの機能 (\_UPC)、この目的に使用されます。 詳細については、以下を参照してください。

- 6.1.6 のセクションでは、「デバイスの Id オブジェクト」と 9.13.1、"USB 2.0 ホスト コント ローラーと\_UPC と\_PLD"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。
- [ACPI を使用してコンピューターに USB ポートを構成する](https://docs.microsoft.com/windows-hardware/drivers/install/using-acpi-to-configure-usb-ports-on-a-computer)します。

## <a name="sd-host-controllers-and-devices"></a>SD ホスト コント ローラーとデバイス

SD ホスト コント ローラーは、ストレージと I/O デバイスへのアクセスの SoC プラットフォームで使用されます。 Windows には、標準 SDA ホスト コント ローラーのハードウェア用の受信トレイのドライバーが含まれています。 このドライバーを使用した互換性のため、SD ホスト コント ローラー、デバイスが SD の関連付けに準拠する必要があります[SD ホスト コント ローラー仕様](https://www.sdcard.org/developers/overview/host_controller/)します。

SoC のプラットフォームでは、ACPI に SD ホスト コント ローラーを列挙できます。 Windows では、次の ACPI 名前空間オブジェクトの列挙と SD の互換性のあるハードウェアの構成を使用します。

- ベンダーが割り当てた ACPI に準拠したハードウェア ID (\_HID)。
- 一意の ID (\_UID) オブジェクト、名前空間 (つまり、2 つまたは複数のノードと同一のデバイスの id オブジェクトを) SD コント ローラーの 1 つ以上のインスタンスがある場合。
- 互換性のある ID (\_CID) SDA 標準に準拠した SD ホスト コント ローラー (PNP0D40)。
- 現在のリソースの設定 (\_CRS) コント ローラーに割り当てられます。 コント ローラーのリソースは次のとおりです。

  - 実装されているスロットのすべてのハードウェア リソースが含まれます。 スロットは、メモリまたは I/O デバイス SDIO バス上の接続ポイントです。 各スロットは、接続されているデバイスとの通信に使用するレジスタと SD のホスト コント ローラーで、割り込みの標準セットに関連付けられます。 SD ホスト コント ローラーは、スロットの任意の数を実装できますが、SoC プラットフォームでは、通常 1 つだけです。
  - スロットのリソースはスロット番号の順序で、一覧表示されます (スロット 0 のリソースが最初、スロット 1 のリソースが、これには 2 つ目)。
  - 各スロットのリソースは次の順序で一覧表示します。

        -   標準の SD のベース アドレスは、スロットのセットを登録します。
        -   スロットの SD 標準割り込みです。
        -   GPIO (標準の SD カード検出インターフェイスがすべての電源状態中にサポートされていない) 場合にカードの挿入と削除を通知するため、スロットのリソースを中断します。
        -   カードは、現在スロット (標準の SD カード検出インターフェイスがすべての電源状態中にサポートされていない) かどうか、GPIO は読み取り用のスロットのリソースを入力します。 挿入/削除割り込みとして同じ pin を使用します。
        -   2 番目の GPIO が、スロットには、カードが書き込み保護されているかどうか、読み取り用にリソースを入力 (標準の sd カード書き込み保護インターフェイスの場合はサポートされていませんすべての電源状態中に)。

割り込みは、("SharedAndWake"または"ExclusiveAndWake"として説明します)、ウェイク アップ対応である必要があります。

### <a name="embedded-sd-devices"></a>組み込みの SD デバイス

SD に接続されたデバイスは、SD バス ドライバーによって列挙されます。 プラットフォームに統合されている SD デバイスは、SD ホスト コント ローラーの子として ACPI 名前空間にも表示される必要があります。 この要件によって、オペレーティング システムにバスによって列挙されたデバイスを ACPI オブジェクト (たとえば、removability 以外、デバイスの電源状態、GPIO または SPB リソースの使用およびなど) によって提供されるデバイス プラットフォームに固有の属性に関連付けます。 関連付けを行うには、デバイスの名前空間には、アドレスが必要です (\_ADR)、SDIO バス上のデバイスのアドレスは、通信オブジェクト。 \_ADR オブジェクトは、整数を返します。 SDIO バスのこの整数の値は、次のように定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>SDIO バス</td>
<td><p>上位ワード – スロット番号 (0 – 最初のスロット)</p>
<p>下位ワード – 関数の数 (定義については「SD 仕様。)</p></td>
</tr>
</tbody>
</table>

埋め込み SD デバイス名前空間も含める必要があります。

- Remove メソッド (\_RMV) オブジェクトを (デバイスを削除できないことを示す) に 0 を返します。
- A \_CRS オブジェクト側波帯リソースが必要な場合 (GPIO ピンまたは SPB 接続) など、デバイスが必要です。

## <a name="imaging-class-devices-cameras"></a>イメージング クラスのデバイス (カメラ)

グラフィックス ドライバーまたは USB カメラ デバイスを列挙することがあります。 いずれの場合も、Windows は、適切な UI を表示できるように、カメラの物理的な場所を把握する必要があります。 これを行うには、システムのシャーシに組み込まれているし、方向が修正機械的カメラ デバイス ACPI 名前空間に含まれ、デバイスの物理的な場所を指定 (\_PLD) オブジェクト。 これが必要です。

- 列挙子のデバイス (GPU デバイスまたは USB デバイス) の子 (入れ子になったデバイス) として表示するカメラ デバイス。
- アドレスを入力するカメラ デバイス (\_ADR) 親デバイスのバス上のカメラのアドレスを格納しているオブジェクト。

  - USB を参照してください。 **ACPI 名前空間の階層と\_埋め込みの USB デバイスの ADR**次のセクションでします。
  - グラフィックス、これは、識別子で指定されている、 \_DOD メソッドが、GPU デバイスの 提供します。 詳細については、「ビデオ拡張機能」を ACPI 5.0 仕様の「付録 B を参照してください。

- 提供するカメラ デバイス、 \_PLD オブジェクト。
- (GPIO 割り込みまたは I/O の接続、SPB 接続など)、カメラのドライバーで必要なすべての側波帯リソースがあるかどうか、 \_CRS オブジェクトでは、これらのリソースが提供されます。

\_PLD オブジェクト、**パネル**フィールド (ビット 67 69)**カバー**フィールド (ビット 66) と**ドッキング**サーフェス上の値を修正するフィールド (ビット 65) が設定されて、カメラはマウントされます。 その他のすべてのフィールドは省略できます。 など、タブレット、ハンドヘルド モバイル デバイスの前面パネルは、表示画面を保持している 1 つを起点と左下隅にある縦向きに画面を表示するとき。 この参照を使用して、"Front"ことを示します、カメラが、[戻る] カメラがすぐに表示することを示します (webcam)、ユーザーを表示するユーザー (静止画またはビデオ カメラ) から。 詳細についてを参照してください、セクション、6.1.8"\_PLD (デバイスの物理的な場所)"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

### <a name="acpi-namespace-hierarchy-and-adr-for-embedded-usb-devices"></a>ACPI 名前空間の階層と\_ADR の組み込みの USB デバイス

組み込みの USB デバイスを ACPI 名前空間を追加する場合デバイス ノードの階層する必要がありますと正確に一致する Windows USB ドライバーで列挙されるデバイスの。 これは、「接続ビュー」モードで Windows デバイス マネージャを調べることで確認できます。 USB ホスト コント ローラーから開始し、組み込みのデバイスまで拡張する、階層全体を含める必要があります。 デバイス マネージャーで指定された各デバイスでデバイスのファームウェアを報告する必要があるアドレスは、"Address"プロパティ\_ADR します。

[ACPI 5.0 仕様](https://www.uefi.org/specifications)USB デバイスのアドレスを次のように定義します。

|              |                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------|
| USB ルート ハブ | ホスト コント ローラーの子のみです。 必要があります、 \_ADR は 0。 ない他の子またはの値\_ADR が許可されます。 |
| USB ポート    | ポート番号 (1 ~ n)                                                                                                |

USB デバイスは、そのポートのアドレスを特定のポート共有に接続します。

ポートに接続されているデバイスが複合 USB デバイスの場合は、複合デバイス内の関数は、次のアドレスを使用する必要があります。

|     |     |
| --- | --- |
| 複合 USB デバイスで USB 関数 | 複合デバイスが接続する、関数の最初のインターフェイスの数を足すポートのポート番号。 (加算)。 |

詳細については、次を参照してください。[内蔵カメラの位置を識別する](https://go.microsoft.com/fwlink/p/?linkid=331060)します。

### <a name="asl-code-examples"></a>ASL コードの例

次の ASL コード例には、3 の USB ポートに直接接続されている USB web カメラがについて説明します。

```asl
Device (EHCI) {
    ...  // Objects required for EHCI devices
    Device {RHUB) {         // the Root HUB
     Name (_ADR, ZERO)      // Address is always 0.
     Device (CAM0) {          // Camera connected directly to USB
                       //   port number 3 under the Root.
            Name (_ADR, 3)      // Address is the same as the port.
            Method (_PLD, 0, Serialized) {...}
            }  //  End of Camera device
    } // End of Root Hub Device
}  // End of EHCI device
```

次の ASL コード例では、関数の 2 つとして web カメラを実装する USB 複合デバイスについて説明します。

```asl
Device (EHCI) {
    ...  // Objects required for EHCI devices
    Device {RHUB) {
     Name (_ADR, ZERO)
     Device (CUSB) {        // Composite USB device
                    //   connected to USB port number 3
                    //   under the Root.
            Name (_ADR, 3)      // Address is the same as the port.
            Device (CAM0) { // Camera function within the
                    //   Composite USB device.
                Name (_ADR, 5)  // Camera function has a first
                    //   Interface number of 2, so
                    //   Address is 3 + 2  = 5.
                Method (_PLD, 0, Serialized) {...}
            }  //  End of Camera device
        } // End of Composite USB Device
    } // End of Root Hub Device
}  // End of EHCI device
```

次の ASL コード例には、I2C 経由で接続されている web カメラがについて説明します。

```asl
Device (GPU0) {
    ... // Other objects required for graphics devices
    Name (_DOD, Package ()  // Identifies the children of this graphics device.
                // Each integer must be unique within the GPU0 namespace.
                {
                    0x00024321,  // The ID for CAM0. It is a non-VGA
                    //   device, cannot be detected by
                    //   the VGA BIOS, and uses a vendor-
                    //   specific ID format in bits 15:0
                    //   (see the _DOD specification).
                    ...     // Other child device IDs (for
                    //   example, display output ports)
                })
    Device (CAM0) {
        Name (_ADR, 0x00024321) // The identifier for this device
                    //   (Same as in _DOD above)
        Name (_CRS, ResourceTemplate()
            {
            // I2C Resource
            // GPIO interrupt resource(s), if required by
            //   driver
            // GPIO I/O resource(s), if required by driver
                ...
            })
        Method (_PLD, 0, Serialized) {...}
    } // End of CAM0 device
} // End of GPU0 device
```

## <a name="hid-over-i2c-devices"></a>HID-over-I2C デバイス

Windows には、ヒューマン インターフェイス デバイス (HID) のクラス ドライバーが含まれています。 このドライバーを使用すると、さまざまな入力デバイス (タッチ パネル、キーボード、マウス、センサーなど) のジェネリックのサポート。 SoC のプラットフォームでは、HID デバイスは I2C、経由で、プラットフォームに接続できるし、ACPI によって列挙されます。 Windows で HID クラスのサポートと互換性のため、次の名前空間オブジェクトが使用されます。

- ベンダー固有\_HID
- A \_PNP0C50 の CID
- A\_と CRS:
  - デバイスにアクセスするため、I2CSerialBusConnection リソース
  - Interrupt(s) の GpioInt リソース
- HIDI2C \_DSM デバイス記述子の登録を非表示にアドレスを返すメソッド。 詳細については、次を参照してください。 [HIDI2C デバイス固有のメソッド (\_DSM)](hidi2c-device-specific-method---dsm-.md)します。

## <a name="button-devices"></a>ボタン デバイス

SoC のプラットフォームでは、Windows は、ACPI 定義コントロール メソッド電源ボタンと、Windows と互換性のある 5 つのボタン配列の両方をサポートします。 電源ボタンを ACPI コントロール メソッドの電源ボタンとは、Windows と互換性のあるボタン配列の一部として実装されているかどうかは、次は。

- 電源をオフになっている場合、プラットフォームをによりします。
- 押し下げたときに電源ボタンのオーバーライドのイベントを生成します。 詳細については、ACPI 5.0 仕様のセクション 4.8.2.2.1.3、電源ボタンを上書きする を参照してください。

### <a name="control-method-power-button"></a>コントロールのメソッドの電源ボタン

クラムシェル デザイン、および組み込みまたは接続されているキーボードなどの他のシステム ボタンを実装、ACPI 定義コントロール メソッド Power (ACPI 5.0 仕様のセクション 4.8.2.2.1.2) GPIO-Signaled ACPI イベント (ACPI 5.0 仕様のセクション 5.6.5) を使用します. 電源ボタンのデバイス、名前空間をサポートするには。

- 非共有 (排他) GPIO として電源ボタンの GPIO 割り込み暗証番号 (pin) をについて説明します。 リソースを中断します。
- 電源ボタンの GPIO 割り込みのリソースを一覧表示、 \_AEI、GPIO コント ローラーのオブジェクトが接続されています。
- GPIO コント ローラーのデバイスで関連付けられたイベント メソッド (Lxx/Exx/EVT) を提供します。 このイベント メソッドには、ボタンのイベントが発生したオペレーティング システムのコントロールのメソッドのボタン ドライバーに通知します。

詳細については、次を参照してください。 [Windows 8 タブレットとコンバーチブル デバイス用のハードウェア ボタン](https://go.microsoft.com/fwlink/p/?linkid=331284)します。

### <a name="windows-compatible-button-array"></a>Windows と互換性のあるボタン配列

タッチ ファースト (キーボードのない) プラットフォームでは、スレートなどは、Windows は、5 つのボタンの配列の汎用ドライバーを提供します。 配列内の各ボタンが定義されている関数 (下の一覧で番号付きの項目を参照)、および特定の「保留を押す」ボタンの組み合わせが、UI で追加の意味を持ちます。 ボタンの組み合わせが定義されていない、電源ボタンを押しを必要とします。 Windows の受信トレイ ボタン ドライバーとの互換性、Windows と互換性のあるボタン配列の ACPI デバイスが実装されます。 デバイスの定義は次のとおりです。

- 5 つのボタンの各は、プラットフォームで独自の専用の割り込みピンに接続されます。
- 各割り込み pin が構成されている edge によってトリガーされる (エッジ) として、非共有 (排他)、両方の端 (ActiveBoth) を中断するリソースが中断します。
- デバイスの名前空間には、ベンダー定義が含まれています。 \_HID と同様に、 \_CID の PNP0C40 します。
- GPIO 割り込みのリソース、 \_CRS オブジェクトの次の順序で並んでいます。

    1. "Power"ボタンに対応する中断します。

        "Power"のボタンは、スリープ解除できる (ExclusiveAndWake) である必要があります。

    2. "Windows"ボタンに対応する中断します。

        Windows ボタンは、スリープ解除できる (ExclusiveAndWake) である必要があります。

    3. 割り込み"Volume Up"ボタンに対応します。

        "Volume Up"ボタンをウェイク アップに対応できないする必要があります (排他的に使用する必要があります)。

    4. 割り込み"Volume Down"ボタンに対応します。

        "Volume Down"ボタンがウェイク アップに対応できないする必要があります (排他的に使用する必要があります)。

サポートされている場合、[回転ロック] ボタンに対応するを中断します。

        The "Rotation Lock" button must not be wake-capable (must use Exclusive).

詳細については、次を参照してください。 [Windows 8 タブレットとコンバーチブル デバイス用のハードウェア ボタン](https://go.microsoft.com/fwlink/p/?linkid=331284)します。

Windows を Windows ボタン UI の進化をサポートするには、デバイス固有のメソッドを定義します (\_DSM) ボタン配列の Windows デバイス用です。 詳細については、次を参照してください。 [Windows ボタン配列のデバイスに固有のメソッド (\_DSM)](windows-button-array-device-specific-method---dsm-.md)します。

## <a name="dock-and-convertible-pc-sensing-devices"></a>ドッキング ステーションとコンバーチブル型の PC をデバイスの検出

Windows では、2 つの検出デバイスを ACPI 名前空間を使用して、ドッキングとコンバーチブル (クラムシェル/タブレット combos) がサポートしています。 これらのデバイスは、Windows の受信トレイ ボタン ドライバーでサポートされます。 ボタン配列のデバイスに適用されるのと同じ要件がこれらのデバイスにも適用することに注意してください。

- GPIO ActiveBoth 割り込みは、(SPB 接続 GPIO コント ローラー) にない SoC に GPIO コント ローラーに接続する必要があります。
- GPIO コント ローラーには、サポート レベル モード割り込みと動的の極性が再プログラミングする必要があります。
- GPIO コント ローラーのドライバーによって提供される ActiveBoth エミュレーションを使用する必要があります、 [GPIO フレームワーク拡張](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-i-o-and-interrupt-interfaces)(**GpioClx**)。
- アサートされている状態 (「ドッキング」または"Converted") がロジックのレベルの低い、GPIO コント ローラーがアサートされていない場合\_GPIO ドライバー スタックの既定の動作をオーバーライドする DSM メソッドが必要です。 詳細については、次を参照してください。、 **GPIO コント ローラー デバイス**セクション、[汎用入出力 (GPIO)](general-purpose-i-o--gpio-.md)トピック。

詳細については、次を参照してください。 [Windows 8 タブレットとコンバーチブル デバイス用のハードウェア ボタン](https://go.microsoft.com/fwlink/p/?linkid=331284)します。

### <a name="dock-sensing-device"></a>デバイスのドック検知

Dock が接続されているまたはシステムから接続されていない場合に、ドッキング検知デバイスは、システムを中断します。 このモードの変更情報は、ユーザー入力を更新して、必要なの経験を出力するために使用します。 デバイスの名前空間が必要です。

- ベンダー固有\_HID
- A \_PNP0C70 の CID
- A \_ActiveBoth 割り込みが 1 つと CRS

    割り込みは、ウェイク アップに対応することはできません。

### <a name="convertible-pc-sensing-device"></a>コンバーチブル PC 検出デバイス

コンバーチブル型の PC がタブレットからクラムシェル フォーム ファクターに切り替わるとき、変換可能な PC 検知デバイスは、システムを中断します。 このモードの変更情報は、ユーザー入力を更新して、必要なの経験を出力するために使用します。 デバイスの名前空間が必要です。

- ベンダー固有\_HID
- A \_PNP0C60 の CID
- A \_ActiveBoth 割り込みが 1 つと CRS

    割り込みは、ウェイク アップに対応することはできません。

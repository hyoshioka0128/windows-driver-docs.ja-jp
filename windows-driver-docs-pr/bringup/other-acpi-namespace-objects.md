---
title: その他の ACPI 名前空間オブジェクト
description: デバイスの特定のクラスについては、名前空間内のこれらのデバイスの下に、追加の ACPI 名前空間オブジェクトを表示するための要件があります。
ms.assetid: 41EA8C3D-F2C9-4BA9-A839-FCB66F271E3C
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: f5621dd3ba0a2ed10a28fd9c21fca689590253de
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968046"
---
# <a name="other-acpi-namespace-objects"></a>その他の ACPI 名前空間オブジェクト

デバイスの特定のクラスについては、名前空間内のこれらのデバイスの下に、追加の高度な構成と電源インターフェイス (ACPI) の名前空間オブジェクトを表示するための要件があります。 このセクションでは、SoC ベースのプラットフォームに必要な追加のオブジェクトの一覧を示します。

## <a name="processor-identification-objects"></a>プロセッサ識別オブジェクト

プロセッサは、ACPI 名前空間で列挙する必要があります。 プロセッサは、 \\ \_ プラットフォームの他のデバイスと同様に、"デバイス" ステートメントを使用して SB で宣言されます。 プロセッサデバイスには、次のオブジェクトが含まれている必要があります。

- \_HID: ACPI0007
- \_UID: MADT 内のプロセッサのエントリに一致する一意の番号。

## <a name="display-specific-objects"></a>表示固有のオブジェクト

表示固有のオブジェクトの詳細については、 [ACPI 5.0 仕様](https://uefi.org/specifications)の付録 B 「ビデオ拡張機能」を参照してください。

### <a name="display-specific-object-requirements"></a>表示固有のオブジェクト要件

| メソッド | 説明                                        | 要件                                                                      |
|--------|----------------------------------------------------|----------------------------------------------------------------------------------|
| \_同名  | 出力の切り替えを有効または無効にします。                   | システムがディスプレイの切り替えまたは LCD の明るさのレベルをサポートする場合に必要です。          |
| \_DOD  | ディスプレイアダプターに接続されているすべてのデバイスを列挙します。 | 統合コントローラーで出力の切り替えがサポートされている場合は必須です。                     |
| \_BIOS  | ROM データを取得します。                                      | ROM イメージが専用形式で格納されている場合は必須です。                           |
| \_GPD  | POST デバイスを取得します。                                   | VPO が実装されている場合は必須です \_ 。                                                |
| \_SPD  | POST デバイスを設定します。                                   | VPO が実装されている場合は必須です \_ 。                                                |
| \_VPO  | ビデオの投稿オプション。                                | システムが post VGA デバイスの変更をサポートする場合に必要です。                            |
| \_ADR  | このデバイスの一意の ID を返します。              | 必須です。                                                                        |
| \_BCL  | サポートされている明るさ制御レベルのクエリ一覧。 | 埋め込み LCD が輝度制御をサポートしている場合は必須。                            |
| \_BCM  | 明るさのレベルを設定します。                          | BCL が実装されている場合は必須です \_ 。                                                |
| \_DDC  | このデバイスの EDID を返します。                   | Embedded LCD が標準インターフェイスを介した EDID の返却をサポートしていない場合に必要です。 |
| \_発見  | 出力デバイスの状態を返します。                    | システムがホットキーを使用してディスプレイの切り替えをサポートしている場合は必須です。                  |
| \_DG  | グラフィックスの状態を照会します。                              | システムがホットキーを使用してディスプレイの切り替えをサポートしている場合は必須です。                  |
| \_DSS  | デバイスの状態セット。                                  | システムがホットキーを使用してディスプレイの切り替えをサポートしている場合は必須です。                  |

## <a name="usb-host-controllers-and-devices"></a>USB ホストコントローラーとデバイス

USB ホストコントローラーは、内部および外部のデバイスを接続するために SoC プラットフォームで使用されます。 Windows には、EHCI または XHCI 仕様に準拠している標準の USB ホストコントローラーの受信トレイドライバーが含まれています。

SoC ベースのプラットフォームでは、USB ホストコントローラーを ACPI で列挙できます。 Windows では、互換性のある USB ハードウェアを列挙して構成するときに、次の ACPI 名前空間オブジェクトを使用します。

- ベンダーによって割り当てられた ACPI 準拠のハードウェア ID ( \_ HID)。

- 一意の ID ( \_ UID) オブジェクト。名前空間に USB コントローラーのインスタンスが複数存在する場合 (つまり、同一のデバイス識別オブジェクトを持つ2つ以上のノード)。

- \_Ehci または XHCI の標準に準拠した USB ホストコントローラー (ehci: PNP0D20) の互換性のある ID (CID)、(XHCI: PNP0D10)。

- USB コントローラーに割り当てられている現在のリソース設定 ( \_ CRS)。 コントローラーのリソースについては、適切なハードウェアインターフェイスの仕様 (EHCI または XHCI) で説明されています。

### <a name="usb-device-specific-method-_dsm"></a>USB デバイス固有の方法 ( \_ DSM)

Windows は、 \_ USB サブシステムのデバイスクラス固有の構成をサポートするためのデバイス固有の方法 (DSM) を定義します。 詳細については、「 [USB デバイス固有の方法](usb-device-specific-method---dsm-.md)」を参照してください。

### <a name="usb-integrated-transaction-translator-tt-support-_hrv"></a>USB 統合トランザクション変換ツール (TT) のサポート ( \_ hrv)

標準の EHCI ホストコントローラーは、高速 USB デバイスのみをサポートしています。 SoC プラットフォームでは、Windows で EHCI 準拠のホストコントローラーの2つの一般的な設計がサポートされており、低速および高速の USB デバイス用の統合されたトランザクション変換機能を実装しています。 Hardware Revision ( \_ hrv) オブジェクトは、USB ホストコントローラードライバーに対する統合された TT サポートの種類を示します。

\_Hrv は、次の条件に従って設定されます。

- **Noインテグレーション Atedtt- \_ hrv = 0**

    標準の EHCI ホストコントローラーは、統合されたトランザクション変換器を実装しません。また、 \_ hrv 値0はこれらのコントローラーに対してのみ有効です。 これらのコントローラーには、hrv オブジェクトを含める必要はありません \_ 。

- **IntegratedTTSpeedInPortSc- \_ hrv = 1**

    統合された TT サポートを有効にします。 このインターフェイスのフレーバーには、PORTSC レジスタ自体に LowSpeed と HiSpeed のビットが含まれています。 これらのビットはそれぞれビットオフセット26と27です。 速度を決定するときに、EHCI ドライバーは PORTSC を読み取り、これらのビットから速度情報を抽出します。

- **IntegratedTTSpeedInHostPc- \_ hrv = 2**

    統合された TT サポートを有効にします。 このインターフェイスのフレーバーには、個別の HOSTPC レジスタに LowSpeed ビットと HiSpeed ビットが含まれています。 EHCI ドライバーは、ポート速度を決定する必要がある場合、対象のポートに対応する HOSTPC レジスタを読み取り、速度に関する情報を抽出します。

### <a name="usb-xhci-d3cold-support"></a>USB XHCI D3cold のサポート

セレクティブサスペンドに加えて、XHCI controller に接続されている内部 USB デバイスを D3cold 状態にし、使用されていないときに電源をオフにすることができます。 詳細については、「[デバイスの電源管理](device-power-management.md)」を参照してください。 すべての USB デバイス関数ドライバーは、D3cold にオプトインする必要があります。

### <a name="usb-port-specific-objects"></a>USB ポート固有のオブジェクト

Windows では、システム上の USB ポートの可視性と接続機能を認識している必要があります。 これは、ポートとデバイスに関する正確な情報をユーザーに提供するために必要です。 \_この目的では、物理デバイスの場所 (pld) と USB ポート機能 (UPC) の2つのオブジェクト \_ が使用されます。 詳細については、「

- 「ACPI 5.0 仕様」の「6.1.6」、「デバイス識別オブジェクト」、「9.13.1」、「USB 2.0 ホストコントローラーと UPC」、および「 \_ \_ pld」のセクション。 [ACPI 5.0 specification](https://uefi.org/specifications)

- [ACPI を使用してコンピューターの USB ポートを構成する](https://docs.microsoft.com/windows-hardware/drivers/install/using-acpi-to-configure-usb-ports-on-a-computer)。

## <a name="sd-host-controllers-and-devices"></a>SD ホストコントローラーとデバイス

SD ホストコントローラーは、ストレージや i/o デバイスにアクセスするために SoC プラットフォームで使用されます。 Windows には、SDA 標準のホストコントローラーハードウェア用の受信トレイドライバーが含まれています。 このドライバーとの互換性を確保するために、sd ホストコントローラーデバイスは SD の関連付けの[Sd ホストコントローラー仕様](https://www.sdcard.org/developers/overview/host_controller/)に準拠している必要があります。

SoC プラットフォームでは、SD ホストコントローラーを ACPI で列挙できます。 Windows では、互換性のある SD ハードウェアを列挙して構成するときに、次の ACPI 名前空間オブジェクトを使用します。

- ベンダーによって割り当てられた ACPI 準拠のハードウェア ID ( \_ HID)。

- 一意の ID ( \_ UID) オブジェクト。名前空間に SD コントローラーのインスタンスが複数存在する場合 (つまり、同一のデバイス識別オブジェクトを持つ2つ以上のノード)。

- \_SDA 標準に準拠している SD ホストコントローラー (PNP0D40) の互換性 ID (CID)。

- コントローラーに割り当てられている現在のリソース設定 ( \_ CRS)。 コントローラーのリソースについては、次のように説明します。

  - 実装されているすべてのスロットのハードウェアリソースが含まれます。 スロットは、メモリまたは i/o デバイス用の SDIO バス上の接続ポイントです。 各スロットは、接続されたデバイスとの通信に使用される、標準のレジスタセットと、SD ホストコントローラーの割り込みに関連付けられています。 SD ホストコントローラーは任意の数のスロットを実装できますが、SoC プラットフォームでは、通常は1つだけです。

  - スロットのリソースは、スロット番号の順に一覧表示されます (スロット0のリソースは最初、スロット1のリソースは2番目など)。

  - 各スロットに対して、リソースは次の順序で一覧表示されます。

    - スロットの SD 標準レジスタセットのベースアドレス。

    - スロットの SD 標準割り込み。

    - スロットの GPIO interrupt リソース。カードの挿入と削除をシグナリングします (すべての電源状態で標準の SD カード検出インターフェイスがサポートされていない場合)。

    - カードが現在スロット内にあるかどうかを読み取るためのスロットの GPIO 入力リソース (すべての電源状態で標準の SD カード検出インターフェイスがサポートされていない場合)。 は、挿入/削除割り込みと同じ pin を使用します。

    - スロット内のカードが書き込み禁止になっているかどうかを読み取るための2番目の GPIO 入力リソース (すべての電源状態で標準の SD 書き込み禁止インターフェイスがサポートされていない場合)。

割り込みは、ウェイクアップに対応している必要があります ("SharedAndWake" または "ExclusiveAndWake" と記述されています)。

### <a name="embedded-sd-devices"></a>埋め込み SD デバイス

Sd 接続デバイスは、SD bus ドライバーによって列挙されます。 プラットフォームに統合されている SD デバイスは、SD ホストコントローラーの子として ACPI 名前空間にも記載されている必要があります。 この要件により、オペレーティングシステムは、デバイスに提供されているプラットフォーム固有の属性を、ACPI オブジェクト (たとえば、非 removability デバイスの電源状態、GPIO や SPB のリソースなど) によって、バスで列挙されたデバイスに関連付けることができます。 この関連付けを行うには、デバイスの名前空間に Address (ADR) オブジェクトが必要です。このオブジェクトは、 \_ SDIO バス上のデバイスのアドレスを通信します。 \_ADR オブジェクトは整数を返します。

SDIO バスの場合、この整数の値は次のように定義されます。

- 上位ワード–スロット番号 (0 –最初のスロット)

- Low word –関数の数 (定義については、「SD の仕様」を参照してください)。

埋め込み SD デバイス名前空間には、次のものも含まれている必要があります。

- \_(デバイスを削除できないことを示す) 0 を返す Remove メソッド (rmv) オブジェクト。

- \_必要に応じて、デバイスが必要とする sideband リソース (GPIO ピンや SPB 接続など) の CRS オブジェクト。

## <a name="imaging-class-devices-cameras"></a>イメージングクラスデバイス (カメラ)

カメラデバイスは、グラフィックスドライバーまたは USB で列挙できます。 どちらの場合も、適切な UI を表示できるように、Windows はカメラの物理的な場所を認識している必要があります。 これを行うには、システムのシャーシに組み込まれていて、機械的固定方向のカメラデバイスを ACPI 名前空間に含め、物理デバイスの場所 ( \_ pld) オブジェクトを指定します。 これには次のものが必要です。

- デバイスの子 (入れ子になったデバイス) として表示されるカメラデバイス (GPU デバイスまたは USB デバイス)。

- カメラデバイスは、 \_ 親デバイスのバス上のカメラのアドレスを含む address (ADR) オブジェクトを提供します。

  - USB については、次のセクションの「 ** \_ embedded usb デバイスの ACPI 名前空間階層と ADR** 」を参照してください。

  - グラフィックスの場合、これは、 \_ GPU デバイスで提供される DOD メソッドで指定される識別子です。 詳細については、ACPI 5.0 仕様の付録 B 「ビデオ拡張機能」を参照してください。

- Pld オブジェクトを提供するカメラデバイス \_ 。

- カメラドライバーに必要な sideband リソース (GPIO 割り込み、i/o 接続、SPB 接続など) がある場合は、 \_ これらのリソースに対して CRS オブジェクトが提供されます。

\_Pld オブジェクトでは、**パネル**フィールド (ビット 67-69)、**カバー**フィールド (ビット 66)、および**Dock**フィールド (ビット 65) は、カメラがマウントされているサーフェイスの正しい値に設定されます。 その他のフィールドはすべて省略可能です。 タブレットを含むハンドヘルドモバイルデバイスでは、前面パネルはディスプレイ画面を保持しています。また、画面が縦方向に表示されている場合は、その原点が左下隅に表示されます。 この参照を使用して、"Front" はカメラがユーザー (webcam) を表示していることを示します。 "戻る" は、カメラがユーザー (静止またはビデオカメラ) から離れていることを示します。 詳細については、ACPI 5.0 仕様の「」、「6.1.8」、「 \_ pld (デバイス[ACPI 5.0 specification](https://uefi.org/specifications)の物理的な場所)」を参照してください。

### <a name="acpi-namespace-hierarchy-and-_adr-for-embedded-usb-devices"></a>Embedded USB デバイスの ACPI 名前空間階層と \_ ADR

組み込み USB デバイスを ACPI 名前空間に追加する場合、デバイスノードの階層は、Windows USB ドライバーによって列挙されるデバイスと正確に一致する必要があります。 これを確認するには、Windows デバイスマネージャーで [接続による表示] モードを調べます。 USB ホストコントローラーから始まり、embedded デバイスに拡張される階層全体が含まれている必要があります。 各デバイスのデバイスマネージャーで指定される "Address" プロパティは、ファームウェアがデバイスの ADR で報告する必要があるアドレスです \_ 。

[ACPI 5.0 仕様](https://uefi.org/specifications)では、次のように USB デバイスのアドレスを定義します。

**USB ルートハブ**: ホストコントローラーの子のみです。 ADR は0である必要があり \_ ます。 ADR の他の子または値は使用できません \_ 。

**USB ポート**: ポート番号 (1-n)


特定のポートに接続されている USB デバイスは、そのポートのアドレスを共有します。

ポートに接続されているデバイスが複合 USB デバイスの場合、複合デバイス内の関数は次のアドレスを使用する必要があります。

**複合 usb デバイス内の usb 機能**: 複合デバイスが接続されているポートのポート番号に、関数の最初のインターフェイス番号を加えたもの。 (算術加算)。


詳細については、「[内部カメラの場所の特定](https://docs.microsoft.com/windows-hardware/drivers/devapps/identifying-the-location-of-internal-cameras)」を参照してください。

### <a name="asl-code-examples"></a>ASL のコード例

次の ASL のコード例は、USB ポート3に直接接続されている USB web カメラを示しています。

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

次の ASL コード例では、機能2として web カメラを実装する USB 複合デバイスについて説明します。

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

次の ASL コード例は、I2C 経由で接続された web カメラを示しています。

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

## <a name="hid-over-i2c-devices"></a>HID-I2C デバイス

Windows には、ヒューマンインターフェイスデバイス (HID) 用のクラスドライバーが含まれています。 このドライバーにより、さまざまな種類の入力デバイス (タッチパネル、キーボード、マウス、センサーなど) の一般サポートが有効になります。 SoC プラットフォームでは、HID デバイスは I2C 経由でプラットフォームに接続でき、ACPI によって列挙されます。 Windows での HID クラスのサポートとの互換性のために、次の名前空間オブジェクトが使用されます。

- ベンダー固有の \_ HID

- \_PNP0C50 の CID

- \_次を含む CRS:

  - デバイスにアクセスするための I2CSerialBusConnection リソース

  - 割り込みの GpioInt リソース

- \_デバイスで HID 記述子レジスタアドレスを返すための HIDI2C DSM メソッド。 詳細については、「 [HIDI2C Device 固有の方法 ( \_ DSM)](hidi2c-device-specific-method---dsm-.md)」を参照してください。

## <a name="button-devices"></a>ボタンデバイス

SoC プラットフォームの場合、Windows は、ACPI で定義されたコントロールメソッドの電源ボタンと、Windows と互換性のある5つのボタンの配列の両方をサポートします。 電源ボタンは、ACPI コントロールメソッドの電源ボタンとして実装されているか、Windows と互換性のあるボタン配列の一部として実装されているかにかかわらず、次の操作を実行します。

- オフになっている場合は、プラットフォームの電源を入れます。

- 保持されている場合は、電源ボタンの上書きイベントを生成します。 詳細については、ACPI 5.0 仕様のセクション4.8.2.2.1.3 「電源ボタンのオーバーライド」を参照してください。

### <a name="control-method-power-button"></a>コントロールメソッドの電源ボタン

Clamshell の設計や、組み込みのキーボードまたは接続されているキーボードを使用するその他のシステムでは、GPIO シグナルの ACPI イベント (ACPI 5.0 仕様のセクション 5.6.5) を使用して、ACPI で定義されたコントロールメソッドの電源ボタン (ACPI 5.0 仕様のセクション 4.8.2.2.1.2) を実装します。 電源ボタンデバイス (名前空間) をサポートするには、次のようにします。

- 電源ボタンの GPIO interrupt pin を、共有されていない (排他的な) GPIO interrupt リソースとして記述します。

- 電源ボタンの GPIO interrupt リソースが接続されている \_ gpio コントローラーの AEI オブジェクトに一覧表示されます。

- GPIO コントローラーデバイスの下に、関連付けられているイベントメソッド (Lxx/Exx/.EVT) を提供します。 このイベントメソッドは、ボタンイベントが発生したことをオペレーティングシステムのコントロールメソッドボタンドライバーに通知します。

詳細については、「 [Windows 8 タブレットおよび変換可能なデバイスのハードウェアボタン](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613928(v=vs.85))」を参照してください。

### <a name="windows-compatible-button-array"></a>Windows 互換のボタン配列

スレートなど、タッチファースト (キーボードレス) プラットフォームの場合、Windows は5つのボタンの配列用の汎用ドライバーを提供します。 配列内の各ボタンには定義された関数があります (以下のリストの番号付き項目を参照してください)。また、特定の "押したまま押している" ボタンの組み合わせは、UI にさらに意味があります。 ボタンの組み合わせが定義されていないため、電源ボタンが押されている必要があります。 Windows の [受信トレイ] ボタンドライバーとの互換性を確保するために、Windows と互換性のあるボタン配列 ACPI デバイスが実装されています。 デバイスは次のように定義されます。

- 5つのボタンはそれぞれ、プラットフォーム上の専用の割り込みピンに接続されています。

- 各割り込みピンは、両方のエッジ (ActiveBoth) で割り込みを行う、非共有 (排他) のエッジトリガー (エッジ) 割り込みリソースとして構成されます。

- デバイスの名前空間には、ベンダー定義の \_ HID と PNP0C40 の CID が含まれてい \_ ます。

- CRS オブジェクトの GPIO interrupt リソースは、 \_ 次の順序で一覧表示されます。

    1. [電源] ボタンに対応する割り込み

        [電源] ボタンは、ウェイク対応 (ExclusiveAndWake) である必要があります。

    1. [Windows] ボタンに対応する割り込み

        Windows ボタンは、ウェイク対応 (ExclusiveAndWake) である必要があります。

    1. [ボリュームアップ] ボタンに対応する割り込み

        [ボリュームアップ] ボタンは、ウェイクアップにはできません (排他的に使用する必要があります)。

    1. [音量ダウン] ボタンに対応する割り込み

        [音量ダウン] ボタンは、ウェイクアップに対応している必要はありません (排他を使用する必要があります)。

    1. "回転ロック" ボタンに対応する割り込み (サポートされている場合)

        [回転ロック] ボタンは、ウェイクアップに対応していない必要があります (排他を使用する必要があります)。

詳細については、「 [Windows 8 タブレットおよび変換可能なデバイスのハードウェアボタン](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613928(v=vs.85))」を参照してください。

Windows ボタンの UI の進化をサポートするために、windows では、 \_ Windows ボタン配列デバイス用のデバイス固有のメソッド (DSM) が定義されています。 詳細については、「 [Windows ボタン配列デバイス固有の方法 ( \_ DSM)](windows-button-array-device-specific-method---dsm-.md)」を参照してください。

## <a name="dock-and-convertible-pc-sensing-devices"></a>PC の検出デバイスをドッキングおよび変換する

Windows では、ACPI 名前空間で2つの検出デバイスを使用することによって、コンバーチブル (clamshell/タブレット combos) をサポートしています。 これらのデバイスは、Windows の [受信トレイ] ボタンドライバーでサポートされています。 ボタン配列デバイスに適用されるものと同じ要件が、これらのデバイスにも適用されることに注意してください。

- GPIO ActiveBoth の割り込みは、(SPB 接続の GPIO コントローラーではなく) SoC GPIO コントローラーに接続されている必要があります。

- GPIO コントローラーは、レベルモード割り込みと動的極性 reprogramming をサポートしている必要があります。

- GPIO controller ドライバーは、 [gpio フレームワーク拡張機能](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-i-o-and-interrupt-interfaces)(**gpioclx**) によって提供される activeboth エミュレーションを使用する必要があります。

- アサート状態 ("ドッキング済み" または "変換済み") がアサートされたロジックレベル low でない場合、gpio \_ ドライバースタックの既定の動作をオーバーライドするには、gpio コントローラー DSM メソッドが必要です。 詳細については、「[汎用 i/o (gpio)](general-purpose-i-o--gpio-.md) 」トピックの「 **gpio controller devices** 」セクションを参照してください。

詳細については、「 [Windows 8 タブレットおよび変換可能なデバイスのハードウェアボタン](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613928(v=vs.85))」を参照してください。

### <a name="dock-sensing-device"></a>ドッキングの検出デバイス

ドッキングを検出するデバイスは、ドッキングがシステムにアタッチされているか、システムから接続されていないときにシステムに割り込みます。 このモード変更情報は、必要に応じてユーザーの入力と出力のエクスペリエンスを更新するために使用されます。 デバイスの名前空間には、次のものが必要です。

- ベンダー固有の \_ HID

- \_PNP0C70 の CID

- \_1 つのアクティブな両方の割り込みを持つ CRS

    割り込みをウェイクアップできません。

### <a name="convertible-pc-sensing-device"></a>変換可能 PC の検出デバイス

コンバーチブル pc では、コンバーチブル PC がタブレットから clamshell フォームファクターに切り替わると、システムに割り込みます。 このモード変更情報は、必要に応じてユーザーの入力と出力のエクスペリエンスを更新するために使用されます。 デバイスの名前空間には、次のものが必要です。

- ベンダー固有の \_ HID

- \_PNP0C60 の CID

- \_1 つのアクティブな両方の割り込みを持つ CRS

    割り込みをウェイクアップできません。

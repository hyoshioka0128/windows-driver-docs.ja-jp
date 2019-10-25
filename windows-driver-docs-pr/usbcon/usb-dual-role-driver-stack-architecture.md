---
Description: Windows では、Windows 10 以降で USB デュアルロールコントローラーがサポートされるようになりました。
title: USB デュアル ロール ドライバー スタック アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d166ac2c6f96444f28255aab503e9424903f9801
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844821"
---
# <a name="usb-dual-role-driver-stack-architecture"></a>USB デュアル ロール ドライバー スタック アーキテクチャ


**最終更新日時**

-   2015 年 11 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

Windows では、Windows 10 以降で USB デュアルロールコントローラーがサポートされるようになりました。

## <a name="introduction"></a>概要


USB デュアルロール機能を使用すると、システムを USB*デバイス*または usb*ホスト*にすることができます。 USB デュアルロールの仕様の詳細については、 [usb.org](https://www.usb.org/developers/wusb/docs/presentations/2006/Taipei06_SA_SBD_DRD_Design_Considerations.pdf)の web サイトを参照してください。

ここで重要な点は、デュアルロール機能によって、携帯電話、phablet、タブレットなどのモバイルデバイスがデバイスまたはホストとして指定されていることです。

*機能*モードのモバイルデバイスは、接続されているモバイルデバイスのホストとして機能する PC またはその他のデバイスに接続されます。

モバイルデバイスが*ホスト*モードの場合、ユーザーは、マウスやキーボードなどのデバイスを接続できます。 この場合、モバイルデバイスは接続されているデバイスをホストします。

Windows 10 で USB デュアルロールのサポートを提供することで、次のような利点があります。

-   Bluetooth などのワイヤレスプロトコルと比較して、より大きなデータ帯域幅を提供する、USB を介したモバイル周辺機器への接続。
-   USB を使用して、他の USB デバイスに接続して通信しているときのバッテリの充電のオプション (必要なハードウェアのサポートが存在する場合)。
-   スマートフォンなど、ほとんどの場合、モバイルデバイスを所有している可能性のあるお客様は、すべての仕事に対応できます。 この機能を使用すると、モバイルデバイスがドッキングされ、周辺機器をホストする、ワイヤード (有線) ドッキングシナリオでの生産性が向上します。

次の表に、Windows のデスクトップおよびモバイル Sku で使用できる*ホスト*クラスドライバーの一覧を示します。

| USB ホストクラスドライバー                                             | Windows 10 Mobile | Windows 10 デスクトップ エディション |
|--------------------------------------------------------------------|-------------------|---------------------------------|
| USB ハブ (USBHUB)                                                  | [はい]               | はい (Windows 2000 以降)        |
| HID-キーボード/マウス (HidClass、KBDCLass、ネズミ Class、KBDHid、) | [はい]               | はい (Windows 2000 以降)        |
| USB 大容量記憶装置 (一括 & UASP)                                     | [はい]               | はい (Windows 2000 以降)        |
| 汎用 USB ホストドライバー (WinUSB)                                   | [はい]               | ○ (Windows Vista 以降)       |
| USB オーディオ送受信 (USBAUDIO)                                      | [はい]               | はい (Windows XP 以降)          |
| シリアルデバイス (USBSER)                                            | [はい]               | はい (Windows 10 以降)          |
| Bluetooth (BTHUSB)                                                 | [はい]               | はい (Windows XP 以降)          |
| 印刷 (usbprint)                                                   | 必須ではない                | はい (Windows XP 以降)          |
| スキャン中 (USBSCAN)                                                 | 必須ではない                | はい (Windows 2000 以降)        |
| Web カメラ (USBVIDEO ビデオ)                                                  | 必須ではない                | ○ (Windows Vista 以降)       |
| メディア転送プロトコル (MTP イニシエーター)                            | 必須ではない                | ○ (Windows Vista 以降)       |
| リモート NDIS (RNDIS)                                                | 必須ではない                | はい (Windows XP 以降)          |
| IP over USB (IPoverUSB)                                            | 必須ではない                | はい (Windows 10 の新)        |



表内のクラスドライバーは、デバイスクラスのテレメトリに基づいて選択されており、Windows 10 用に選択された主要なシナリオに基づいています。 Windows 10 Mobile の主要なデバイスをサポートするために、限られた数の受信トレイ、サードパーティのホストドライバーを含めることを計画しています。 また、Windows 10 for desktop のエディションでは、OEM の web サイトまたは Windows Update (WU) を使用してこれらのドライバーを入手できます。

Windows 10 Mobile の場合、受信トレイに含まれていないサードパーティ製のドライバーは、WU では利用できません。 USB ホストスタックと HID のディスクフットプリントが小さくなりました。 ここでは、すべてのクラスドライバーが含まれているわけではなく、ほとんどのサードパーティ製ドライバーが Windows 10 Mobile の受信トレイに含まれているわけではありません。 サードパーティ製のドライバーを使用できるようにする OEM は、ボードサポートパッケージ (BSP) を使用して、モバイルデバイスの OS イメージに追加することができます。 このポリシーの詳細については、「 [Windows Phone のドライバー開発](https://go.microsoft.com/fwlink/p/?LinkId=761246)」を参照して、「 *Windows Phone と Windows のドライバー開発の違い*」というセクションまでスクロールしてください。

次の表は、Windows のモバイル Sku で使用できる*関数*クラスのドライバーを示しています。

**メモ** 関数ドライバーは、Windows 10 for desktop エディションでは使用でき*ません*。



| USB 関数クラスドライバー                 | Windows 10 Mobile | Windows 10 デスクトップ エディション | 注意                                                                                                                                  |
|--------------------------------------------|-------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| メディア転送プロトコル (MTP レスポンダー)    | [はい]               | 必須ではない                              | デスクトップに MTP レスポンダーを使用するシナリオはありません。 デスクトップシステム間の P2P シナリオは、WinUSB を介して簡単に MigCable できるようになりました。 |
| ビデオの表示 (vidstream)              | [はい]               | 必須ではない                              |                                                                                                                                        |
| 汎用 USB 関数ドライバー (GenericUSBFn) | [はい]               | 必須ではない                              | これは、IPoverUSB およびその他のデスクトップの点滅シナリオで必要になります。                                                                 |



デバイスの添付データを監視して、追加のクラスドライバーサポートを提供する必要があるかどうかをお知らせします。これは、デバイスクラスの人気リストが時間の経過と共に変化するためです。

## <a name="driver-implementation"></a>ドライバーの実装


Microsoft USB 役割スイッチ (URS) ドライバーを使用すると、システムの実装者は、そのプラットフォームのデュアルロール USB 機能を利用できます。

URS ドライバーは、単一のポートでホストと周辺の両方の役割を果たすことができる単一の USB コントローラーを使用するプラットフォームに対して、デュアルロールの機能を提供することを目的としています。 *周辺役割*は、*機能ロール*とも呼ばれます。 URS ドライバーは、そのポートの現在の役割、およびプラットフォームからのハードウェアイベントに基づいて、適切なソフトウェアスタックの読み込みとアンロードを管理します。

USB micro-AB コネクタが搭載されているシステムでは、ドライバーは、コネクタの ID ピンの状態を示すハードウェア割り込みを使用します。 この pin は、コントローラーが接続でホストロールと関数ロールのどちらを想定する必要があるかを検出するために使用されます。 詳細については、「 [USB を](https://go.microsoft.com/fwlink/p/?LinkId=698414)使用した場合の仕様」を参照してください。 USB タイプ C コネクタを使用するシステムでは、OEM 実装者は、 [Usb タイプ c コネクタドライバーのプログラミングインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)を使用して、コネクタクライアントドライバーを提供することが想定されています。 クライアントドライバーは、Microsoft が提供する USB コネクタマネージャークラス拡張 (UcmCx) と通信して、CC 検出、PD メッセージングなど、USB タイプ C コネクタのすべての側面を管理します。 役割の交代の場合、クライアントドライバーは、USB タイプ C コネクタの状態を URS ドライバーに伝えます。

次の図は、URS ドライバーを使用するデュアルロールコントローラーの USB ソフトウェアドライバースタックを示しています。

![usb ロール-スイッチドライバースタックのアーキテクチャ。 ](images/dual-role-arch.png)

URS ドライバーは、前の図に示されている関数とホストスタックを同時に読み込まないことに注意してください。 URS ドライバーは、USB コントローラーの役割に応じて、関数スタック*または*ホストスタック*を読み込みます*。

## <a name="hardware-requirements"></a>ハードウェア要件


URS ドライバーを利用するプラットフォームを開発している場合は、デュアルロール USB 機能を提供するために、次のハードウェア要件を満たす必要があります。

-   USB コントローラー

    これらのドライバーは、Microsoft によってインボックスドライバーとして提供されています。

    Synopsys DesignWare Core USB 3.0 コントローラー。 受信トレイ INF: UrsSynopsys .inf。

    Chipidea 高速 USB OTG コントローラー。 受信トレイ INF: UrsChipidea .inf。

-   ID の pin の割り込み

    非 USB タイプ C システムの ID ピン割り込みは、次の2つの方法のいずれかで実装できます。

    エッジによってトリガーされる2つの割り込み: コネクタの ID ピンが接地されたときに発生する割り込みと、ID ピンがフローティング状態のときに発生する割り込みです。

    1つのアクティブな (ID ピンが接地されたときのアクティブレベルの割り込み)。

-   USB コントローラー列挙型

    USB デュアルロールコントローラーは、ACPI で列挙されている必要があります。

-   ソフトウェアのサポート

    URS ドライバーは、コネクタ経由での VBus の制御を可能にするソフトウェアインターフェイスを必要とします。 このインターフェイスは SoC 固有です。 詳細については、SoC ベンダにお問い合わせください。

これらの USB OTG 機能は、Windows ではサポートされていません。

-   アクセサリチャージャーアダプター検出 (ACA)。
-   セッション要求プロトコル (SRP)。
-   ホストネゴシエーションプロトコル (HNP)。
-   接続検出プロトコル (ADP)。

## <a href="" id="acpi"></a>システム構成


URS ドライバーを使用するには、システムの ACPI 定義ファイルを作成する必要があります。 また、ドライバー関連の考慮事項がいくつかあります。

USB デュアルロールコントローラーの ACPI 定義の例を次に示します。

```Text
//
// You may name the device whatever you want; we don't depend on it being called 'URS0'.
//
Device(URS0)
{
    //
    // Replace with your own hardware ID. Microsoft will add it to the inbox INF,
    // or you may choose to author a custom INF that uses Needs & Includes directives
    // to include sections from the inbox INF.
    //
    Name(_HID, "ABCD1234")

    Name(_CRS, ResourceTemplate() {
        //
        // The register space for the controller must be defined here.
        //
        Memory32Fixed(ReadWrite, 0xf1000000, 0xfffff)


        //
        // The ID pin interrupts, if you are using two edge-triggered interrupts.
        //
        GpioInt(Edge, ActiveHigh, Exclusive, PullUp, 0, "\\_SB.GPI0", 0, ResourceConsumer, , ){0x1001}
        GpioInt(Edge, ActiveHigh, Exclusive, PullUp, 0, "\\_SB.GPI0", 0, ResourceConsumer, , ){0x1002}

        //
        // Following is an example of a single active-both interrupt.
        //
        // GpioInt(Edge, ActiveBoth, Exclusive, PullUp, 0, "\\_SB.GPI0", 0, ResourceConsumer, , ){0x12}
        //

        //
        // For a Type-C platform, you do not need to specify any interrupts here.
        //
    })

    //
    // This child device represents the USB host controller. This device node is in effect
    // when the controller is in host mode.
    // You may name the device whatever you want; we don't depend on it being called 'USB0'.
    //
    Device(USB0)
    {
        //
        // The host controller device node needs to have an address of '0'
        //
        Name(_ADR, 0)
        Name(_CRS, ResourceTemplate() {

            //
            // The controller interrupt.
            //
            Interrupt(ResourceConsumer, Level, ActiveHigh, Exclusive, , , ){0x10}
        })
    }

    //
    // This child device represents the USB function controller. This device node is in effect
    // when the controller is in device/function/peripheral mode.
    // You may name the device whatever you want; we don't depend on it being called 'UFN0'.
    //
    Device(UFN0)
    {
        //
        // The function controller device node needs to have an address of '1'
        //
        Name(_ADR, 1)
        Name(_CRS, ResourceTemplate() {

            //
            // The controller interrupt (this could be the same as the one defined in
            // the host controller).
            //
            Interrupt(ResourceConsumer, Level, ActiveHigh, Exclusive, , , ){0x11}
        })
    }
}
```

ここでは、ACPI ファイルの主なセクションについて説明します。

-   URS0 は、USB デュアルロールコントローラーの ACPI 定義です。 これは、URS ドライバーが読み込まれる ACPI デバイスです。

-   USB0 と UFN0 は、URS0 のスコープ内にある子デバイスです。 USB0 と UFN0 は、URS ドライバーによって列挙される2つの子スタックと、それぞれのホストと関数スタックを表します。 \_ADR は、ACPI がこれらのデバイス定義を URS ドライバーによって作成されたデバイスオブジェクトと照合する手段であることに注意してください。

-   コントローラーが両方のロールに同じ割り込みを使用する場合、両方の子デバイスで同じコントローラーの割り込みを記述できます。 その場合でも、割り込みは "排他" として記述できます。

-   必要に応じて、この ACPI 定義ファイルに追加することができます。 たとえば、ACPI 定義ファイル内のいずれかのデバイスで必要なその他のメソッドやプロパティを設定できます。 このような追加によって、URS ドライバーの操作が妨げられることはありません。 任意のスタックに必要なその他のリソースは、適切なデバイスの \_CRS に記述することもできます。

URS ドライバーは、ホストおよび関数スタックにハードウェア Id を割り当てます。 これらのハードウェア Id は、URS デバイスのハードウェア ID から派生します。 たとえば、ハードウェア ID が ACPI\\ABCD1234 の URS デバイスがある場合、URS ドライバーは次のようにホストおよび機能スタックのハードウェア Id を作成します。

-   ホストスタック: URS\\ABCD1234 & ホスト

-   関数スタック: URS\\ABCD1234 & 関数

## <a href="" id="inf"></a>ドライバーのインストールパッケージ


必要に応じて、サードパーティ製のドライバーパッケージがこのスキームに依存している可能性があります。

IHV または OEM で、独自のドライバーパッケージを提供することを検討している場合は、次の点を考慮する必要があります。

- URS ドライバーパッケージ

  各プラットフォームのデュアルロールコントローラーのハードウェア ID が URS の受信トレイ INF に追加されることが想定されています。 ただし、何らかの理由で ID を追加できない場合、IHV/OEM は、受信トレイ INF を必要とし、そのハードウェア ID と一致する INF を含むドライバーパッケージを提供することがあります。

  これは、IHV/OEM がドライバースタックにフィルタードライバーを提示する必要がある場合に必要です。

- ホストドライバーパッケージ。

  受信トレイの*usbxhci*が必要/インクルードされ、ホストデバイスのハードウェア ID と一致する必要がある、IHV/OEM が提供するドライバーパッケージが必要です。 ハードウェア ID の一致は、前のセクションで説明したスキームに基づいています。

  これは、IHV/OEM がドライバースタックにフィルタードライバーを提示する必要がある場合に必要です。

  URS ドライバーがホストデバイスに対して XHCI と互換性のある ID を割り当てるために進行中の作業があります。

- 関数ドライバーパッケージ

  受信トレイ*Ufxsynopsys*が必要/インクルードされ、周辺機器ハードウェア ID と一致する必要がある、IHV/OEM 提供のドライバーパッケージ。 ハードウェア ID の一致は、前のセクションで説明したスキームに基づいています。

  また、IHV/OEM は、ドライバーパッケージにフィルタードライバーを含めることもできます。
  ## <a name="see-also"></a>参照

[デュアルロールコントローラードライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#dual-role-controller-driver-reference)







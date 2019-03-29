---
Description: 2 つのロールを USB コント ローラーは、Windows、Windows 10 以降ではサポートされています。
title: USB デュアル ロール ドライバー スタック アーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505f71a6bf3b1ad66aeb377cae63a9ab4ecd9adc
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348941"
---
# <a name="usb-dual-role-driver-stack-architecture"></a>USB デュアル ロール ドライバー スタック アーキテクチャ


**最終更新日**

-   2015 年 11 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

2 つのロールを USB コント ローラーは、Windows、Windows 10 以降ではサポートされています。

## <a name="introduction"></a>概要


USB デュアル ロール機能により、システムのいずれかの USB を*デバイス*または USB*ホスト*します。 USB デュアル ロールの詳細な仕様で確認できます、 [usb.org](http://www.usb.org/developers/wusb/docs/presentations/2006/Taipei06_SA_SBD_DRD_Design_Considerations.pdf) web サイト。

ここでの重要なポイントは、2 つのロール機能は、電話、ファブレット、またはタブレットでは、デバイスまたはホストされている自体を指定するなどのモバイル デバイスです。

モバイル デバイスの場合で*関数*モードでは、PC または接続しているモバイル デバイスのホストとして機能する他のいくつかのデバイスにアタッチされています。

モバイル デバイスの場合*ホスト*モードでは、ユーザーは、マウスやキーボードなど、デバイスをそれにアタッチできます。 この場合、モバイル デバイスが接続されているデバイスをホストします。

Windows 10 での USB デュアル ロール、サポートを提供し、次の利点を提供します。

-   Bluetooth などのワイヤレス プロトコルと比較して、大きなデータ帯域幅を提供する USB 経由でモバイルの周辺機器を接続します。
-   バッテリに接続されている USB 経由での課金と (必要なハードウェアのサポートが限り存在する) 他の USB デバイスとの通信のオプションです。
-   ほとんどの場合、すべての作業のスマート フォンなどのモバイル デバイスを所有するお客様を有効にします。 この機能により、生産性の向上ワイヤード (有線) のドッキング シナリオでモバイル デバイスがドッキングし、そのための周辺機器をホストします。

次の表の一覧を示します*ホスト*Sku の Windows デスクトップおよびモバイルで使用できるドライバーのクラスします。

| ホストの USB クラス ドライバー                                             | Windows 10 Mobile | Windows 10 デスクトップ エディション |
|--------------------------------------------------------------------|-------------------|---------------------------------|
| USB ハブ (USBHUB)                                                  | はい               | はい (Windows 2000) 以降        |
| HID のキーボード/マウス (HidClass、KBDCLass、MouClass、KBDHid、MouHid) | はい               | はい (Windows 2000) 以降        |
| USB 大容量記憶装置 (一括 & UASP)                                     | はい               | はい (Windows 2000) 以降        |
| 汎用 USB ホスト ドライバー (WinUSB)                                   | はい               | [はい] (Windows Vista) 以降       |
| USB オーディオ入力/出力 (USBAUDIO)                                      | はい               | [はい] (Windows XP) 以降          |
| シリアル デバイス (USBSER)                                            | はい               | [はい] (Windows 10) 以降          |
| Bluetooth (BTHUSB)                                                 | はい               | [はい] (Windows XP) 以降          |
| 印刷 (usbprint)                                                   | いいえ                | [はい] (Windows XP) 以降          |
| スキャン (USBSCAN)                                                 | いいえ                | はい (Windows 2000) 以降        |
| Web カメラ (USBVIDEO)                                                  | いいえ                | [はい] (Windows Vista) 以降       |
| メディア転送プロトコル (MTP 開始側)                            | いいえ                | [はい] (Windows Vista) 以降       |
| リモート NDIS (RNDIS)                                                | いいえ                | [はい] (Windows XP) 以降          |
| IP over USB (IPoverUSB)                                            | いいえ                | [はい] (新しい Windows 10 の)        |



デバイス クラスの遠隔測定に基づいており、Windows 10 用に選択された主なシナリオに基づいて、テーブル内のクラス ドライバーが選択されています。 Windows 10 Mobile のデバイスのキーをサポートするために、サード パーティ製ホスト ドライバーの受信トレイ、限られた数を含むで予定です。 Windows 10 デスクトップ エディションの場合、これらのドライバーは、OEM の web サイトや Windows Update (WU) 経由で提供されます。

Windows 10 Mobile の含まれる受信トレイではないサード パーティ製のドライバーは WU に利用可能なできません。 USB ホスト スタック + HID のディスク フット プリントは、少数に抑えされています。 すべてのクラス ドライバーと非常にいくつかのサード パーティ製ドライバーは、なぜこれは、Windows 10 Mobile の受信トレイが含まれています。 サード パーティ製ドライバーを使用できるようにすることを希望する OEM は、ボード サポート パッケージ (BSP) を使用して、自分のモバイル デバイス用の OS イメージに追加できます。 このポリシーの詳細については、次を参照してください。 [Windows Phone 向けドライバー開発](https://go.microsoft.com/fwlink/p/?LinkId=761246)、というセクションまでスクロールして*Windows Phone 用ドライバーの開発と Windows 間の違い*します。

次の表は、*関数*クラス ドライバーを Windows のモバイル Sku では使用できます。

**注**関数ドライバーが*いない*デスクトップ エディションの Windows 10 で使用できます。



| 関数の USB クラス ドライバー                 | Windows 10 Mobile | Windows 10 デスクトップ エディション | メモ                                                                                                                                  |
|--------------------------------------------|-------------------|---------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| メディア転送プロトコル (MTP 応答側)    | はい               | いいえ                              | デスクトップ上の MTP レスポンダーのシナリオはありません。 デスクトップ システム間での P2P シナリオは、WinUSB 経由で簡単な MigCable 経由で有効にされました。 |
| Out (vidstream) のビデオの表示              | はい               | いいえ                              |                                                                                                                                        |
| 一般的な USB 機能ドライバー (GenericUSBFn) | はい               | いいえ                              | これは、IPoverUSB とシナリオが点滅している他のデスクトップで必要になります。                                                                 |



添付ファイルのデータをデバイス監視、デバイスとして、追加のクラス ドライバーのサポートを提供する必要がありますを知らせ、クラスの人気のリストが時間と共に変化します。

## <a name="driver-implementation"></a>ドライバーの実装


Microsoft USB ロール スイッチ (URS) ドライバーは、そのプラットフォームのデュアル ロール USB 機能を活用するためにシステムの実装を使用できます。

URS ドライバーは、1 つのポート経由でホストと周辺のロールの両方で動作する単一の USB コント ローラーを使用するプラットフォームのデュアル ロール機能を提供するものです。 *周辺のロール*とも呼ばれますが、*関数ロール*します。 URS ドライバーでは、ポート、および読み込みの現在のロールと、プラットフォームからハードウェア イベントに基づいて、適切なソフトウェア スタックのアンロードを管理します。

USB micro AB コネクタがあるシステムで、ドライバーは、ハードウェアの割り込みのコネクタ ID ピンの状態を示すに使用します。 この pin は、コント ローラーがホストの役割または接続が関数の役割を想定する必要があるかどうかを検出するために使用されます。 詳細については、次を参照してください。、 [USB に外出先から仕様](https://go.microsoft.com/fwlink/p/?LinkId=698414)します。 使用して、コネクタのクライアント ドライバーを提供するシステム型-C# の USB コネクタでは、OEM 実行者が期待どおり、[型-C# の USB コネクタ ドライバーのプログラミング インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)します。 クライアント ドライバーは、CC の検出、PD がメッセージング、およびその他のユーザーなど、Manager クラスの拡張機能 (UcmCx)、USB 型-c コネクタのすべての側面を管理する Microsoft 提供の USB コネクタと通信します。 役割の交代、クライアント ドライバーは、URS ドライバーを USB 型-c コネクタの状態を通信します。

次の図には、URS ドライバーを使用するデュアル ロール コント ローラーの USB ソフトウェア ドライバー スタックが表示されます。

![usb の役割の交代ドライバー スタック アーキテクチャです。 ](images/dual-role-arch.png)

URS ドライバーが同時に、前の図に示した関数とホストのスタックを読み込まないことに注意してください。 URS ドライバーをロード*か*関数の履歴*または*USB コント ローラーの役割によって、ホスト スタック。

## <a name="hardware-requirements"></a>ハードウェア要件


URS ドライバの利用するプラットフォームを開発している場合のデュアル ロール USB 機能を提供する、次のハードウェア要件が満たす必要があるがあります。

-   USB コント ローラー

    これらのドライバーは、インボックス ドライバーと Microsoft によって提供されます。

    Synopsys DesignWare Core USB 3.0 コント ローラー。 受信トレイ INF:UrsSynopsys.inf します。

    Chipidea 高速 USB OTG コント ローラー。 受信トレイ INF:UrsChipidea.inf します。

-   ID の暗証番号 (pin) の割り込み

    2 つの方法のいずれかで USB 型-C 以外のシステム ID pin interrupt(s) を実装することがあります。

    2 つのエッジによってトリガーされる割り込み: と ID の暗証番号 (pin) が固定されていないときに起動されるもう 1 つのコネクタ ID pin が接地、ときに起動します。

    1 つアクティブ両方の割り込みレベルにあるアクティブなときに、ID の pin が基礎になっています。

-   USB コント ローラーの列挙型

    USB のデュアル ロール コント ローラーは、ACPI 列挙をする必要があります。

-   ソフトウェアのサポート

    URS ドライバーには、VBus コネクタ経由で制御できるようにするソフトウェア インターフェイスで必要があります。 このインターフェイスは、SoC 固有です。 詳細については、SoC、ベンダーにお問い合わせください。

これらの USB OTG 機能は、Windows ではサポートされません。

-   アクセサリ充電器アダプターの検出 (ACA)。
-   セッション要求のプロトコル (SRP)。
-   ネゴシエーション プロトコル (HNP) をホストします。
-   検出プロトコル (ADP) をアタッチします。

## <a href="" id="acpi"></a>システムの構成


URS ドライバーを使用するには、システムの ACPI 定義ファイルを作成する必要があります。 また、特定のドライバーに関連する注意事項を考慮する必要がありますが使用されます。

USB デュアル ロール コント ローラーの ACPI 定義の例を次に示します。

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

いくつかの説明については、ACPI ファイルの主要なセクションを次に示します。

-   URS0 は、デュアル ロールの USB コント ローラーの ACPI 定義です。 これは、ACPI デバイス URS ドライバーが読み込まれます。

-   USB0 と UFN0 は、URS0 のスコープ内の子デバイスです。 USB0 と UFN0 URS ドライバーで列挙する 2 つの子スタックとホストと関数のスタックをそれぞれ表します。 なお\_ADR は ACPI するには、URS ドライバーを作成するデバイス オブジェクトを持つこれらのデバイス定義と一致することを意味します。

-   コント ローラーは、両方のロールの同じ割り込みを使用している場合は、子デバイスの両方で同じコント ローラーの割り込みを記述できます。 その場合でも、割り込み依然として記述できます「排他的です」

-   必要に応じてこの ACPI 定義ファイルへの追加を行うことができます。 たとえば、ACPI の定義ファイルで、デバイスのいずれかで他の必要なメソッドやプロパティを設定できます。 このような追加機能は、URS ドライバーの操作には影響しません。 スタックのいずれかで必要なその他のリソースで記述できます、 \_CRS の適切なデバイス。

URS ドライバーでは、ホストと関数のスタックにハードウェア Id を割り当てます。 これらのハードウェア Id は、URS デバイスのハードウェア ID から派生します。 たとえば、ハードウェア ID を持つ URS デバイスがある場合は、ACPI\\ABCD1234、し URS ドライバー作成ハードウェア Id、ホストと関数のスタックの次のようにします。

-   ホストのスタック:URS\\ABCD1234 &AMP; ホスト

-   関数の履歴:URS\\ABCD1234 関数 (&AMP;)

## <a href="" id="inf"></a>ドライバー インストール パッケージ


サード パーティ製のドライバー パッケージは、必要に応じて、このスキームでは、に対して依存関係を実行できます。

IHV または OEM のドライバー パッケージを提供する検討する場合は、次にいくつかの考慮事項を示します。

- URS ドライバー パッケージ

  URS の各プラットフォームでデュアル ロール コント ローラーのハードウェア ID が受信トレイの INF に追加することが必要です。 ただし場合何らかの理由は、ID を追加できません、IHV と OEM 提供する必要があります/受信トレイ INF を含み、そのハードウェアの id。 一致する INF でドライバー パッケージ

  これは、ために必要な場合は、IHV と OEM がドライバー スタックに存在するフィルター ドライバーが必要です。

- ドライバー パッケージをホストします。

  必要がある/受信トレイが含まれている IHV と OEM が提供ドライバー パッケージ*usbxhci.inf*と一致するホスト デバイスのハードウェア ID が必要です。 ハードウェア ID の一致は、前のセクションで説明されているスキームに基づくなります。

  これは、ために必要な場合は、IHV と OEM がドライバー スタックに存在するフィルター ドライバーが必要です。

  XHCI の互換性のある ID、ホスト デバイスを割り当てる URS ドライバーに進行中の作業があります。

- ドライバー パッケージの関数

  必要がある/受信トレイが含まれている IHV と OEM が提供ドライバー パッケージ*Ufxsynopsys.inf*と一致するハードウェア ID の周辺機器が必要です。 ハードウェア ID の一致は、前のセクションで説明されているスキームに基づくなります。

  また、IHV と OEM は、ドライバー パッケージにフィルター ドライバーを含めることができます。
  ## <a name="see-also"></a>関連項目

[デュアル ロール コント ローラー ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#dual-role-controller-driver-reference)







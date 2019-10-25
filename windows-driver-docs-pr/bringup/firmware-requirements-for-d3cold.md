---
title: D3cold のファームウェア要件
description: Windows 8 以降では、システムが S0 電源状態のままであっても、デバイスは D3cold の電源サブ状態に入ることができます。
ms.assetid: 4BADC310-CC53-4084-A592-66197C348279
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4084c49517e1d3dde685243b7c700d36ac70ba0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834516"
---
# <a name="firmware-requirements-for-d3cold"></a>D3cold のファームウェア要件


Windows 8 以降では、システムが S0 電源状態のままであっても、デバイスは D3cold の電源サブ状態に入ることができます。 このトピックでは、embedded デバイスの D3cold サポートを実装するためのファームウェアの要件について説明します。 次の説明は、ファームウェア開発者が、埋め込みデバイスで D3cold を確実に入力して終了できるようにするためのものです。

また、D3cold をサポートするためのデバイスドライバーの要件についても簡単に説明します。 D3cold のデバイスドライバーサポートの詳細については、「[ドライバーでの D3cold](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-d3cold-in-a-driver)のサポート」を参照してください。

## <a name="introduction"></a>概要


[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)は、ACPI 仕様およびさまざまなバス仕様で定義されています。 PCI バス仕様には PCI 電源管理が導入されたため、D3 (オフ) デバイスの電源状態が2つのサブ状態 (D3hot と D3cold) に分割されています。 この区別は acpi 3.0 の acpi 仕様に追加され、ACPI 4.0 で拡張されました。 Windows では常に D3 のサブ状態がサポートされていますが、windows 7 以前のバージョンの windows では、コンピューター全体が S0 (動作) システムの電源状態を終了して、スリープ状態または休止状態 (通常は S3 または S4) になる場合にのみ、D3cold サブ状態がサポートされます。 Windows 8 以降では、デバイスドライバーは、システムが S0 のままであっても、デバイスが D3cold 状態になることを可能にします。

D3hot は、多くの場合 "D3" と呼ばれ、デバイスの "ソフトオフ" 状態です。 この状態では、バススキャンによってデバイスが検出され、デバイスに送信されたコマンドによってデバイスの電源が再度オンになる可能性があります。 D3cold では、すべての電源が削除されます。ただし、デバイスのウェイクアップロジックを駆動するために少量の電力を使用する場合があります。 たとえば、PCI Express (PCIe) デバイスの場合、D3cold への移行では、主なデバイスの電源と Vcc がオフになっていることがよくあります。 Vcc をオフにすると、電力消費が減少し、モバイルハードウェアプラットフォームをバッテリ充電で実行できる時間が長くなります。 デバイスが D3cold にある場合、バススキャンでは検出できず、コマンドを受け取ることはできません。 Vcc パワーを復元すると、デバイスが初期化されていない状態に移行します。これは通常、D0 状態と同じです。 その後、ソフトウェアはデバイスを再初期化して、デバイスを動作中の状態にする必要があります。

デバイスを D3cold に配置することは、デバイスの電源のすべての供給元が取り外されているという意味ではありません。これは、メイン電源の Vcc が取り外されているだけであることを意味します。 Wake ロジックに必要ない場合は、補助電源 (Vaux) も削除される可能性があります。 ただし、ウェイクアップイベントをプロセッサに通知するために必要なデバイスは、ウェイクアップロジックを操作するのに十分なパワーを描画できる必要があります。 たとえば、メインの電源が入っているイーサネットネットワークインターフェイスカード (NIC) は、イーサネットケーブルから十分な電力を引くことができます。 または、Wi-fi NIC のスタンバイ電源が、PCIe インターフェイスの外部のソースから提供される場合があります。この場合、PCIe インターフェイスは完全にオフにできます。

次の説明では、デバイスの電源状態を D3cold に移行できるようにするための一連の要件について説明します。 これらの要件は、次の2つのカテゴリに分類されます。

-   ファームウェアとプラットフォームの要件
-   デバイスドライバーの要件

これら2つのカテゴリのうちの1つ目は、この説明の主な焦点です。 2番目のカテゴリの簡単な概要が示されます。 デバイスドライバーの要件の詳細については、「 [D3cold でのドライバーのサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-d3cold-in-a-driver)」を参照してください。

## <a name="firmware-and-platform-requirements"></a>ファームウェアとプラットフォームの要件


次の説明では、これらの2つの場合に、D3cold を有効にするためのファームウェアとプラットフォームの要件について説明します。

-   デバイスが ACPI で列挙されたとき。
-   デバイスが親バスによって列挙された場合。

以下の説明のほとんどは、PCIe に固有のものです。 ただし、ここで説明する一般的な原則は、他のバスにも当てはまります。

いくつかの詳細を抽象化すると、embedded デバイスに Vcc power を再適用することで、D3cold から D0 への移行がトリガーされます。 電源を再適用すると、デバイスのバスへの接続が効果的に復元されます。 Windows は、次の2つのケースを区別するためにデバイスの識別子を読み取ります。

-   デバイスが削除され、別のデバイスに置き換えられました。
-   同じデバイスが削除されてから再挿入されました。

識別子が一致する場合は、デバイスドライバーによってデバイスが再初期化されます。 識別子が一致しない場合、Windows はデバイスドライバーをアンロードし、新しいデバイス用の新しいドライバースタックを構築します。 たとえば、ベンダー ID、デバイス ID、およびサブシステム Id に対するクエリ (一部のバージョンの仕様では、サブデバイスとサブベンダー Id に分割されます)。 これらの識別子は、電源が再適用された後に、以前に接続されたデバイスの id と一致する必要があります (およびバス指定の待機期間が経過した場合)。そうしないと、新しいデバイスは前のデバイスとは異なるものと見なされます。

### <a name="case-1-an-embedded-device-is-enumerated-in-acpi"></a>ケース 1: 組み込みデバイスが ACPI で列挙される

組み込みデバイスが PCIe や USB などのバス仕様で定義されているメカニズムによって検出されないが、デバイスが完全に接続されている (または、少なくとも既知のデバイスに接続されている) 場合は、プラットフォームファームウェアでこのデバイスを記述できます。ACPI \_HID または \_CID オブジェクト。 これらのオブジェクトにより、OSPM によってデバイスが列挙されます。 ("OSPM" は、ACPI 仕様で定義されている用語です。 これは、"ファームウェアではないソフトウェア" を意味します。OSPM は、バス列挙子がデバイス ID を検出できない場合にのみ、デバイスを列挙します。 たとえば、ISA バス上のデバイスは、OSPM によって列挙されます。 さらに、チップ (SoC) 上のシステム上のデバイスは、列挙できないファブリック上にあるため、多くの場合、ACPI によって列挙されます。 このようなデバイスの例としては、USB および SD ホストコントローラーなどがあります。

**プラットフォームのファームウェア**

OSPM は \\\_SB.\_.OSC を使用してプラットフォーム全体の OSPM 機能をプラットフォームファームウェアに伝達します。 プラットフォームのファームウェアでは、\\\_SB.\_の .OSC 戻り値を設定して、デバイスが \_PR3 をサポートしていることを OSPM に示す必要があります。 詳細については、ACPI 5.0 仕様の「6.2.10.2 the Platform Wide OSPM Capabilities」セクションを参照してください。

**Embedded デバイス– ACPI によってのみ検出**

D3cold をサポートするには、プラットフォームのファームウェアで、embedded デバイスの次の ACPI 電源リソースオブジェクトを実装する必要があります。

-   \_PR0: このオブジェクトは、D0 (完全にオン) デバイスの電源状態のデバイスの電力要件に評価されます。 戻り値は、デバイスが D0 状態で必要とする電源リソースの一覧です。
-   \_PR2: このオブジェクトは、D2 デバイスの電源状態のデバイスの電力要件に評価されます。 戻り値は、デバイスが D2 状態で必要とする電源リソースの一覧です。 歴史的な理由から、\_PR0 が存在する場合、Windows では \_PR2 が存在する必要があることに注意してください。 D2 がハードウェアに実装されている場合、\_PR2 は D2 に必要な電力リソースの一覧を表示します。 D2 が実装されていない場合、\_PR2 では \_PR0 と同じリソースが一覧表示されます。
-   \_PR3: このオブジェクトは、D3hot デバイスの電源状態のデバイスの電力要件に評価されます。 戻り値は、デバイスが D3hot 状態で必要とする電源リソースの一覧です。
-   \_PRx オブジェクトで識別される各電源リソースについて、次のコントロールメソッドを実装する必要があります。

    -   \_オフ: 電源リソースを*オフ*の状態に設定します (リソースの電源をオフにします)。
    -   \_: 電源リソースを*オン*状態 (リソースの電源) に設定します。
    -   \_STA: このオブジェクトは、電源リソース (0: off、1: on) の現在の*オン*または*オフ*の状態に評価されます。

D3cold への移行は、ACPI が \_PR3 に一覧表示されている電源リソースの \_オフコントロールメソッドを実行すると発生します。 デバイス関数ドライバーで D3cold のサポートが示されている場合、このサポートでは、D3 に対するすべての移行が D3cold に移行することを意味するわけではないことに注意してください。 デバイスが長時間にわたって D3hot に入って保持され、D3cold を入力せずに D0 に戻るか、後で D3cold を入力する可能性があります。

**親デバイス**

親デバイスの電源管理を可能にするための要件はありません。 ただし、親デバイスが電源管理されている場合、その子 (依存デバイス) のいずれかが D3 に含まれていないと、Windows はこのデバイスの電源を切ることができません。

**例**

次のブロック図は、システムバス上の組み込みデバイス ( **Embd**) を示しています。 デバイスに対する主電源 (**Vcc**) と補助電力 (**vaux**) は、ラベルが付いた**電源ロジック**で個別にオンとオフを切り替えることができます。

![acpi で列挙された埋め込みデバイス](images/d3cold1.png)

次の ASL コード例では、前の図の組み込みデバイスで使用される電力リソースについて説明します。 この例では、まず、デバイスドライバーの機能を記述する \_のコードを宣言します。 次に、デバイスの2つの電源リソースが宣言されます。リソース名 PVCC と PVCC は、デバイスのメインおよび補助電源 ( **Vcc**と**vaux**) に割り当てられます。 最後に、デバイスがサポートするデバイスの電源状態ごとに電力リソースの要件が一覧表示され、デバイスのウェイクアップ機能について説明します。

```asl
Scope (\_SB)
{
     Method(_OSC, 4, NotSerialized) // Platform-wide Capabilities Check.
     {  
          ... // This must indicate support for _PR3.
     }

     PowerResource(PVCC,0,0) // Power resource representing the main power for the device.
                             // Required for the device to be fully functional (D0).
     {
          Name(_STA,VAR1)        // Return the state of the power resource.
          Method(_ON,0x0) {...}  // Turn on the power resource and set VAR1 to 1.
          Method(_OFF,0x0) {...} // Turn off the power resource and set VAR1 to 0.
     }

     PowerResource(PVAX,0,0) // Power resource representing the auxiliary power for the device.
                             // Required for low-power, less-functional states (e.g., D3hot).
     {
          Name(_STA,VAR2)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     Device(EMBD) // An ACPI-enumerated device on the processor bus that supports D3Cold
     {
               Name(_HID, ...)
               ... // Other (non-power) objects for this device

          // Indicate support for D0.
               Name(_PR0, Package() {PVCC, PVAX}) // Power resources required for D0

          // Indicate support for D1 (optional)...

          // Indicate support for D2.
               Name(_PR2, Package() {PVCC, PVAX}) // If D2 is implemented in the hardware,
                                                  //  list the power resources needed by D2.
                                                  // If D2 is not implemented, list the same
                                                  //  resources as _PR3.

          // Indicate support for D3Cold.
               Name(_PR3, Package() {PVCC, PVAX}) // Power resource for D3. These will be 
                                                  //  turned off ONLY if drivers opt-in to D3cold.
 
          // Indicate support for wake. Required for entry into D3cold, even if the device doesn't
          // need or have a wake mechanism.
               Name(_S0W, 4) // The existence of this object indicates that the platform is
                             //  capable of handling wake events from this device while in S0. 
                             // The value of this object indicates the lowest D-state this device
                             //  can be in to trigger wake events that can be handled while the
                             //  platform is in S0.

          // Enable wake events (optional) 
          //  If this device actually does generate wake events, there must be a way for OSPM to
          //  enable and disable them. The mechanism for this depends on the platform hardware:
               /*
               Name(_PRW, ...) // If the event is signaled via a GPE bit (SCI) OR
                               //  if there are power resources required only for wake.
               Name(_CRS, ...) // If the event is signaled via a wake-capable interrupt.
                
               Method(_DSW, 3) {...) // Can be used with either of the above, if wake enablement
                                     // varies depending on the target S-state and D-state.
               */
     }  // End of Device EMBD
} End Scope \_SB
```

### <a name="case-2-an-embedded-device-is-bus-enumerated"></a>ケース 2: 組み込みデバイスがバスで列挙されている

Embedded デバイスが PCIe や USB などの一般的なバス仕様に準拠している場合、このデバイスはバス定義メカニズムによって検出可能であり、電源を部分的または完全にバス経由で提供できます。 このデバイスに他の sideband 電源リソースが搭載されていない場合、デバイスのメイン電源は、デバイスを親バスコントローラーに接続するリンクです。 バスで列挙されたデバイスは、embedded デバイスの定義で \_ADR オブジェクトによって識別できます。 \_ADR オブジェクトは、embedded デバイスの親バス上のデバイスのアドレスを OSPM に提供するために使用されます。 このアドレスは、バスハードウェアによって示されるように、バスのデバイスの表現をデバイスのプラットフォームの表現 (ACPI ファームウェアによる) に関連付けるために使用されます。 (\_ADR アドレスのエンコードはバス固有です。 詳細については、ACPI 5.0 仕様のセクション6.1.1 「\_ADR (Address)」を参照してください。)このメカニズムを使用する場合は、D3cold サポートを親バスドライバーと連携させる必要があります。

Embedded デバイスのメインの電源がこのデバイスを親バスに接続するリンクである場合、デバイスを D3cold に配置するための重要な要件は、リンクの電源を切ることです。 D3cold への移行の詳細については、「デバイスの[電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)」の状態グラフを参照してください。

**プラットフォームのファームウェア**

OSPM は \\\_SB.\_.OSC を使用してプラットフォーム全体の OSPM 機能をプラットフォームファームウェアに伝達します。 プラットフォームのファームウェアでは、\\\_SB.\_の .OSC 戻り値を設定して、デバイスが \_PR3 をサポートしていることを OSPM に示す必要があります。 詳細については、ACPI 5.0 仕様の「6.2.10.2 the Platform Wide OSPM Capabilities」セクションを参照してください。

**埋め込みデバイス**

D3cold 固有の ACPI 変更は必要ありません。 この場合、デバイスドライバーとプラットフォームで D3cold のサポートが示されていれば、親バスが D0 を終了し、省電力状態の Dx に入ると、embedded デバイスに電力を供給するバスリンクをオフにすることができます。 埋め込みデバイスの D3hot から D3cold への移行は、リンクから電源が削除されると発生します。 親バスによって入力される Dx の状態は、リンクの電源をオフにする状態にすることができます。

**親デバイス**

親バスの ACPI 記述子は、次の操作を行う必要があります。

-   \_S0W (Dx) を実装します。 このオブジェクトは、システムが S0 状態のときに子 (埋め込み) デバイスをスリープ解除できる最小の電源 D 状態として Dx を指定します。

-   子 (埋め込み) デバイスを親バスに接続するリンクを表すために、電源リソースを定義します。 さらに、この電源リソースに対して、\_オン、\_オフ、および \_の STA オブジェクトを定義する必要があります。 この一覧の後に続く ASL コード例では、PVC1 と PVX1 という2つのリソースとしてのリンクの電源について説明しています。 これらの各リソースについて、\_ON、\_OFF、および \_STA オブジェクトが定義されています。

-   "Dx" (1 番目のリスト項目を参照してください) が D3cold の場合は、子 (埋め込み) デバイスが D3hot に必要とする電力リソース (Vcc、Vaux など) を含む \_PR3 オブジェクトを指定します。 D0、D2、および D3hot に同じ電源が必要な場合は、\_PR0、\_PR2、\_PR3 all で同じ電源リソースを指定します。 これらのリソースは、子デバイスが D3cold に入ったときにのみオフになります。

    履歴上の理由により、\_PR0 が存在する場合、Windows では \_PR2 が存在する必要があります。 D2 がハードウェアに実装されている場合、\_PR2 は D2 に必要な電力リソースの一覧を表示します。 D2 が実装されていない場合、\_PR2 では \_PR0 と同じリソースが一覧表示されます。

-   \_PR0 を実装します。 親バスの \_PR0 オブジェクト内のリソースの一覧には、親バスを子 (埋め込み) デバイスに接続するリンクを電源に入れるリソースが含まれている必要があります。

**例**

次のブロック図のハードウェア構成の例では、PCIe デバイスに対して D3cold を有効にする2つの方法を示しています。 まず、エンドポイント (名前は**Endp**) が pcie ルートポート (**が rp01 で**) に接続され、 **pcie リンク**を介して親デバイスから補助電力を受け取ります。 2つ目の方法として、図の**HD オーディオ**デバイスは、親デバイス ( **PCI0**というラベルが付いた PCI コントローラー) への標準リンクを持っていないため、ACPI で列挙されたケースと同様にモデル化されています。

![バスで列挙された埋め込みデバイス](images/d3cold2.png)

この図の**が rp01 で**デバイスには、主電源、 **Vcc1**、および補助電源 ( **Vaux1**) があります。 同様に、 **HD オーディオ**デバイスには、主電源、 **Vcc2**、および補助電力供給 ( **Vaux2**) があります。

次の ASL コードでは、前の図に示した**Endp**と**HD オーディオ**デバイスに必要な、親バスコントローラー (**PCI0**) と電力リソースについて説明しています。

```asl
Scope (\_SB)
{
     Method(_OSC, 4, NotSerialized) // Platform-wide Capabilities Check.
     {  
          ... // This must indicate support for _PR3.
     }

     PowerResource(PVC1,0,0) // Power resource representing Vcc1 for the RP01 device.
                             // Required for the device(s) to be fully functional (D0).
     {
          Name(_STA,VAR0)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     PowerResource(PVX1,0,0) // Power resource representing Vaux1 for the RP01 device.
                             // Required for low-power, less-functional states (e.g., D3hot).
     {
          Name(_STA,VAR1)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     PowerResource(PVC2,0,0) // Power resource representing Vcc2 for the HD device.
                             // Required for the device(s) to be fully functional (D0).
     {
          Name(_STA,VAR2)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     PowerResource(PVX2,0,0) // Power resource representing Vaux2 for the HD device.
                             // Required for low-power, less-functional states (e.g., D3hot).
     {
          Name(_STA,VAR3)
          Method(_ON,0x0) {...}
          Method(_OFF,0x0) {...}
     }

     ... // Power resources for other child devices

     Device(PCI0) // The PCI root complex
     {
          Name(_HID, EISAID("PNP0A08"))  // ACPI enumerated
          Method(_OSC, 4, NotSerialized) // PCIe-specific Capabilities Check.
          {     
               ... // This must support hand-off of PCIe control to the OS.
          }
          ... // Other (non-power) objects for this device

          Device(RP01) // PCIe Root Port 1
          {
                    Name(_ADR, "...") // Bus enumerated
                    ... // Other (non-power) objects for this device
    
               // Indicate support for D0.
                    Name(_PR0, Package() {PVC1, PVX1}) // Power resources required for D0.
                                                       // Includes the Link Power for ENDP.

               // Indicate support for D1 (optional)...

               // Indicate support for D2.
                    Name(_PR2, Package(){PVC1, PVX1}) 

               // Indicate support for wake. Required for entry into D3cold, even if the
               // device doesn't need or have a wake mechanism.
                    Name(_S0W, 4) // The existence of this object indicates the platform
                                  //  is capable of handling wake events from this device
                                  //  while the platform is in S0. 
                                  // The value of this object indicates the lowest D-state
                                  //  this device can be in to trigger wake events that 
                                  //  can be handled while the platform is in S0.

               // Enable wake events (optional) 
               //  If this device actually does generate wake events, there must be a way
               //  for OSPM to enable and disable them. The mechanism for this depends on
               //  the platform hardware:

                    /*
                    Name(_PRW, ...) // If the event is signaled via a GPE bit (SCI) OR
                                    //  if there are power resources required only for wake.
                    Name(_CRS, ...) // If the event is signaled via a wake-capable interrupt.

                    Method(_DSW, 3) {...) // Can be used with both of the above, if wake
                                          //  enablement varies depending on the target 
                                          //  S-state and D-state.
                    */

                    Device(ENDP) // This device supports D3cold. No power-related objects
                                 // are required.
                    {
                         Name(_ADR, "...")  // Bus enumerated
                         ... // Other (non-power) objects
                    }  // End of Device ENDP
          }  // End of Device RP01

          Device(HD) // A PCIe Bus0 device (HD Audio) that supports D3cold. Note that
                     //  this case is modeled similar to the ACPI-enumerated case
                     //  because device HD has no standard link to its parent.
          {
                    Name(_ADR, "...") // Bus enumerated
                    ... // Other (non-power) objects for this device
    
               // Indicate support for D0.
                    Name(_PR0, Package() {PVC2, PVX2}) // Power resources required for D0
                            
               // Indicate support for D1 (optional)...

               // Indicate support for D2.
                    Name(_PR2, Package(){PVC2, PVX2})

               // Indicate support for D3Cold.
                    Name(_PR3, Package() {PVC2, PVX2}) // Power resource for D3; These will
                                                       //  be turned off ONLY if drivers
                                                       //  opt-in to D3cold.
 
               // Indicate support for wake. Required for entry into D3cold, even if the
               // device doesn't need or have a wake mechanism.
                    Name(_S0W, 4) // The existence of this object indicates that the platform
                                  //  is capable of handling wake events from this device 
                                  //  while the platform is in S0. 
                                  // The value of this object indicates the lowest D-state
                                  //  this device can be in to trigger wake events that can
                                  //  be handled while the platform is in S0.

               // Enable wake events (optional). 
               //  If this device actually does generate wake events, there must be a way for
               //  OSPM to enable and disable them. The mechanism for this depends on the HW:
                    /*
                    Name(_PRW, ...) // If the event is signaled via a GPE bit (SCI) OR
                                    //  if there are power resources required only for wake.
                    Name(_CRS, ...) // If the event is signaled via a wake-capable interrupt.

                    Method(_DSW, 3) {...) // Can be used with both of the above, if wake
                                          //  enablement varies depending on the target
                                          //  S-state and D-state.
                    */
          }  // End Device HD

          ... // Device objects for other child devices

     }  // End Device PCI0
}  // End Scope \_SB
```

### <a name="other-possibilities"></a>その他の可能性

前の2つの例に示されている手法を組み合わせて、バスパワーと sideband の両方の機能を使用する構成をサポートできます。

## <a name="device-driver-requirements"></a>デバイスドライバーの要件


デバイスの電源ポリシー所有者 (通常は関数ドライバー) は、デバイスの D3hot から D3cold への移行を有効にするかどうかをオペレーティングシステムに通知します。 ドライバーは、デバイスをインストールする INF ファイルにこの情報を提供できます。 または、ドライバーは実行時に[*SetD3ColdSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)ルーチンを呼び出して、デバイスの D3cold への移行を動的に有効または無効にすることができます。 デバイスで D3cold を入力できるようにすることで、ドライバーは次の動作を保証します。

-   コンピューターが S0 のままになっている場合、デバイスは D3hot から D3cold への移行を許容できます。
-   デバイスは、D3cold から D0 に戻ると正常に動作します。

いずれかの要件を満たしていないデバイスは、D3cold を入力した後に、コンピューターが再起動されるか、またはスリープ状態になるまで使用できません。 デバイスが、入力された省電力の Dx 状態からウェイクアップイベントを通知できる必要がある場合、D3cold へのエントリを有効にすることはできません。ただし、デバイスのスリープ解除信号が D3cold で動作することがドライバーによって特定される場合を除きます。

詳細については、「 [D3cold でのドライバーのサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-d3cold-in-a-driver)」を参照してください。

 

 





---
title: D3cold のファームウェア要件
description: Windows 8 以降では、デバイスを入力できます D3cold 電源のサブ状態システム S0 電源の状態のままになる場合でもです。
ms.assetid: 4BADC310-CC53-4084-A592-66197C348279
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff10d3af3c23cf857e2e68f772bfeacc59683d03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557659"
---
# <a name="firmware-requirements-for-d3cold"></a>D3cold のファームウェア要件


Windows 8 以降では、デバイスを入力できます D3cold 電源のサブ状態システム S0 電源の状態のままになる場合でもです。 このトピックでは、D3cold を実装するための要件をサポートして、embedded デバイスのファームウェアをについて説明します。 次の説明の目的は、embedded デバイスを確実に入力し、D3cold の終了を有効にするファームウェアの開発者を支援します。

さらに、D3cold をサポートするためのデバイス ドライバーの要件について簡単に説明します。 D3cold のデバイス ドライバーのサポートについての詳細については、[ドライバーではサポートしている D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)を参照してください。

## <a name="introduction"></a>概要


[デバイスの電源状態](https://msdn.microsoft.com/library/windows/hardware/ff543162)ACPI の仕様とバスのさまざまな仕様で定義されます。 PCI バスの仕様には、PCI 電源管理が導入されてからは、2 つのサブ状態 D3hot と D3cold に (off) デバイスの電源状態 D3 を分割します。 この区別は、ACPI 3.0 では ACPI の仕様に追加され、ACPI 4.0 で拡張されました。 Windows が常に両方 D3 のサブ状態をサポートするが、Windows 7 および以前のバージョンの Windows のサポート、D3cold サブ状態マシン全体に S0 が終了したときにのみ、スリープまたは休止状態の状態を入力する (操作) システムの電源状態 — 通常 S3 または S4 します。 Windows 8 以降、デバイス ドライバーの自分のデバイス、システムに残ります S0 中でも D3cold 状態にできるようにします。

"D3"と呼ばれる多くの場合だけ、D3hot は、デバイスの「ソフト オフ」状態です。 この状態で、バスをスキャンして、デバイスを検出でき、デバイスに送信されたコマンドできます電源でもう一度します。 D3cold でデバイスのスリープ解除のロジックを促進するための電力量が少ないことを除いて、すべての電源は削除されます。 たとえば、PCI Express (PCIe) デバイスでは、メインのデバイスの電源ソース Vcc、頻繁に無効になって D3cold への移行にします。 Vcc オフにすると、電力消費量を削減し、モバイル ハードウェア プラットフォームは、バッテリの充電で実行できる時間を拡張できます。 D3cold でデバイスがある場合はバス スキャンによって検出されないし、コマンドを受信することはできません。 Vcc 電源を入れ、そのデバイスが D0 の状態には、通常と同じですが、初期化されていない状態に移動します。 ソフトウェアは、稼働状態に配置するデバイスを再初期化しする必要があります。

D3cold にデバイスを配置することは必ずしもデバイスの電源のすべてのソースが削除されている-は、主電源ソース Vcc が削除されるだけです。 ウェイク アップ ロジックに必要でない場合、補助電力ソース、Vaux を削除も可能性があります。 ただし、プロセッサにウェイク イベントを通知に必要なデバイスは、スリープ解除ロジックを操作するための十分な電力を消費できる必要があります。 たとえばのイーサネット ネットワーク インターフェイス カード (NIC) が主電源ソースを削除では、イーサネット ケーブルから電力が十分を描画する可能性があります。 または、する場合、PCIe インターフェイス完全にオフにすること、PCIe インターフェイスの外部ソースから Wi-fi NIC にスタンバイ電源を指定する場合があります。

次の詳細については、一連の要件は D3cold にデバイスの電源の状態遷移を有効にするため説明します。 これらの要件は、次の 2 つのカテゴリに分類されます。

-   ファームウェアとプラットフォームの要件
-   デバイス ドライバーの要件

これら 2 つのカテゴリの 1 つ目は、この説明の中心です。 2 番目のカテゴリの簡単な概要が表示されます。 デバイス ドライバーの要件の詳細については、[ドライバーではサポートしている D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)を参照してください。

## <a name="firmware-and-platform-requirements"></a>ファームウェアとプラットフォームの要件


次の説明では、これら 2 つのケースの D3cold を有効にするためのファームウェアとプラットフォームの要件が表示されます。

-   ときに、デバイスは、ACPI に列挙されます。
-   ときに、デバイスがその親バスによって列挙されます。

次の説明のほとんどは、PCIe に固有です。 ただし、他のバスも大きくここで説明した一般的な原則が適用されます。

いくつかの詳細を抽象化 D3cold から D0 への移行は、embedded デバイスに Vcc 電源を再適用することでトリガーされます。 電源を効果的に再適用すると、バスにデバイスの接続が復元されます。 Windows では、次の 2 つのケースを区別するために、デバイスの識別子を読み取ります。

-   デバイスが削除され、別のデバイスによって置き換えられます。
-   同じデバイスが削除され、後に再挿入します。

識別子が一致している場合、デバイス ドライバーには、デバイスが再初期化します。 識別子が一致しない場合、Windows は、デバイス ドライバーをアンロードし、新しいデバイスの新しいドライバー スタックを構築します。 PCIe、たとえば、ベンダーの ID、デバイス ID、およびサブシステムの Id (仕様の一部のバージョンでサブデバイスとサブ ベンダーの Id に分類されます) をクエリします。 これらの識別子と一致しなければなりません以前接続されているデバイスの電源が再適用 (とバスが指定した待機期間が経過する)。それ以外の場合、Windows では、別の 1 つ前に新しいデバイスが考慮されます。

### <a name="case-1-an-embedded-device-is-enumerated-in-acpi"></a>ケース 1:組み込みデバイスは、ACPI に列挙されます。

組み込みデバイスは検出 PCIe など、USB バス仕様で定義されているメカニズムではありませんが、デバイスが完全に接続されている場合 (または、少なくとも接続は、既知のデバイス専用)、このデバイスは、プラットフォーム ファームウェアで記述できますACPI \_HID や\_CID オブジェクト。 これらのオブジェクトは、OSPM で列挙するデバイスを有効にします。 ("OSPM"は、ACPI 仕様で定義されている用語です。 これは、ため、疎、「ファームウェアのないソフトウェア」)バスの列挙子がデバイス ID を検出しなかった場合にのみ、OSPM はデバイスを列挙します。 たとえば、ISA バス上のデバイスは、OSPM によって列挙されます。 さらに、チップ (SoC) 上のシステム上のデバイスが列挙可能でないファブリック上にあるため、多くの場合、ACPI に列挙されます。 このようなデバイスの例には、USB や SD のホスト コント ローラーが含まれます。

**プラットフォーム ファームウェア**

OSPM を使用して\\ \_SB.\_OSC プラットフォームのファームウェアにプラットフォーム全体にわたる OSPM 機能を伝達するためにします。 プラットフォームのファームウェアでは、ビット 2 を設定する必要があります、 \\ \_SB.\_OSC をデバイスをサポートしている OSPM を示す値を返す\_PR3 します。 詳細については、ACPI 5.0 仕様の 6.2.10.2、「プラットフォーム全体にわたる OSPM 機能」」セクションを参照してください。

**ACPI を通じてのみ検出 – embedded デバイス**

D3cold をサポートするために、プラットフォーム ファームウェアは、embedded デバイスの次の ACPI power リソース オブジェクトを実装する必要があります。

-   \_PR0:このオブジェクトは、D0 (完全に) デバイスの電源状態で、デバイスの電源の要件を評価します。 戻り値は、D0 状態で、デバイスに必要な電源リソースのリストです。
-   \_PR2:このオブジェクトは、D2 デバイスの電源状態で、デバイスの電源の要件を評価します。 戻り値は、D2 状態で、デバイスに必要な電源リソースの一覧です。 歴史的な理由から、Windows を期待しているに注意してください\_たびに存在する PR2 \_PR0 が存在します。 ハードウェアの D2 が実装されている場合\_PR2 D2 に必要な電源リソースを一覧表示します。 D2 が実装されていない場合\_PR2 と同じリソースを一覧表示\_PR0 します。
-   \_PR3:このオブジェクトは、D3hot デバイスの電源状態で、デバイスの電源の要件を評価します。 戻り値は、D3hot 状態で、デバイスに必要な電源リソースのリストです。
-   いずれかで識別される各 power リソースの\_PRx オブジェクト、次の制御メソッドを実装する必要があります。

    -   \_オフします。電源のリソースを設定、*オフ*状態 (電源オフ、リソース)。
    -   \_オン:電源のリソースを設定、*で*状態 (電源オン、リソース)。
    -   \_STA の場合:このオブジェクトが現在評価*で*または*オフ*power リソースの状態 (0: オフ、1: 上)。

ACPI の実行時に D3cold への遷移が発生、 \_OFF コントロール メソッドで示されている電源リソース\_PR3 します。 ドライバー関数では、D3cold のサポートが示されている場合このサポートを意味しません D3 にすべての遷移が D3cold に swift の遷移になることに注意してください。 デバイスが入力し D3hot のまま、長期間にわたってし D0 D3cold のこれまで入力せずに戻しますか D3cold を入力した後でことができます。

**親デバイス**

親デバイスを電源管理の対応する必要はありません。 ただし、親デバイスが電源管理対象の場合、Windows しない電源ダウンこのデバイス D3 にその子 (依存しているデバイス) のいずれかがない場合。

**例**

次のブロック図は、embedded デバイスを示しています (というラベルの付いた**EMBD**) システム バスにします。 主電源 (**Vcc**) と補助電源 (**Vaux**) デバイスに個別に有効にできましていないオンとオフというラベルが付いたブロック**ロジックの電源を**します。

![acpi 列挙 embedded デバイス](images/d3cold1.png)

ASL の次のコード例では、前の図では、embedded デバイスで使用される電源リソースについて説明します。 この例の宣言から始まります、 \_OSC コントロール メソッドをデバイス ドライバーの機能について説明します。 次に、デバイスの 2 つの電源のリソースが宣言されている-PVCC と PVAX がデバイスの主なや補助機能のソースに割り当てられているリソース名**Vcc**と**Vaux**します。 最後に、power リソースの要件は、デバイスをサポートする各デバイスの電源状態にし、デバイスのウェイク アップ機能が説明されています。

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

### <a name="case-2-an-embedded-device-is-bus-enumerated"></a>ケース 2:組み込みデバイスは、bus 列挙

Embedded デバイスでは、共通のバス仕様に準拠している場合、このデバイスは、bus によって定義されたメカニズムを探索可能な PCIe USB などれ、電源一部または全部バスを介して指定されます。 このデバイスが他の側波帯 power リソースで電源がいない場合、デバイスの主な電源、親のバス コント ローラーに、デバイスを接続するリンクです。 バスで列挙されるデバイスで識別できます、 \_embedded デバイスの定義で、ADR オブジェクト。 \_ADR オブジェクトは、embedded デバイスの親のバス上のデバイスのアドレスを持つ OSPM を指定するために使用します。 このアドレスは、(ACPI ファームウェアに表示される) とデバイスのプラットフォームの表現に (バス ハードウェアに表示される) とデバイスのバスの表現に使用されます。 (、 \_ADR アドレスのエンコーディングは、バスに固有です。 詳細については、section 6.1.1 を参照してください"\_ADR (アドレス)"、ACPI 5.0 仕様です。)。このメカニズムが使用されている場合、D3cold サポートが親バス ドライバーを使用した調整する必要があります。

組み込みデバイスの主な電源がその親のバスをこのデバイスを接続するリンクの場合は、D3cold にデバイスを配置するため、重要な要件は、リンクの電源です。 D3cold への移行の詳細については、状態のグラフを参照してください。[デバイスの電源状態](https://msdn.microsoft.com/library/windows/hardware/ff543162)します。

**プラットフォーム ファームウェア**

OSPM を使用して\\ \_SB.\_OSC プラットフォームのファームウェアにプラットフォーム全体にわたる OSPM 機能を伝達するためにします。 プラットフォームのファームウェアでは、ビット 2 を設定する必要があります、 \\ \_SB.\_OSC をデバイスをサポートしている OSPM を示す値を返す\_PR3 します。 詳細については、ACPI 5.0 仕様の 6.2.10.2、「プラットフォーム全体にわたる OSPM 機能」」セクションを参照してください。

**Embedded デバイス**

D3cold 固有 ACPI の変更は必要ありません。 ここでは、デバイス ドライバーとプラットフォームによっては、D3cold のサポートが示されますが、限り bus リンクは、embedded デバイスの電源を提供することができますオフにする親バスは、D0 を終了し、Dx 低電力状態になったときに。 D3cold に D3hot から、embedded デバイスへの移行では、電源がリンクから削除されたときに発生します。 Dx 状態親バスが入力するには、リンクの電源をオフにすると、任意の状態を指定できます。

**親デバイス**

親バスの ACPI 記述子では、次の操作を行う必要があります。

-   実装\_S0W(Dx) します。 このオブジェクトは、システムが S0 状態元となる子 (埋め込み) デバイスがスリープ解除できる最も低い power D 状態として Dx を指定します。

-   親バスを子 (埋め込み) デバイスを接続するリンクを表す power リソースを定義します。 さらに、 \_、 \_OFF および\_この電源リソースの STA オブジェクトを定義する必要があります。 この一覧を次の ASL コード例では、PVC1 と PVX1 の 2 つのリソースとしてリンク機能について説明します。 これらのリソースごとに\_、 \_OFF および\_STA オブジェクトが定義されています。

-   "Dx"(最低 power D 状態は、最初の項目を参照してください) が D3cold の場合は、提供、\_子 (埋め込み) デバイスが (たとえば、Vcc と Vaux) D3hot を必要とする power リソースを含む PR3 オブジェクト。 同じ電源が、D0、d2 に切り替わり、および D3hot、必要な場合\_PR0、 \_PR2、および\_PR3 すべてが同じ電源リソースを指定します。 子デバイス D3cold を入力した場合にのみ、これらのリソースがオフになります。

    Windows では歴史的な理由から、\_たびに存在する PR2 \_PR0 が存在します。 ハードウェアの D2 が実装されている場合\_PR2 D2 に必要な電源リソースを一覧表示します。 D2 が実装されていない場合\_PR2 と同じリソースを一覧表示\_PR0 します。

-   実装\_PR0 します。 リソースの一覧、\_親 bus PR0 オブジェクトには、親のバスを子 (埋め込み) デバイスに接続しているリンクの電源をリソースが含まれている必要があります。

**例**

次のブロック図のハードウェア構成の例では、PCIe デバイスに対して D3cold を有効にできる 2 つの方法を示します。 最初に、エンドポイント (というラベルの付いた**ENDP**) PCIe ルート ポートに接続されている (**が rp01 で**) を通じて、親デバイスから補助電源の送受信、 **PCIe リンク**します。 2 つ目は、 **HD オーディオ**、ダイアグラム内のデバイスに、親デバイスへの標準的なリンクがありません (というラベルの付いた PCI コント ローラー **PCI0**) およびモデル化同様に、したがって ACPI 列挙ケースにします。

![バス列挙 embedded デバイス](images/d3cold2.png)

**が rp01 で**この図では、デバイスが主電源**Vcc1**、および補助電源**Vaux1**します。 同様に、 **HD オーディオ**デバイスが主電源**Vcc2**、および補助電源**Vaux2**します。

次の ASL コードが、親のバス コント ローラーについて説明します (**PCI0**) と必要な電源リソース、 **ENDP**と**HD オーディオ**デバイス上の図に示すようにします。

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

### <a name="other-possibilities"></a>その他の方法

前の 2 つの例で示した技法は、両方のバスの電源および側波帯 power を使用する構成をサポートするために結合できます。

## <a name="device-driver-requirements"></a>デバイス ドライバーの要件


(関数ドライバーでは通常) デバイスの電源ポリシー所有者は、D3hot から D3cold へのデバイスの移行を有効にするかどうかをオペレーティング システムに指示します。 ドライバーでは、デバイスをインストールする INF ファイルでは、この情報を提供できます。 または、ドライバーを呼び出すことができます、 [ *SetD3ColdSupport* ](https://msdn.microsoft.com/library/windows/hardware/hh967716)定期実行時に動的に有効または D3cold にデバイスの移行を無効にします。 D3cold を入力するデバイスを有効にすると、ドライバーは、次の動作を保証します。

-   デバイスは、コンピューターの S0 内に存続するとき、D3hot から D3cold への移行を許容できます。
-   D0 に D3cold から返されるときに、デバイスが正常に動作はします。

いずれかの要件を満たすために失敗したデバイスできない可能性があります、D3cold を入力すると、使用可能なコンピューターが再起動されるかがスリープ状態になるまでです。 デバイスは、それが入力する低電力 Dx 状態からウェイク イベントを通知できる必要がある場合、ドライバーは、特定のデバイスのウェイク信号 D3cold で動作する場合を除き、D3cold にエントリが有効にしない必要があります。

詳細については、[ドライバーではサポートしている D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)を参照してください。

 

 





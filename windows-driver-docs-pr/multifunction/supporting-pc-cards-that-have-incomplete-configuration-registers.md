---
title: 不完全な構成レジスターを持つ PC カードのサポート
description: 不完全な構成レジスターを持つ PC カードのサポート
ms.assetid: 62bdb1e7-ca45-42e6-bdf5-c48fb3ddb3fc
keywords:
- 不完全な構成は、WDK の多機能デバイスを登録します。
- システム提供の多機能バス ドライバー WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e438eccd6028f59a8a8de144ea4351dedf16ce4
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350119"
---
# <a name="supporting-pc-cards-that-have-incomplete-configuration-registers"></a>不完全な構成レジスターを持つ PC カードのサポート





多機能 16 ビット PC カード デバイスでは、各関数のレジスタを構成することはない場合、このようなデバイスの製造元は、システム提供の多機能バス ドライバー (mf.sys) を使用できますが、個々 の関数のカスタムの INF ファイルとサポートを提供する必要があります。

NT ベースのプラットフォーム上のようなデバイスの製造元は、次のシステム提供のコンポーネントを使用できます。

-   多機能デバイス関数ドライバー。 (システム提供の)

    デバイスのカスタム INF では、デバイスの機能のドライバーとして mf.sys を指定する必要があります。 システム提供の mf.sys ドライバーにし、デバイスの機能が列挙されます。

    参照してください[System-Supplied 多機能バス ドライバーを使用して](using-the-system-supplied-multifunction-bus-driver.md)詳細については、システム提供の mf.sys ドライバーを使用します。

このようなデバイスの製造元は、次で提供する必要があります。

-   多機能デバイスのカスタム INF ファイルです。 (ベンダーから提供された)

    仕入先には、多機能のバス ドライバーとして mf.sys を指定し、(とその関連付けられている GUID として devguid.h で定義されている)、「多機能」クラスを指定し、不足している構成の登録情報を提供多機能 INF ファイルを指定する必要があります。 さらに、このセクションで後述する情報も参照してください。

-   デバイスの各関数の関数の PnP ドライバー。 (ベンダーから提供された)

    多機能バス ドライバーでは、多機能のセマンティクスを処理するため、関数ドライバーは、関数が個々 のデバイスとしてパッケージ化するときに使用される同じドライバーを指定できます。

-   各関数の場合、デバイスの INF ファイル。 (ベンダーから提供された)

    INF ファイルには、関数が個々 のデバイスとしてパッケージ化するときに使用される同じファイルを指定できます。 INF ファイルでは、多機能の特殊なセマンティクスは必要ありません。

このようなデバイスのベンダーから提供されたカスタム INF を指定する必要があります。

-   デバイスのサービスとして mf.sys します。

    参照してください[System-Supplied 多機能バス ドライバーを使用して](using-the-system-supplied-multifunction-bus-driver.md)詳細についてはします。

-   多機能デバイスのリソース要件。

    リソース要件を指定する[ **INF DDInstall.LogConfigOverride セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547339)します。

-   各関数の場合、デバイスのハードウェア ID。

    内のハードウェア Id を指定する[ **INF DDInstall.HW セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547330)します。

-   各関数の場合、デバイスは、各子関数で必要な親のリソースを特定のリソース マップします。

    リソースは、INF でマップを指定*DDInstall*.**HW**セクション。 参照してください[多機能デバイスのリソースがマップを作成する](creating-resource-maps-for-a-multifunction-device.md)リソースの作成の詳細については、マップします。

INF では、上書きの構成、INF に存在する場合は、PnP マネージャーは、デバイスから、デバイスのリソース要件を使用しないために、デバイスで指定されたすべてのリソース要件を再確認する必要があります。

このようなデバイスの構成オプションの登録をプログラムすることを使用して、 **PcCardConfig**単一関数のデバイスのプログラミングのようなエントリです。 **PcCardConfig**エントリには、デバイス全体に適用される情報が含まれています。 **PcCardConfig**にエントリが記載されている[ **INF LogConfig ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547448)します。

指定するときに、 **PcCardConfig**の多機能デバイスの形式のエントリ、 *ConfigIndex*単一関数のデバイスに対して定義されているのと同じです。 単一関数の PC カードの構成の登録には、そのデバイスの属性で定義されているリソースのセットへのインデックスが含まれています。 このディレクティブは、構成オプションのレジスタのインデックスに基づく形式を使用する特定の多機能デバイスにも使用できます。

次の例では、そのバス ドライバーに mf.sys を使用し、構成が不完全なレジスタが多機能デバイスをインストールするため、INF ファイルを示します。

```cpp
; MFSupra.inf
; This file installs the Supra Dual 56K modem
; Copyright 1999 Microsoft Corporation

[version]
Signature  = "$Windows NT$"
provider   = %MSFT%
Class      = MultiFunction              ; system-defined class
ClassGUID  = {4d36e971-e325-11ce-bfc1-08002be10318}

[ControlFlags]
ExcludeFromSelect=*SUP2440  ; don't include PnP devices in lists of
                            ; devices to be manually installed

[Manufacturer]
%M_Supra% = Supra

[Supra]
%Supra1% = Sup2231GoCard.mf, *SUP2440 

[Sup2231GoCard.mf.NT]
Include = mf.inf           ; specify that this device needs mf.sys
Needs = MFINSTALL.mf

[Sup2231GoCard.mf.NT.HW]
AddReg=Sup2231.mf.RegHW

[Sup2231.mf.RegHW]   
HKR, Child0000, HardwareID,  ,  MF\Shotgun_DEV0  ;modem1
HKR,Child0000,ResourceMap,1,00,02
HKR, Child0001, HardwareID,  ,  MF\Shotgun_DEV1  ;modem2
HKR,Child0001,ResourceMap,1,01,02

[Sup2231GoCard.mf.NT.Services]   
Include = mf.inf
Needs = MFINSTALL.mf.Services

[Sup2231GoCard.mf.NT.LogConfigOverride]   
LogConfig = Sup223x.mf.Override0, Sup223x.mf.Override1, \
 Sup223x.mf.Override2, Sup223x.mf.Override3

[Sup223x.mf.Override0]
ConfigPriority = NORMAL
IOConfig     = 2F8-2FF                  ; Com2
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ    
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 59(W)                    ; ConfigIndex

[Sup223x.mf.Override1]
ConfigPriority = NORMAL
IOConfig     = 3E8-3EF                  ; Com3
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ    
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 69(W)                    ; ConfigIndex

[Sup223x.mf.Override2]
ConfigPriority = NORMAL
IOConfig     = 2E8-2EF                  ; Com4
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ    
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 79(W)                    ; ConfigIndex

[Sup223x.mf.Override3]
ConfigPriority = NORMAL
IOConfig     = 3F8-3FF                  ; Com1
IOConfig     = 20@100-FFFF%FFE0         ; NIC I/O
IRQConfig    = 3,4,5,7,9,10,11,12,15          ; IRQ
MemConfig    = 1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor
PCCardConfig = 49(W)                    ; ConfigIndex

[strings]
MSFT = "Microsoft"
M_Supra = "Supra"
Supra1 = "Supra Dual 56K modem"
```

コピー ID とリソースの情報をレジストリに子関数の前に示したような INF します。 Mf.sys ドライバーでは、デバイスの子の機能を列挙したときに、レジストリから情報を取得します。









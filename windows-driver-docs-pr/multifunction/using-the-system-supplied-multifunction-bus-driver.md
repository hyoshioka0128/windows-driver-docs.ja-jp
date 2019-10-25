---
title: システム提供の多機能バス ドライバーの使用
description: システム提供の多機能バス ドライバーの使用
ms.assetid: 75fe659d-5311-4bc6-adfb-fd608e10c718
keywords:
- 多機能デバイス WDK、システム提供のバスドライバー
- システムで提供される多機能バスドライバー WDK
- mf
- 機能デバイスオブジェクト WDK 多機能デバイス
- FDOs WDK 多機能デバイス
- 物理デバイスオブジェクト WDK 多機能デバイス
- PDOs WDK 多機能デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28c2043a74e8a5f801814a6ca5d5ace827f76484
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838287"
---
# <a name="using-the-system-supplied-multifunction-bus-driver"></a>システム提供の多機能バス ドライバーの使用





デバイスの基礎となるバスが PC カードなどの多機能バス規格をサポートしている場合、NT ベースのプラットフォーム上の多機能なデバイスのベンダーは、システムによって提供される多機能バスドライバー (mf) を使用してデバイスをサポートできます。

Mf バスドライバーは、関数間のデバイス関数の PnP 列挙と判別リソース (i/o ポートや Irq など) を処理します。 Mf ドライバーは、子機能の電源管理を、親の多機能なデバイスの電源管理によって処理します。

Mf を使用するには、多機能デバイスが次の要件を満たしている必要があります。

-   デバイスの基盤となるバスには、多機能な標準が必要です。

-   [**デバイス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の子関数は同一である必要があり、親デバイスの機能と一致している必要があります。 子関数 ([**IRP\_\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)) のデバイス機能に対してクエリを実行すると、mf ドライバーは親デバイスのデバイス機能を報告します。

-   Pcmcia などの多機能なデバイスが常駐するバスのドライバーは、すべての Irp\_を処理する必要があります。この場合、\_構成と Irp\_[ **\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config) [ **\_構成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)要求を書き込むことができます。 Mf ドライバーは、これらの Irp を親バスドライバーに渡します。

-   これらの関数は、独立している必要があります。開始順序の依存関係を持つことはできません。1つの関数のリソース要件は、別の関数のリソースという観点では表現できません (たとえば、function1 は i/o ポート X を使用し、function2 は portX + 200 を使用します)。また、各関数は、別の関数と同じドライバーによって処理される場合でも、個別のデバイスとして動作できる必要があります。

Mf を使用するために、ベンダは、デバイスのドライバーとして mf を指定する、多機能なデバイス用の INF を提供します。 デバイスが、基盤となるバスの多機能標準に完全かつ正確に準拠している場合、このようなデバイスのベンダーはシステムが提供する mf を使用できます。 デバイスが標準に完全に準拠していない場合、ベンダーはカスタム INF を提供する必要があります。

どちらの場合も、ベンダーは、デバイス上の個々の機能に対してドライバーと INF ファイルを提供します。

次のカスタム多機能 INF のスケルトンは、mf を多機能デバイスのドライバーとして指定するために必要な構文を示しています。

```cpp
[Version]
Signature = "$Windows NT$"
; ...
Class = Multifunction   ; the system-defined class for MF devices
ClassGUID  = {4d36e971-e325-11ce-bfc1-08002be10318} ; GUID for MF
; ...
; ...
[ControlFlags]
ExcludeFromSelect = *   ; don't include PnP devices in a displayed list of 
                        ; devices available for manual installation
[Manufacturer]
; ...
; ...
[ModelsSection]         ; models section
; ...
; ...
[DDInstall.NT]          ; install section
Include = mf.inf        ; specify that this device requires mf.sys
Needs = MFINSTALL.mf
; ...
 
[DDinstall.NT.Services]
Include = mf.inf
Needs = MFINSTALL.mf.Services

[DDInstall.NT.HW]
AddReg=DDInstall.RegHW
 
[DDInstall.RegHW]
; put entries with child function hardware IDs here
; ...
 
; put override sections here...
; ...
 
[Strings]
; ...
```

LAN/モデム PC カードデバイスの組み合わせを検討してください。 特別な機能をサポートしていない場合、このようなデバイスは、PCMCIA バスドライバーによって1つのモデムデバイスとして報告されることがあります。 多機能な INF と mf bus ドライバーの追加のサポートにより、デバイスの両方の機能が列挙されます。 次の図は、このような多機能サポートを備えたコンボ PC カード用に作成されるデバイススタックの例を示しています。

![mf によって列挙された多機能デバイスのデバイススタックを示す図](images/mf-layers.png)

上の図に示すように、多機能デバイスが存在するバスのドライバーは、1つのデバイスを列挙します。 多機能 INF ファイルのハードウェア ID を使用すると、PnP マネージャーは、そのデバイスの関数ドライバーとして mf を読み込みます。 Mf バスドライバーは、2つの子デバイス (LAN デバイスとモデム) を列挙します。

PnP マネージャーは、デバイスごとにデバイススタックが作成されるまで、一般的なデバイス、INF ファイルの検索、適切なドライバーの読み込み、AddDevice ルーチンの呼び出しなど、各子デバイスを扱います。 判別バスドライバーは、子デバイスのリソースを管理し、デバイスの他の機能面を管理します。 多機能カードのベンダーは、複数の機能 (LAN およびモデム) 用の関数ドライバーと Inf を、独立したデバイスであるかのように提供します。

この図では、関数ドライバーと親バスドライバー、およびそれらに関連付けられている FDOs と PDOs に焦点を当てています。 単純化するために、すべてのフィルタードライバー (およびフィルター DOs) は省略されています。

 

 





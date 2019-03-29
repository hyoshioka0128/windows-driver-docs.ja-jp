---
title: システム提供の多機能バス ドライバーの使用
description: システム提供の多機能バス ドライバーの使用
ms.assetid: 75fe659d-5311-4bc6-adfb-fd608e10c718
keywords:
- 多機能デバイス WDK、システム提供のバス ドライバー
- システム提供の多機能バス ドライバー WDK
- mf.sys
- 機能のデバイス オブジェクトの WDK 多機能デバイス
- Fdo WDK 多機能デバイス
- 物理デバイス オブジェクトの WDK 多機能デバイス
- Pdo WDK 多機能デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94f9cbdb5f0fd1e6eed1785b5149344b804f0793
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349736"
---
# <a name="using-the-system-supplied-multifunction-bus-driver"></a>システム提供の多機能バス ドライバーの使用





デバイスの基になるバスは、PC カードなどの多機能 bus 標準をサポートしている場合、NT ベースのプラットフォーム上の多機能デバイスのベンダーは、デバイスをサポートするシステム提供の多機能バス ドライバー (mf.sys) を使用できます。

Mf.sys バス ドライバーのハンドルは PnP デバイス関数の列挙と、関数の間での I/O ポートと Irq などのリソースを介しします。 Mf.sys ドライバーは、電源親多機能デバイスを管理して、子関数の電源管理を処理します。

Mf.sys を使用するには、多機能デバイスは、次の要件を満たす必要があります。

-   デバイスの基になるバスには、多機能の標準が必要です。

-   [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)関数、子のと同じである必要があり、親デバイスのものと一致する必要があります。 子関数のデバイス機能にクエリされるときに ([**IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664))、mf.sys ドライバーのデバイス機能の報告親となるデバイス。

-   いずれかの多機能デバイスが存在するなど pcmcia.sys、バス ドライバーが処理する必要があります[ **IRP\_MN\_読み取り\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551727)と[**IRP\_MN\_書き込み\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551769)要求。 Mf.sys ドライバーは、親のバス ドライバーにこれらの Irp を渡すのみです。

-   関数は、独立系である必要があります起動順序の依存関係を含めることはできません。(例、function1 は I/O ポート X と function2 はマッピング + 200); の別の関数のリソースの観点から、1 つの関数のリソース要件を表現できません。場合でも、別の関数と同じドライバーがサービスを提供、各関数が別のデバイスとして動作することがあります。

Mf.sys を使用するには、ベンダーは mf.sys をデバイスのドライバーとしてを指定する多機能デバイスに対して、INF を提供します。 デバイスを完全かつ正確に次の基になるバスの標準多機能に準拠している、このようなデバイスの製造元は、システム提供の mf.inf を使用できます。 デバイスが標準に完全に準拠していない場合、ベンダーは、カスタムの INF を提供する必要があります。

仕入先いずれの場合も、ドライバーと、デバイス上の個々 の関数の INF ファイルも提供します。

カスタムの多機能 INF の次のスケルトンは、多機能デバイスのドライバーとして mf.sys を指定するため、必要な構文を示しています。

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

LAN/モデム PC カード デバイスの組み合わせを検討してください。 特別な多機能サポートなしには、ようなデバイスを単一のモデム デバイスとしての PCMCIA バス ドライバーによって報告される可能性があります。 多機能 INF と mf.sys バス ドライバーの追加のサポートと共に、デバイスの両方の関数が列挙されます。 次の図は、このようなコンボ PC カードで必要な多機能サポートの作成されるサンプル デバイス スタックを示します。

![mf.sys によって列挙多機能デバイスのデバイス スタックを示す図](images/mf-layers.png)

上のドライバー、バスを上記の図に示すように、多機能デバイス上に存在する 1 つのデバイスを列挙します。 多機能 INF ファイルで、ハードウェア ID が原因で、デバイスの機能のドライバーとして mf.sys バス ドライバーを読み込む PnP マネージャー。 Mf.sys バス ドライバーでは、2 つの子デバイス、LAN デバイスおよびモデムを列挙します。

PnP マネージャーでは、各デバイスのデバイス スタックが作成されるまでなど、AddDevice ルーチンを呼び出すこと、適切なドライバーの読み込み、INF ファイルを検索するなど、一般的なデバイスでは、それぞれの子デバイスを扱います。 Mf.sys バス ドライバーでは、子デバイス用のリソースを調停およびデバイスの他の多機能の側面を管理します。 多機能カードの製造元と提供します関数ドライバーの Inf (LAN およびモデム) は、複数の関数の別のデバイスがあった場合と同様。

図は、関数のドライバーと親バス ドライバーおよび関連付けられている Fdo と Pdo について説明します。 フィルター ドライバー (とフィルター DOs) わかりやすくするため省略しています。

 

 





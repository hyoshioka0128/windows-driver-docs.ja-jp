---
title: カスタム ハードウェア ID および互換性 ID の使用
description: カスタム ハードウェア ID および互換性 ID の使用
ms.assetid: 4f0ae082-b601-4322-add8-63941c2bdad3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d85f3fdb8b529732d7f41dcf93c8f93cc2f049a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384769"
---
# <a name="using-custom-hardware-ids-and-compatible-ids"></a>カスタム ハードウェア ID および互換性 ID の使用


」の説明に従って[識別文字列](device-identification-strings.md)、新しいバス ドライバーがプラグ アンド プレイ (PnP) ハードウェア Id と互換性のある Id を使用する一般的な形式を次に示します。

```cpp
enumerator\enumerator-specific-device-ID 
```

各項目の意味は次のとおりです。

-   *列挙子*識別、*列挙子*(バス ドライバー) を検出し、PnP マネージャーにバス上の子デバイスを報告します。

-   *列挙子特定のデバイス ID*列挙子に固有のデバイス識別子を指定します。

構成またはバスの操作は、他のバスから非常に異なる場合と、バスのバス ドライバーが、バスの子デバイス誤って、または不適切なグループ分けされていないは子デバイスを使用することを確認する一意の列挙子名を使用する必要があります。他のバスをバス ドライバーによってこれらの列挙。 バス ドライバーには、PnP マネージャーにデバイスの識別文字列をレポートには、次の形式を使用する必要があります。

```cpp
bus-type-guid\vendor-specific-id
```

各項目の意味は次のとおりです。

-   *バスの種類-guid*バスを識別し、バスを識別するために使用される同じ GUID があります。 一意の GUID です。 」の説明に従って[バス ドライバーをインストールする](installing-a-new-bus-driver.md)、バス ドライバーへの応答内のデバイスのバスの種類を識別する、 [ **IRP_MN_QUERY_BUS_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)デバイスの要求。

-   *ベンダー固有の id*は通常、ベンダー、デバイス、サブシステム、リビジョン番号、および可能性があるその他のデバイス情報を識別するベンダ定義の形式です。 たとえば、形式がの形式をかかる場合があります*ベンダー*&*デバイス*&*サブシステム*&*リビジョン、* アンパサンド文字 ("&")、サブフィールドを取り出すためベンダー固有で、各サブフィールドの形式。 実際のデバイスの識別文字列の例については、次を参照してください。[識別文字列](device-identification-strings.md)します。

PnP マネージャー送信[ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)デバイスのデバイスの識別文字列を取得するバス ドライバーに要求します。 デバイスの識別文字列には、デバイス ID、デバイスのインスタンス ID をハードウェア Id の一覧、および互換性 Id の一覧が含まれます。 次の架空の例には、デバイス ID、ハードウェア Id の一覧、および互換性 Id の一覧が含まれます。 これらの例では、列挙子で指定された、*バスの種類-guid*サブフィールドで、"{17ed6609-9bc8-44ca-8548-abb79b13781b}"の GUID です。 形式、*ベンダー固有の id*フィールドは*ベンダー*&*デバイス*&*サブシステム*&*リビジョン*という、*ベンダー*サブフィールドは"ven_1"、*デバイス*サブフィールドは"dev_2"、*サブシステム*サブフィールド"subsys_3"は、および*リビジョン*サブフィールドは"rev_4"。

デバイス ID は、ハードウェア ID、デバイスの特定の説明を表すです。 次の例では、デバイス ID は、仕入先、デバイス、サブシステム、およびリビジョンを指定します。

```cpp
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&subsys_3&rev_4 
```

ハードウェア ID の一覧から順番に Id を指定しますから最も限定的固有性の高い。 次の一覧でデバイスの識別文字列として報告されますハードウェア ID を指定する場合、少なくとも、ベンダー、デバイス、およびサブシステム。 ほとんどの情報を含むハードウェア ID は、最初に表示されます。

```cpp
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&subsys_3&rev_4 
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&subsys_3 
```

少なくとも指定と、ベンダーやデバイスがない場合は、デバイスの識別文字列を互換性のある ID として報告するよう、以下のサブシステムを指定します。 ほとんどの情報を含む互換性 ID が最初に表示されます。

```cpp
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2&rev_4 
{17ed6609-9bc8-44ca-8548-abb79b13781b}\ven_1&dev_2
```

 

 






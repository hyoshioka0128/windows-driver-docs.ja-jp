---
title: カスタム ハードウェア ID および互換性 ID の使用
description: カスタム ハードウェア ID および互換性 ID の使用
ms.assetid: 4f0ae082-b601-4322-add8-63941c2bdad3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb25fe8bc5132877af5419a22d9fced8b579ad5
ms.sourcegitcommit: 1983d65315876b5b3783632f3a3395b287d15b86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289474"
---
# <a name="using-custom-hardware-ids-and-compatible-ids"></a>カスタム ハードウェア ID および互換性 ID の使用


「[デバイス Id 文字列](device-identification-strings.md)」で説明されているように、新しいバスドライバーがプラグアンドプレイ (PnP) ハードウェア id と互換性 id に対して使用する一般的な形式を次に示します。

```cpp
enumerator\enumerator-specific-device-ID 
```

各値の説明:

-   *列挙子*は、バス上の子デバイスを検出し、PnP マネージャーに報告するバスドライバーを識別します。

-   *列挙子-デバイス id*は、バスドライバーに固有のデバイス識別子です。

バスの構成または操作が他のバスと大きく異なる場合、バスのバスドライバーは一意の列挙子名を使用する必要があります。これにより、バスの子デバイスは、これらの他のバスのバスドライバーで列挙される子デバイスと誤って誤ってグループ化されないようにします。 バスドライバーは、デバイス id 文字列を PnP マネージャーに報告するために、次の形式を使用する必要があります。

```cpp
bus-type-guid\vendor-specific-id
```

各値の説明:

-   バス*タイプ guid*は、バスを識別する一意の guid であり、バスを識別するために使用されるものと同じ guid である必要があります。 「 [Bus ドライバーのインストール](installing-a-new-bus-driver.md)」で説明されているように、バスドライバーは、デバイスの[**IRP_MN_QUERY_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)要求に応答して、デバイスのバスの種類を識別します。

-   ベンダー*固有 id*は、通常、ベンダー、デバイス、サブシステム、リビジョン番号、およびその他のデバイス情報を識別するベンダー定義の形式です。 たとえば、という形式では、*ベンダー* & *デバイス* & *サブシステム*リビジョンの形式が使用されます & 。ここ*で*、アンパサンド文字 ("&") はフィールドを区切り、各サブフィールドの形式はベンダー固有です。 実際のデバイス識別文字列の例については、「[デバイス識別文字列](device-identification-strings.md)」を参照してください。

PnP マネージャーは[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)要求をバスドライバーに送信して、デバイスのデバイス id 文字列を取得します。 デバイス id 文字列には、デバイス ID、デバイスインスタンス ID、ハードウェア Id の一覧、および互換性 Id の一覧が含まれます。 次の架空の例には、デバイス ID、ハードウェア Id の一覧、および互換性 Id の一覧が含まれています。 これらの例では、列挙子は、GUID "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx-zzzz-xxxx-yyyyyyyyyyyy}" という*バスの種類*のサブフィールドによって指定されます。 ベンダー*固有 id*フィールドの形式は*ベンダー* & *デバイス* & *サブシステム* & *リビジョン*です。 *vendor*サブフィールドが "ven_1"、*デバイス*サブフィールドが "dev_2"、*サブシステムサブ*フィールドが "subsys_3"、*リビジョン*サブフィールドが "rev_4" です。

デバイス ID は、デバイスの最も具体的な説明であるハードウェア ID です。 次の例では、デバイス ID によって、ベンダー、デバイス、サブシステム、およびリビジョンが指定されています。

```cpp
{xxxxxxxx-yyyy-zzzz-xxxx-yyyyyyyyyyyy}\ven_1&dev_2&subsys_3&rev_4 
```

ハードウェア ID の一覧では、最も限定的なものから順に Id が指定されています。 次の一覧では、少なくともベンダー、デバイス、およびサブシステムが指定されている場合、デバイス id 文字列がハードウェア ID として報告されます。 最も多くの情報が含まれているハードウェア ID が最初に表示されます。

```cpp
{xxxxxxxx-yyyy-zzzz-xxxx-yyyyyyyyyyyy}\ven_1&dev_2&subsys_3&rev_4 
{xxxxxxxx-yyyy-zzzz-xxxx-yyyyyyyyyyyy}\ven_1&dev_2&subsys_3 
```

次の一覧では、少なくともベンダーとデバイス (位置1と 2) を指定している場合、デバイス id 文字列は互換性 ID として報告されますが、サブシステム (位置 3) は指定されません。 最も多くの情報を含む互換性のある ID が最初に表示されます。

```cpp
{xxxxxxxx-yyyy-zzzz-xxxx-yyyyyyyyyyyy}\ven_1&dev_2&rev_4 
{xxxxxxxx-yyyy-zzzz-xxxx-yyyyyyyyyyyy}\ven_1&dev_2
```

ドライバーがハードウェア ID を使用してインストールされている場合は、一致するデバイスのすべての機能を意味します。 ドライバーが互換性のある ID を使用してインストールされる場合は、少なくともデバイスを一致させる基本的な機能を意味します。ドライバーは、一般的なドライバーが多数のデバイスで動作できるように、互換性のある ID を使用する場合があります。 たとえば、Windows システムによって提供されるドライバーの多くは、互換性のある Id と一致します。 ハードウェア ID と一致するドライバーは、通常、少数のデバイスを対象としますが、すべての機能を提供します。




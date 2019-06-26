---
title: PPD 固有のインターフェイス
description: PPD 固有のインターフェイス
ms.assetid: 12d5baa2-4fd4-4eca-84c7-1ee168ee8259
keywords:
- PostScript プリンター ドライバー WDK の印刷、PPD 固有のインターフェイス
- Pscript WDK の印刷、PPD に固有のインターフェイス
- IPrintCoreUI2
- PPD ファイル WDK Pscript
- WDK Pscript PPD 固有のインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f7debc40ac377db31bcd9b5a328b4237cbe0248
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373804"
---
# <a name="ppd-specific-interface"></a>PPD 固有のインターフェイス





IPrintCoreUI2 COM インターフェイスのファイルです。 これらのメソッドの 6 つのではサポートされて、 [IPrintCorePS2 COM インターフェイス](iprintcoreps2-com-interface.md)します。 このセクションでは、これらのメソッドの PPD 固有の動作について説明します。

### <a name="iprintcoreui2-interface-ppd-methods"></a>IPrintCoreUI2 インターフェイス PPD メソッド

[**IPrintCoreUI2::EnumConstrainedOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2::EnumFeatures**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)

[**IPrintCoreUI2::EnumOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)

[**IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)

[**IPrintCoreUI2::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)

[**IPrintCoreUI2::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)

[**IPrintCoreUI2::SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2::WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

### <a name="iprintcoreps2-interface-ppd-methods"></a>IPrintCorePS2 インターフェイス PPD メソッド

[**IPrintCorePS2::EnumFeatures**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures)

[**IPrintCorePS2::EnumOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions)

[**IPrintCorePS2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptions)

[**IPrintCorePS2::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute)

[**IPrintCorePS2::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute)

[**IPrintCorePS2::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute)

このセクションを通じて、両方のインターフェイスのメンバーである任意のメソッドへの参照は、両方のメソッドに適用されます。 参照をたとえば、 **GetOptions**に適用されます**IPrintCoreUI2::GetOptions**でなく**IPrintCorePS2::GetOptions**します。

### <a name="ppd-feature-availability"></a>PPD 機能の可用性

このセクションでは、語句では「PPD 機能は現在使用できません」か、プリンターが、機能をサポートしていないか、機能の非-なし/False オプションは、現在インストール可能なオプションの設定によって制限されます。

たとえば、"双方向機能は現在使用できません"PPD のいずれかで指定されていないことを意味、 \***双方向**機能、キーワード、または\***双方向**キーワードの機能非-None オプションは、両面印刷ユニットがインストールされていないという事実によって現在制限されます。

 

 





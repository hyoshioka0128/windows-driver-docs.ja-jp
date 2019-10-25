---
title: PPD 固有のインターフェイス
description: PPD 固有のインターフェイス
ms.assetid: 12d5baa2-4fd4-4eca-84c7-1ee168ee8259
keywords:
- PostScript プリンタードライバー WDK 印刷、PPD 固有のインターフェイス
- Pscript WDK print、PPD 固有のインターフェイス
- IPrintCoreUI2
- PPD ファイル WDK Pscript
- PPD 固有のインターフェイス WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7eba7e61097e8b9ab34feb6a56a59344c2e405e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844663"
---
# <a name="ppd-specific-interface"></a>PPD 固有のインターフェイス





IPrintCoreUI2 COM インターフェイスファイル。 これらのメソッドの6つは、 [IPRINTCOREPS2 COM インターフェイス](iprintcoreps2-com-interface.md)でサポートされています。 このセクションでは、これらのメソッドの PPD 固有の動作について説明します。

### <a name="iprintcoreui2-interface-ppd-methods"></a>IPrintCoreUI2 Interface の PPD メソッド

[**IPrintCoreUI2::EnumConstrainedOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2:: EnumFeatures**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)

[**IPrintCoreUI2::EnumOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)

[**IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2:: GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)

[**IPrintCoreUI2:: GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)

[**IPrintCoreUI2::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)

[**IPrintCoreUI2::SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2:: WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

### <a name="iprintcoreps2-interface-ppd-methods"></a>IPrintCorePS2 Interface の PPD メソッド

[**IPrintCorePS2:: EnumFeatures**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures)

[**IPrintCorePS2::EnumOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions)

[**IPrintCorePS2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptions)

[**IPrintCorePS2:: GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute)

[**IPrintCorePS2:: GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute)

[**IPrintCorePS2::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute)

このセクション全体で、両方のインターフェイスのメンバーである任意のメソッドへの参照が両方のメソッドに適用されます。 たとえば、 **GetOptions**への参照は、 **IPrintCoreUI2:: GetOptions**と**IPrintCorePS2:: GetOptions**に適用されます。

### <a name="ppd-feature-availability"></a>PPD 機能の可用性

このセクションでは、"PPD 機能は現在使用できません" という語句は、プリンターが機能をサポートしていないこと、または機能の [なし]/[偽] オプションが現在インストール可能なオプションの設定によって制限されていることを意味します。

たとえば、"二重化機能は現在使用できません" という意味では、PPD で \***デュプレックス**機能のキーワードが指定されていないか、または \***二重**機能のキーワードの [なし] オプションが、現在のところ、両面印刷ユニットがインストールされていません。

 

 





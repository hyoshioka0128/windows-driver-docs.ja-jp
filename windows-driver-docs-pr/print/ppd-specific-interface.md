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
ms.openlocfilehash: 99db8f3645f569daff11cbc767fdd81a0585841a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389548"
---
# <a name="ppd-specific-interface"></a>PPD 固有のインターフェイス





IPrintCoreUI2 COM インターフェイスのファイルです。 これらのメソッドの 6 つのではサポートされて、 [IPrintCorePS2 COM インターフェイス](iprintcoreps2-com-interface.md)します。 このセクションでは、これらのメソッドの PPD 固有の動作について説明します。

### <a name="iprintcoreui2-interface-ppd-methods"></a>IPrintCoreUI2 インターフェイス PPD メソッド

[**IPrintCoreUI2::EnumConstrainedOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553045)

[**IPrintCoreUI2::EnumFeatures**](https://msdn.microsoft.com/library/windows/hardware/ff553050)

[**IPrintCoreUI2::EnumOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553052)

[**IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)

[**IPrintCoreUI2::GetFeatureAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553056)

[**IPrintCoreUI2::GetGlobalAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553059)

[**IPrintCoreUI2::GetOptionAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553064)

[**IPrintCoreUI2::SetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553081)

[**IPrintCoreUI2::WhyConstrained**](https://msdn.microsoft.com/library/windows/hardware/ff553087)

### <a name="iprintcoreps2-interface-ppd-methods"></a>IPrintCorePS2 インターフェイス PPD メソッド

[**IPrintCorePS2::EnumFeatures**](https://msdn.microsoft.com/library/windows/hardware/ff552990)

[**IPrintCorePS2::EnumOptions**](https://msdn.microsoft.com/library/windows/hardware/ff552996)

[**IPrintCorePS2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553019)

[**IPrintCorePS2::GetFeatureAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553006)

[**IPrintCorePS2::GetGlobalAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553009)

[**IPrintCorePS2::GetOptionAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553013)

このセクションを通じて、両方のインターフェイスのメンバーである任意のメソッドへの参照は、両方のメソッドに適用されます。 参照をたとえば、 **GetOptions**に適用されます**IPrintCoreUI2::GetOptions**でなく**IPrintCorePS2::GetOptions**します。

### <a name="ppd-feature-availability"></a>PPD 機能の可用性

このセクションでは、語句では「PPD 機能は現在使用できません」か、プリンターが、機能をサポートしていないか、機能の非-なし/False オプションは、現在インストール可能なオプションの設定によって制限されます。

たとえば、"双方向機能は現在使用できません"PPD のいずれかで指定されていないことを意味、 \***双方向**機能、キーワード、または\***双方向**キーワードの機能非-None オプションは、両面印刷ユニットがインストールされていないという事実によって現在制限されます。

 

 





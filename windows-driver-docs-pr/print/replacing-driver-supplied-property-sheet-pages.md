---
title: ドライバーによって提供されるプロパティシートページの置換
description: ドライバーによって提供されるプロパティシートページの置換
ms.assetid: b7f79841-f82c-4a60-9c2f-58772a65a5eb
keywords:
- ユーザーインターフェイスプラグイン WDK print、プロパティシートページ
- UI プラグイン WDK print、プロパティシートページ
- プロパティシートページの WDK 印刷
- プロパティシートのページの置換
- IPrintCoreUI2
- ドキュメント-固定プロパティの WDK 印刷
- プリンターの固定プロパティの WDK 印刷
- デバイス固定プロパティの WDK 印刷
- 固定プロパティの WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3b658b248f9280d1944179956fedd6a9cb9f9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840413"
---
# <a name="replacing-driver-supplied-property-sheet-pages"></a>ドライバーによって提供されるプロパティシートページの置換





[IPRINTCOREUI2 COM インターフェイス](iprintcoreui2-com-interface.md)には、windows XP 以降のバージョンの windows オペレーティングシステムで実行されている Pscript5 UI プラグインがコアドライバーの標準 UI ページを完全に置き換える場合に使用する必要がある4つのメソッドが用意されています。 (コアドライバーという用語は、Unidrv または Pscript5 プリンタードライバーを指します)。これらのメソッドは次のとおりです。

[**IPrintCoreUI2::EnumConstrainedOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2::SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2:: WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

これらのメソッドは、UI プラグインの[**Iprintoemui::D ocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)および[**Iprintoemui::D evicepropertysheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)メソッドとそのプロパティシートコールバックルーチンの実行中にのみサポートされます。 UI プラグインは、これらのメソッドをサポートして独自のユーザーインターフェイスを表示します。 サポートされていない場合、これらのメソッドは E\_NOTIMPL を返します。

コアドライバーでは、 [**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)と[**DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)の2つの状況で、独自のプロパティシートの UI が表示されます。 最初のメソッドは、ドキュメント (ドキュメントの固定プロパティ) のみに適用されるプロパティを表示します。2番目のメソッドは、デバイスに適用されるプロパティ (デバイスまたはプリンターの固定プロパティ) を表示します。

コアドライバーは、処理するプロパティシートの種類を記憶しています (したがって、モード--ドキュメントとプリンターの固定)。 コアドライバーは、UI インスタンス用に作成した構造体 ( [**Oemuiobj**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemuiobj)構造体) にその状態情報を保存します。 コアドライバーは、プラグインのインターフェイスメソッドを呼び出すと、OEMUIOBJ 構造体へのポインターを渡します。これにより、プラグインが[**IPrintCoreUI2:: EnumConstrainedOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions), [**IPrintCoreUI2:: GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)からコアドライバーにコールバックするときに、 [**IPrintCoreUI2:: SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)または[**IPrintCoreUI2:: WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)。これらのメソッドは、ポインターをコアドライバーに渡してから、モードを決定できるようにします。

**IPrintCoreUI2:: EnumConstrainedOptions**、 **IPrintCoreUI2:: SetOptions**、および**IPrintCoreUI2:: Whyconstrained**の場合、 **Iprintoemui::D ocumentpropertysheets の実行中に、ドキュメント固定機能のみがサポートされます。** または、そのプロパティシートのコールバックルーチンと、 **Iprintoemui ui**の実行中にサポートされるのは、evicepropertysheets またはそのプロパティシートのコールバックルーチンだけです。 **IPrintCoreUI2:: SetOptions**の場合、現在の固定モードに一致しない持続性を持つすべての機能は無視する必要があります。 **IPrintCoreUI2:: EnumConstrainedOptions**または**IPrintCoreUI2:: whyconstrained**が、持続性が現在の固定モードと一致しないフィーチャーに対して呼び出された場合、メソッドは E\_invalidarg を返す必要があります。

[**IPrintCoreUI2:: GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)の場合、ドキュメント固定モード ( [**Iprintoemui::D ocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)またはそのプロパティシートのコールバックルーチンが実行されている場合) では、ドキュメントとプリンターの両方の機能がサポートされますが、プリンター固定機能は、プリンターの固定モードでサポートされています ( [**Iprintoemui::D evicepropertysheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets) 、またはそのプロパティシートのコールバックルーチンが実行されている場合)。

 

 





---
title: ドライバー提供のプロパティ シート ページを置換する
description: ドライバー提供のプロパティ シート ページを置換する
ms.assetid: b7f79841-f82c-4a60-9c2f-58772a65a5eb
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、プロパティ シート ページ
- UI プラグインを WDK の印刷、プロパティ シートのページ
- WDK プロパティ シートのページを印刷します。
- プロパティ シートのページを置き換える
- IPrintCoreUI2
- WDK ドキュメント固定のプロパティを印刷します。
- 印刷するプリンター スティッキー プロパティ WDK
- デバイス スティッキー プロパティ WDK を印刷します。
- 固定プロパティ WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5526d38fee79e98186e4cbc1d21a2a72d7879fd6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383525"
---
# <a name="replacing-driver-supplied-property-sheet-pages"></a>ドライバー提供のプロパティ シート ページを置換する





[IPrintCoreUI2 COM インターフェイス](iprintcoreui2-com-interface.md)core ドライバーの標準の UI ページを完全に置換する予定の場合に使用する必要があります、Pscript5 UI プラグインで実行されている Windows XP 以降のバージョンの Windows オペレーティング システムの 4 つのメソッドを提供します。 (用語 core ドライバーは、Unidrv または Pscript5 のプリンター ドライバーを参照)。これらのメソッドは次のとおりです。

[**IPrintCoreUI2::EnumConstrainedOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2::SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2::WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

これらのメソッドが、UI プラグインの実行中にのみサポートされている[ **IPrintOemUI::DocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)と[ **IPrintOemUI::DevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)メソッドとそのプロパティ シートのコールバック ルーチン。 プラグインの UI には、独自のユーザー インターフェイスを表示するこれらのメソッドがサポートしています。 サポートされていないときにこれらのメソッドが返す E\_NOTIMPL します。

コア ドライバーの - 2 つの状況では、独自プロパティ シートの UI を表示する[ **DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)、および[ **DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets). 最初のメソッドは、ドキュメント (固定ドキュメントのプロパティ) にのみ適用されるプロパティを表示、メソッドを 2 番目には、デバイス (デバイスまたはプリンターの固定プロパティ) に適用されるプロパティを表示します。

コア ドライバーには、プロパティ シートの処理 (およびそのため、固定ドキュメントまたはプリンター スティッキー--モード) の種類が記録されています。 コア ドライバーが、構造にその状態情報を保存します (、 [ **OEMUIOBJ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printoem/ns-printoem-_oemuiobj)構造) の UI のインスタンスが作成されます。 コア ドライバー、プラグインのインターフェイス メソッドを呼び出すと OEMUIOBJ 構造体にポインターを渡すようにときに、プラグイン呼び出しは、中核となるドライバーから[ **IPrintCoreUI2::EnumConstrainedOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)、 [ **IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)、 [ **IPrintCoreUI2::SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)、または[ **IPrintCoreUI2::WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)、これらのメソッドは、モードを確認することでは、そのコア ドライバーにポインターを渡します。

**IPrintCoreUI2::EnumConstrainedOptions**、 **IPrintCoreUI2::SetOptions**、および**IPrintCoreUI2::WhyConstrained**、固定ドキュメントの機能のみ実行中にサポートされている**IPrintOemUI::DocumentPropertySheets**またはそのプロパティ シートのコールバック ルーチンとのみプリンター固定機能の実行中にサポート**IPrintOemUI::DevicePropertySheets**またはそのプロパティ シートのコールバック ルーチン。 **IPrintCoreUI2::SetOptions**が持続性が現在の固定モードと一致しない任意の機能を無視する必要があります。 ときにいずれか**IPrintCoreUI2::EnumConstrainedOptions**または**IPrintCoreUI2::WhyConstrained**が持続性と一致しません、現在の固定モード、メソッドが返す機能が呼び出されると E\_INVALIDARG します。

[ **IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)、固定ドキュメント モードでは、固定ドキュメントとプリンター付箋の両方の機能がサポートされて (つまり、 [ **IPrintOemUI::DocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)またはそのプロパティ シートのコールバック ルーチンが実行中)、プリンター固定モードでのみプリンター固定機能がサポートされていますが、(場合[ **IPrintOemUI::DevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)またはそのプロパティ シートのコールバック ルーチンが実行中)。

 

 





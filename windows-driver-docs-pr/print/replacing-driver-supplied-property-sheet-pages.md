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
ms.openlocfilehash: 4d7bc30e52dcbfc099bd0ebc754cfa33c99055ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382578"
---
# <a name="replacing-driver-supplied-property-sheet-pages"></a>ドライバー提供のプロパティ シート ページを置換する





[IPrintCoreUI2 COM インターフェイス](iprintcoreui2-com-interface.md)core ドライバーの標準の UI ページを完全に置換する予定の場合に使用する必要があります、Pscript5 UI プラグインで実行されている Windows XP 以降のバージョンの Windows オペレーティング システムの 4 つのメソッドを提供します。 (用語 core ドライバーは、Unidrv または Pscript5 のプリンター ドライバーを参照)。これらのメソッドは次のとおりです。

[**IPrintCoreUI2::EnumConstrainedOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553045)

[**IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)

[**IPrintCoreUI2::SetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553081)

[**IPrintCoreUI2::WhyConstrained**](https://msdn.microsoft.com/library/windows/hardware/ff553087)

これらのメソッドが、UI プラグインの実行中にのみサポートされている[ **IPrintOemUI::DocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554173)と[ **IPrintOemUI::DevicePropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff554165)メソッドとそのプロパティ シートのコールバック ルーチン。 プラグインの UI には、独自のユーザー インターフェイスを表示するこれらのメソッドがサポートしています。 サポートされていないときにこれらのメソッドが返す E\_NOTIMPL します。

コア ドライバーの - 2 つの状況では、独自プロパティ シートの UI を表示する[ **DrvDocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548548)、および[ **DrvDevicePropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548542). 最初のメソッドは、ドキュメント (固定ドキュメントのプロパティ) にのみ適用されるプロパティを表示、メソッドを 2 番目には、デバイス (デバイスまたはプリンターの固定プロパティ) に適用されるプロパティを表示します。

コア ドライバーには、プロパティ シートの処理 (およびそのため、固定ドキュメントまたはプリンター スティッキー--モード) の種類が記録されています。 コア ドライバーが、構造にその状態情報を保存します (、 [ **OEMUIOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff559571)構造) の UI のインスタンスが作成されます。 コア ドライバー、プラグインのインターフェイス メソッドを呼び出すと OEMUIOBJ 構造体にポインターを渡すようにときに、プラグイン呼び出しは、中核となるドライバーから[ **IPrintCoreUI2::EnumConstrainedOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff553045)、 [ **IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)、 [ **IPrintCoreUI2::SetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553081)、または[ **IPrintCoreUI2::WhyConstrained**](https://msdn.microsoft.com/library/windows/hardware/ff553087)、これらのメソッドは、モードを確認することでは、そのコア ドライバーにポインターを渡します。

**IPrintCoreUI2::EnumConstrainedOptions**、 **IPrintCoreUI2::SetOptions**、および**IPrintCoreUI2::WhyConstrained**、固定ドキュメントの機能のみ実行中にサポートされている**IPrintOemUI::DocumentPropertySheets**またはそのプロパティ シートのコールバック ルーチンとのみプリンター固定機能の実行中にサポート**IPrintOemUI::DevicePropertySheets**またはそのプロパティ シートのコールバック ルーチン。 **IPrintCoreUI2::SetOptions**が持続性が現在の固定モードと一致しない任意の機能を無視する必要があります。 ときにいずれか**IPrintCoreUI2::EnumConstrainedOptions**または**IPrintCoreUI2::WhyConstrained**が持続性と一致しません、現在の固定モード、メソッドが返す機能が呼び出されると E\_INVALIDARG します。

[ **IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)、固定ドキュメント モードでは、固定ドキュメントとプリンター付箋の両方の機能がサポートされて (つまり、 [ **IPrintOemUI::DocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554173)またはそのプロパティ シートのコールバック ルーチンが実行中)、プリンター固定モードでのみプリンター固定機能がサポートされていますが、(場合[ **IPrintOemUI::DevicePropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff554165)またはそのプロパティ シートのコールバック ルーチンが実行中)。

 

 





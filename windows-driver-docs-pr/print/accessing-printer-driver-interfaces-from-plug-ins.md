---
title: プラグインからプリンター ドライバー インターフェイスにアクセスする
description: プラグインからプリンター ドライバー インターフェイスにアクセスする
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM インターフェイスの WDK 印刷へのアクセスのプリンターのドライバー インターフェイスします。
- プラグインを WDK を印刷するインターフェイスへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355a168f9e9b5ad377c31875ff2d5f44d544c1df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385412"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>プラグインからプリンター ドライバー インターフェイスにアクセスする





場合、ドライバーによって提供されるに属しているプラグイン呼び出しメソッド[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)、 [IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)の COM インターフェイスをそのインターフェイスを取得する必要があります次のように、ドライバーからのポインター。

1.  IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemPS、または IPrintOemPS2 インターフェイスの PublishDriverInterface メソッドは、プラグインの場合に実装する必要があります。

2.  (Unidrv または Pscript5) ドライバーがプラグの PublishDriverInterface メソッドを呼び出すと、IPrintOemDriverUI へのポインターを提供[IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インスタンスの IUnknown インターフェイス。

3.  プラグインする必要がありますを使用して、IUnknown インターフェイス ポインター呼び出す iunknown::queryinterface の目的のバージョンを表すインターフェイス識別子を指定する、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス。 (詳細については、次を参照してください[プリンター ドライバーのインターフェイス識別子](interface-identifiers-for-printer-drivers.md)。)。

4.  QueryInterface がへのポインターを返します、プラグイン、ドライバーでサポートされているインターフェイスのバージョンを表すインターフェイス識別子を指定する場合、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス。 ドライバーは、その前に、インターフェイスの AddRef メソッド (Windows SDK のドキュメントで説明) を呼び出すプラグインにインターフェイス ポインターを返します。 インターフェイス メソッドの呼び出しに後で使用するには、このポインターは、プラグインの場合に保存する必要があります。

5.  ときに、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス ポインターが不要になった、プラグインは、インターフェイスのメソッド (Windows SDK のドキュメントで説明) を呼び出す必要があります。

新しい Windows Vista を使用するには、プラグインの[IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)または[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)インターフェイスのサポートを追加するプラグインに合わせて**OEMGI\_GETREQUESTEDHELPERINTERFACES**でその[ **IPrintOemUI::GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-getinfo)、 [ **IPrintOemPS::GetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-getinfo)、または[ **IPrintOemUni::GetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-getinfo)メソッド。

 

 





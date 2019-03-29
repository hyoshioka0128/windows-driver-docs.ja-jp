---
title: プラグインからプリンター ドライバー インターフェイスにアクセスする
description: プラグインからプリンター ドライバー インターフェイスにアクセスする
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM インターフェイスの WDK 印刷へのアクセスのプリンターのドライバー インターフェイスします。
- プラグインを WDK を印刷するインターフェイスへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fd903fec5c4e4c8d8f5e90686adaac7e9152b64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579520"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>プラグインからプリンター ドライバー インターフェイスにアクセスする





場合、ドライバーによって提供されるに属しているプラグイン呼び出しメソッド[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)、 [IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)の COM インターフェイスをそのインターフェイスを取得する必要があります次のように、ドライバーからのポインター。

1.  IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemPS、または IPrintOemPS2 インターフェイスの PublishDriverInterface メソッドは、プラグインの場合に実装する必要があります。

2.  (Unidrv または Pscript5) ドライバーがプラグの PublishDriverInterface メソッドを呼び出すと、IPrintOemDriverUI へのポインターを提供[IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インスタンスの IUnknown インターフェイス。

3.  プラグインする必要がありますを使用して、IUnknown インターフェイス ポインター呼び出す iunknown::queryinterface の目的のバージョンを表すインターフェイス識別子を指定する、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス。 (詳細については、次を参照してください[プリンター ドライバーのインターフェイス識別子](interface-identifiers-for-printer-drivers.md)。)。

4.  QueryInterface がへのポインターを返します、プラグイン、ドライバーでサポートされているインターフェイスのバージョンを表すインターフェイス識別子を指定する場合、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス。 ドライバーは、その前に、インターフェイスの AddRef メソッド (Windows SDK のドキュメントで説明) を呼び出すプラグインにインターフェイス ポインターを返します。 インターフェイス メソッドの呼び出しに後で使用するには、このポインターは、プラグインの場合に保存する必要があります。

5.  ときに、 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス ポインターが不要になった、プラグインは、インターフェイスのメソッド (Windows SDK のドキュメントで説明) を呼び出す必要があります。

新しい Windows Vista を使用するには、プラグインの[IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)または[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)インターフェイスのサポートを追加するプラグインに合わせて**OEMGI\_GETREQUESTEDHELPERINTERFACES**でその[ **IPrintOemUI::GetInfo**](https://msdn.microsoft.com/library/windows/hardware/ff554178)、 [ **IPrintOemPS::GetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553221)、または[ **IPrintOemUni::GetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff554256)メソッド。

 

 





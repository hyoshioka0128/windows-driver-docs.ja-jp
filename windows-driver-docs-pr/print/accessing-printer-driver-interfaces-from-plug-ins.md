---
title: プラグインからプリンター ドライバー インターフェイスにアクセスする
description: プラグインからプリンター ドライバー インターフェイスにアクセスする
ms.assetid: 021ba789-99bd-4ab5-98fb-0d24ffd0ce25
keywords:
- COM インターフェイス WDK print、プリンタードライバーインターフェイスへのアクセス
- プラグイン WDK 印刷、インターフェイスへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c84acc734e3e73972eb540a96153282e96f010
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837567"
---
# <a name="accessing-printer-driver-interfaces-from-plug-ins"></a>プラグインからプリンター ドライバー インターフェイスにアクセスする





プラグインが、ドライバーによって提供される[Iprintoemdriverui](iprintoemdriverui-com-interface.md)、iprintcoreIPrintCoreUI2 [perp](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)、 [iprintcoreの peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)、 [](iprintcoreui2-com-interface.md)、 [Iprintoemdriverui](iprintoemdriveruni-com-interface.md)、 [iprintoemdriverui](iprintoemdriverps-com-interface.md)、または[](iprintcoreps2-com-interface.md) COM インターフェイスに属するメソッドを呼び出した場合、次のようにドライバーからインターフェイスポインターを取得する必要があります。

1.  このプラグインは、IPrintOemUI、IPrintOemUI2、Iprintoemui、IPrintOemUni2、IPrintOemPS、または IPrintOemPS2 インターフェイスの PublishDriverInterface メソッドを実装する必要があります。

2.  ドライバー (Unidrv または Pscript5) がプラグインの PublishDriverInterface メソッドを呼び出すと、IPrintOemDriverUI、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [iprintoemdriverui](iprintoemdriveruni-com-interface.md)、 [iprintoemdriverui](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md)へのポインターが提供されます。インスタンスの IUnknown インターフェイス。

3.  プラグインは、iunknown インターフェイスポインターを使用して IUnknown:: QueryInterface を呼び出す必要があります。このとき、必要なバージョンの[Iprintoemdriverui](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [iprintoemdriverui](iprintoemdriveruni-com-interface.md)を[表すインターフェイス識別子を指定します。IPrintOemDriverPS](iprintoemdriverps-com-interface.md)または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス。 (詳細については、「[プリンタードライバーのインターフェイス識別子](interface-identifiers-for-printer-drivers.md)」を参照してください)。

4.  このプラグインで、ドライバーでサポートされているインターフェイスバージョンを表すインターフェイス識別子が指定されている場合、QueryInterface は[Iprintoemdriverui](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [iprintoemdriverui](iprintoemdriveruni-com-interface.md)[にポインターを返します。IPrintOemDriverPS](iprintoemdriverps-com-interface.md)または[IPrintCorePS2](iprintcoreps2-com-interface.md)インターフェイス。 ドライバーは、インターフェイスポインターをプラグインに返す前に、(Windows SDK のドキュメントで説明されている) インターフェイスの AddRef メソッドを呼び出すことに注意してください。 プラグインは、後でこのポインターを使用してインターフェイスメソッドを呼び出すために、このポインターを保存する必要があります。

5.  [Iprintoemdriverui](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、iprintoemdriverui、 [iprintoemdriverui](iprintoemdriverps-com-interface.md)、または[IPrintCorePS2](iprintcoreps2-com-interface.md) interface ポインターが不要になった場合、プラグインはインターフェイスの Release メソッド (Windows SDK のドキュメントで説明) を呼び出す必要があります。 [](iprintoemdriveruni-com-interface.md)

プラグインが新しい Windows Vista [IprintcoreIPrintOemPS Perps](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)インターフェイスまたは[Iprintcoreの peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)インターフェイスを使用できるようにするには、そのプラグインは、 [**iprintoemui:: GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo)、 [ **:: Getinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-getinfo)、または[**Iprintoemuni:: GETINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo)メソッドに**oemgi\_getrequestedの perinterface**のサポートを追加する必要があります。

 

 





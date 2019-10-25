---
title: プリンター ドライバーからプラグイン インターフェイスにアクセスする
description: プリンター ドライバーからプラグイン インターフェイスにアクセスする
ms.assetid: 639734c9-1aac-428c-bd5b-803607f1cf66
keywords:
- COM インターフェイス WDK 印刷、プラグインインターフェイスへのアクセス
- プラグイン WDK 印刷、インターフェイスへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32135bc1d5bffdb01806939580f37c663d934c9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837570"
---
# <a name="accessing-plug-in-interfaces-from-printer-drivers"></a>プリンター ドライバーからプラグイン インターフェイスにアクセスする





UI プラグインまたはレンダリングプラグインがインストールされている場合、プリンタードライバー (Unidrv または Pscript5) は次の呼び出しシーケンスを使用して、プラグインの[Iprintoemui](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [iprintoemui](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)にアクセスします。[IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md) COM インターフェイス:

1.  ドライバーは、LoadLibrary を呼び出してプラグイン DLL を読み込みます。これにより、プラグインの `DllMain` 関数が呼び出されます。

2.  ドライバーは、プラグインの `DllGetClassObject` 関数を呼び出します。この関数は、プラグインの IClassFactory インターフェイスへのポインターを返します。

3.  ドライバーは、IClassFactory インターフェイスの CreateInstance メソッドを呼び出します。これにより、 **\_IUnknown**のインターフェイス識別子が指定されます。これにより、メソッドは、プラグインの[Iprintoemui](iprintoemui-com-interface.md), [IPrintOemUI2](iprintoemui2-com-interface.md)[のインスタンスを作成します。IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)インターフェイスで、インスタンスの IUnknown インターフェイスへのポインターを返します。

4.  ドライバーは IUnknown インターフェイスの QueryInterface メソッドを呼び出して、 [Iprintoemui](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [iprintoemui](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[のバージョンを特定します。IPrintOemPS2](iprintoemps2-com-interface.md)インターフェイスは、プラグインによってサポートされており、サポートされているインターフェイスへのポインターを受け取ります。

5.  ドライバーは、プラグインインターフェイスの `PublishDriverInterface` メソッドを呼び出して、ドライバーの IPrintOemDriverUI、IPrintCoreUI2、Iprintoemdriverui、Iprintoemdriverui、または IPrintCorePS2 インターフェイスをプラグインで使用できるようにします。

6.  プラグインが[iprintoemuni](iprintoemuni-com-interface.md)インターフェイスを実装している場合、ドライバーは[**Iprintoemuni:: GetImplementedMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod)を呼び出して、実装されているインターフェイスメソッドを特定します。 同様に、プラグインで[IPrintOemUni2](iprintoemuni2-com-interface.md)インターフェイスが実装されている場合、ドライバーは同じ目的で**IPrintOemUni2:: GetImplementedMethod**を呼び出します。

 

 





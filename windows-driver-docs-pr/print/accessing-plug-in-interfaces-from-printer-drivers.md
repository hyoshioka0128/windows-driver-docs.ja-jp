---
title: プリンター ドライバーからプラグイン インターフェイスにアクセスする
description: プリンター ドライバーからプラグイン インターフェイスにアクセスする
ms.assetid: 639734c9-1aac-428c-bd5b-803607f1cf66
keywords:
- WDK の COM インターフェイスを印刷するプラグインのインターフェイスへのアクセス
- プラグインを WDK を印刷するインターフェイスへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdf595693082d49ad6be56c2d3ca80562b295b9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388725"
---
# <a name="accessing-plug-in-interfaces-from-printer-drivers"></a>プリンター ドライバーからプラグイン インターフェイスにアクセスする





場合、プラグインまたはレンダリングの UI プラグインがインストールされているプリンター ドライバー (Unidrv または Pscript5) を使用して次の呼び出しの順序、プラグインへのアクセスを取得する[IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)COM インターフェイス:

1.  ドライバーは、呼び出し時に、プラグインのプラグインの DLL を読み込む LoadLibrary を呼び出し`DllMain`関数。

2.  ドライバーは、プラグインの呼び出す`DllGetClassObject`プラグインの IClassFactory インターフェイス ポインターを返す関数。

3.  ドライバーは、インターフェイスの識別子を指定する IClassFactory インターフェイスの CreateInstance メソッドを呼び出します**IID\_IUnknown**、それが原因で、プラグインのインスタンスを作成するメソッド[。IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)インターフェイスし、インスタンスの IUnknown インターフェイスへのポインターを返します。

4.  ドライバーのバージョンを決定する IUnknown インターフェイスの QueryInterface メソッドを呼び出し、 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)を受信して、プラグインによってインターフェイスがサポートします。サポートされているインターフェイスへのポインター。

5.  プラグインのインターフェイスの呼び出し、ドライバー`PublishDriverInterface`ドライバーの IPrintOemDriverUI、IPrintCoreUI2、IPrintOemDriverUni、IPrintOemDriverPS、または IPrintCorePS2 インターフェイスをプラグインに使用できるようにするメソッド。

6.  プラグインが実装された場合、 [IPrintOemUni](iprintoemuni-com-interface.md)インターフェイス、ドライバー呼び出し[ **IPrintOemUni::GetImplementedMethod** ](https://msdn.microsoft.com/library/windows/hardware/ff554253)メソッドがあるインターフェイスを決定するには実装されています。 同様に、プラグインが実装された場合、 [IPrintOemUni2](iprintoemuni2-com-interface.md)インターフェイス、ドライバー呼び出し**IPrintOemUni2::GetImplementedMethod**を同じ目的。

 

 





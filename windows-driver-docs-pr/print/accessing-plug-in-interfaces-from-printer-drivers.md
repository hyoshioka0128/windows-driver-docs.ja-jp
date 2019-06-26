---
title: プリンター ドライバーからプラグイン インターフェイスにアクセスする
description: プリンター ドライバーからプラグイン インターフェイスにアクセスする
ms.assetid: 639734c9-1aac-428c-bd5b-803607f1cf66
keywords:
- WDK の COM インターフェイスを印刷するプラグインのインターフェイスへのアクセス
- プラグインを WDK を印刷するインターフェイスへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c04218eb15f8fd938cbeba4a393c07772b4b34c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369005"
---
# <a name="accessing-plug-in-interfaces-from-printer-drivers"></a>プリンター ドライバーからプラグイン インターフェイスにアクセスする





場合、プラグインまたはレンダリングの UI プラグインがインストールされているプリンター ドライバー (Unidrv または Pscript5) を使用して次の呼び出しの順序、プラグインへのアクセスを取得する[IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)COM インターフェイス:

1.  ドライバーは、呼び出し時に、プラグインのプラグインの DLL を読み込む LoadLibrary を呼び出し`DllMain`関数。

2.  ドライバーは、プラグインの呼び出す`DllGetClassObject`プラグインの IClassFactory インターフェイス ポインターを返す関数。

3.  ドライバーは、インターフェイスの識別子を指定する IClassFactory インターフェイスの CreateInstance メソッドを呼び出します**IID\_IUnknown**、それが原因で、プラグインのインスタンスを作成するメソッド[。IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)インターフェイスし、インスタンスの IUnknown インターフェイスへのポインターを返します。

4.  ドライバーのバージョンを決定する IUnknown インターフェイスの QueryInterface メソッドを呼び出し、 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)を受信して、プラグインによってインターフェイスがサポートします。サポートされているインターフェイスへのポインター。

5.  プラグインのインターフェイスの呼び出し、ドライバー`PublishDriverInterface`ドライバーの IPrintOemDriverUI、IPrintCoreUI2、IPrintOemDriverUni、IPrintOemDriverPS、または IPrintCorePS2 インターフェイスをプラグインに使用できるようにするメソッド。

6.  プラグインが実装された場合、 [IPrintOemUni](iprintoemuni-com-interface.md)インターフェイス、ドライバー呼び出し[ **IPrintOemUni::GetImplementedMethod** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod)メソッドがあるインターフェイスを決定するには実装されています。 同様に、プラグインが実装された場合、 [IPrintOemUni2](iprintoemuni2-com-interface.md)インターフェイス、ドライバー呼び出し**IPrintOemUni2::GetImplementedMethod**を同じ目的。

 

 





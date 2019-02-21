---
title: プラグインの作成
description: プラグインの作成
ms.assetid: 4e52c855-f2c6-49b5-ac79-96dcac785579
keywords:
- COM インターフェイスの WDK 印刷、プラグインを作成します。
- プラグインを WDK の印刷、作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f18a79765275c06b11f48d052131c7bd1dda2beb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552693"
---
# <a name="creating-the-plug-in"></a>プラグインの作成





すべてプリンターのドライバー プラグインでは、DllMain、DllGetClassObject、および DllCanUnloadNow 関数を定義する必要があります。 COM の IClassFactory インターフェイスとの 1 つも実装する必要があります、 [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md) COM インターフェイスです。

いずれかを作成するとき、[プラグインのユーザー インターフェイス](user-interface-plug-ins.md)または[プラグインでレンダリング](rendering-plug-ins.md)、基に、コード、 [UI プラグインのサンプル](sample-ui-plug-in.md)または[サンプル レンダリングプラグイン](sample-rendering-plug-ins.md)WDK で提供します。

プラグインのいずれかの種類を作成するには、次の操作を行う必要があります。

1.  (Windows SDK のドキュメントで説明) DllMain 関数を定義します。

    これは、すべての Win32 Dll のエントリ ポイントです。

2.  定義し、(Windows SDK のドキュメントで説明) DllGetClassObject 関数をエクスポートします。

    プリンター ドライバーでは、(Windows SDK のドキュメントで説明) IClassFactory インターフェイスの実装、プラグインへのアクセスを取得するには、この関数を呼び出します。 ドライバーは、DllGetClassObject を呼び出すと (prcomoem.h で定義されている) 次のクラス識別子のいずれかを指定します。

    CLSID\_OEMUI - UI プラグイン

    CLSID\_OEMRENDER - レンダリング プラグイン

    ドライバーでは、インターフェイスの識別子も指定します**IID\_IClassFactory**します。

    DllGetClassObject 関数は IClassFactory インターフェイスのインスタンスを作成し、サンプル コードに示すように、ポインターを返す必要があります。

3.  COM の IClassFactory インターフェイスを実装します。

    IClassFactory インターフェイスの CreateInstance メソッドでは、次の COM インターフェイスの 1 つのプラグインでは、実装のインスタンスを作成する必要があります。

    [IPrintOemUI](iprintoemui-com-interface.md)、 [IPrintOemUI2](iprintoemui2-com-interface.md)、 [IPrintOemUni](iprintoemuni-com-interface.md)、 [IPrintOemUni2](iprintoemuni2-com-interface.md)、 [IPrintOemUni3](iprintoemuni3-com-interface.md)、 [IPrintOemPS](iprintoemps-com-interface.md)、または[IPrintOemPS2](iprintoemps2-com-interface.md)

    CreateInstance メソッドの入力の 1 つは、インターフェイス識別子です。 ドライバーは、インターフェイスの識別子が CreateInstance を呼び出す**IID\_IUnknown**、(Windows SDK で説明します作成されたインスタンスの IUnknown インターフェイスへのポインターを返す必要がありますつまり CreateInstance メソッド。ドキュメント)、サンプル コードに示すようにします。

4.  いずれかのサンプル コードに示すように、標準の IUnknown インターフェイスを含む IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemUni3、IPrintOemPS、または IPrintOemPS2 COM インターフェイスを実装します。

    ドライバーによって呼び出される実装されたメソッドの最初は、(Windows SDK のドキュメントで説明)、IUnknown インターフェイスの QueryInterface メソッドです。 このメソッドは、のいずれかを受け取る、[プリンター ドライバーの識別子をインターフェイス](interface-identifiers-for-printer-drivers.md)入力引数として。 ドライバーは、プラグインによって、インターフェイスのバージョンがサポートされているかを判断して、サポートされているインターフェイスへのポインターを受信するメソッドを呼び出します。

5.  定義し、(Windows SDK のドキュメントで説明) DllCanUnloadNow 関数をエクスポートします。

    これで DllCanUnloadNow 関数が返す必要があります S\_了解のプラグインでの実装の IPrintOemUI、IPrintOemUI2、IPrintOemUni、IPrintOemUni2、IPrintOemUni3、IPrintOemPS、または IPrintOemPS2 COM インターフェイスのすべてのインスタンスがリリースされた場合。 S\_戻り値が [ok]、プラグインがアンロードされるドライバーを示します。

    プリンター ドライバーでは、プラグインの DLL をアンロードするときに、まずを呼び出すプラグの DllCanUnloadNow 関数に注意してください。 DllCanUnloadNow によって返される値に関係なく、プリンター ドライバーは、FreeLibrary 関数を呼び出すことでプラグインの DLL をアンロードします。 これは、ドライバーが読み込まれる前に、プラグインの DLL が読み込まれないようにします。

    プラグインの DLL がする必要があります (たとえば、プラグインの DLL を使用するスレッドの作成時に) 読み込む残っている場合、スレッドは、LoadLibrary 関数の呼び出しを使用して、DLL を読み込む必要があります。 スレッドが終了するには、DLL は、アドインをアンロードする FreeLibraryAndExitThread 関数を呼び出す必要があります。 LoadLibrary、単なるデクリメント、DLL の参照カウントを FreeLibrary へのドライバーの呼び出しがアンロードされるを防ぐ、スレッドが呼び出されて場合。 LoadLibrary、FreeLibrary、および FreeLibraryAndExitThread 関数は、Windows SDK のドキュメントで説明します。

 

 





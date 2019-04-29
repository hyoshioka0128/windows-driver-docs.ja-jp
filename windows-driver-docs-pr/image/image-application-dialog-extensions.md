---
title: イメージ アプリケーション ダイアログの拡張
description: イメージ アプリケーション ダイアログの拡張
ms.assetid: 4bb7d2f9-58c3-4cfa-aa6b-a4bd9335d2ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f163fcba553303c2f072be8b847074ab384d312
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384655"
---
# <a name="image-application-dialog-extensions"></a>イメージ アプリケーション ダイアログの拡張





WIA イメージのアプリケーションのダイアログ ボックスを拡張するための 3 つのメカニズムがあります。 次のようなクラスがあります。

-   アイコンが、デバイスに表示する必要がある任意の場所で、システム提供のアイコンの代わりに使用されるデバイスのアイコンを指定します。 これを行うには、実装、 [ **IWiaUIExtension::GetDeviceIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff545075)メソッド。

-   提供する[プロパティ シートの拡張機能](property-sheet-extensions.md)WIA 買収のコモン ダイアログ ボックスで、または Windows で高度な設定やデバイスのプロパティをユーザーが表示したときに表示されるシステム提供のプロパティ ページを拡張します。エクスプ ローラー。 これを行うには、実装、 **IShellExtInit**と**IShellPropSheetExt**インターフェイス (Microsoft Windows SDK のドキュメントを参照してください)。

-   呼び出しに応答に表示される、システム指定のダイアログ ボックスの完全な置き換えを提供する**IWiaItem::DeviceDlg** (Windows SDK のドキュメントを参照してください)。 これを行うには、実装、 [ **IWiaUIExtension::DeviceDialog** ](https://msdn.microsoft.com/library/windows/hardware/ff545069)メソッド。

このセクションの残りの部分に関する追加情報を格納する、 [IWiaUIExtension COM インターフェイス](iwiauiextension-com-interface.md)します。

 

 





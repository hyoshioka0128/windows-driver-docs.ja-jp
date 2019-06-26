---
title: イメージ アプリケーション ダイアログの拡張
description: イメージ アプリケーション ダイアログの拡張
ms.assetid: 4bb7d2f9-58c3-4cfa-aa6b-a4bd9335d2ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4acad15fb0dba025294369216ba9e40b55d5c95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363034"
---
# <a name="image-application-dialog-extensions"></a>イメージ アプリケーション ダイアログの拡張





WIA イメージのアプリケーションのダイアログ ボックスを拡張するための 3 つのメカニズムがあります。 次のようなクラスがあります。

-   アイコンが、デバイスに表示する必要がある任意の場所で、システム提供のアイコンの代わりに使用されるデバイスのアイコンを指定します。 これを行うには、実装、 [ **IWiaUIExtension::GetDeviceIcon** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))メソッド。

-   提供する[プロパティ シートの拡張機能](property-sheet-extensions.md)WIA 買収のコモン ダイアログ ボックスで、または Windows で高度な設定やデバイスのプロパティをユーザーが表示したときに表示されるシステム提供のプロパティ ページを拡張します。エクスプ ローラー。 これを行うには、実装、 **IShellExtInit**と**IShellPropSheetExt**インターフェイス (Microsoft Windows SDK のドキュメントを参照してください)。

-   呼び出しに応答に表示される、システム指定のダイアログ ボックスの完全な置き換えを提供する**IWiaItem::DeviceDlg** (Windows SDK のドキュメントを参照してください)。 これを行うには、実装、 [ **IWiaUIExtension::DeviceDialog** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))メソッド。

このセクションの残りの部分に関する追加情報を格納する、 [IWiaUIExtension COM インターフェイス](iwiauiextension-com-interface.md)します。

 

 





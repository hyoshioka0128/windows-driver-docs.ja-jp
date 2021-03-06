---
title: インターフェイスを公開する
description: インターフェイスを公開する
ms.assetid: 3beefaa0-58b9-459a-89e5-1d9d81e80519
keywords:
- IPrintCoreHelperPS
- IPrintCoreHelperUni
- IPrintCoreHelper
- ヘルパー インターフェイス WDK プリンター インターフェイス DLL
- 発行の WDK プリンター インターフェイス DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b86038d561b7dd22288af6249ec69baed5038b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384691"
---
# <a name="publishing-the-interfaces"></a>インターフェイスを公開する


プラグインには、通常、公開と呼ばれるメカニズムによって、core のドライバーの動作を実装するオブジェクトのインスタンスが表示されます。 [IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper)、 [IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)、および[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)ヘルパー インターフェイスが同じモデルでは、いくつかの小さな違いがありますを使用して公開します。

次の一覧は、ユーザー インターフェイス (UI) で公開され、Unidrv と Pscript5 の両方のモジュールを描画するオブジェクトの順序をまとめたものです。 4 つのモジュールごとに、リスト内の数は、オブジェクトがパブリッシュされるとという名前の COM インターフェイスは、オブジェクトを実装するインターフェイスを指定の順序を示します。

指定された任意のモジュールに、ドライバーにならないように、ポインターを保存し、呼び出すことによって発行されたオブジェクトの 1 つだけ、 **AddRef**そのオブジェクトのメソッド。 プラグインが返す必要があります、プラグインは、オブジェクトへの参照を格納後、S\_ok をクリックします。 コア ドライバーでは、発行インターフェイスは停止します。 このモデルは前の発行メカニズムから大きな違いではありません。

UI では、オブジェクトのパブリッシュ、 **IPrintOemUI**クラス識別子を持つ CLSID は、クラス インターフェイス\_OEMUI します。 パブリッシュされたオブジェクトのレンダリング コンテキストで、 **IPrintOemPS**または**IPrintOemUni**インターフェイス。

アスタリスクでマークされているオブジェクト (\*) は次の一覧に発行された、 **IPrintOemPrintTicketProvider**インターフェイス。

### <a href="" id="unidrv-ui-module-publishing-order"></a> Unidrv UI モジュールの順序を公開

1.  **IUnknown**と\* **IPrintCoreHelper**と**IPrintCoreHelperUni**

2.  **IUnknown**と**IPrintOemDriverUI**

### <a href="" id="unidrv-render-module-publishing-order"></a> Unidrv レンダー モジュールの順序を公開

1.  **IUnknown**と**IPrintCoreHelper**と**IPrintCoreHelperUni**

2.  **IUnknown**と**IPrintOemDriverUni**

### <a href="" id="pscript5-ui-module-publishing-order"></a> Pscript5 UI モジュールの順序を公開

1.  **IUnknown**と\* **IPrintCoreHelper**と**IPrintCoreHelperPS**

2.  **IUnknown**と**IPrintCoreUI2**

3.  **IUnknown**と**IPrintOemDriverUI**

### <a href="" id="pscript5-render-module-publishing-order"></a> Pscript5 レンダー モジュールの順序を公開

1.  **IUnknown**と**IPrintCoreHelper**と**IPrintCoreHelperPS**

2.  **IUnknown**と**IPrintCorePS2**

 

 





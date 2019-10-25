---
title: インターフェイスを公開する
description: インターフェイスを公開する
ms.assetid: 3beefaa0-58b9-459a-89e5-1d9d81e80519
keywords:
- Iprintcoreの Perps
- Iprintcoreの Peruni
- IPrintCoreHelper
- ヘルパーインターフェイス WDK プリンターインターフェイス DLL
- WDK プリンターインターフェイス DLL の発行
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2db3a1255d1316b0cba1797fcfebbba49a5d9710
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840415"
---
# <a name="publishing-the-interfaces"></a>インターフェイスを公開する


プラグインは通常、発行と呼ばれるメカニズムによってコアドライバーの動作を実装するオブジェクトのインスタンスを受け取ります。 [Iprintcorehelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)、 [iprintcorehelper perps](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)、および[Iprintcorehelper peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)ヘルパーインターフェイスは、この同じモデルを使用して公開されており、わずかな違いがあります。

次の一覧は、Unidrv と Pscript5 の両方について、ユーザーインターフェイス (UI) とレンダーモジュールでオブジェクトが発行される順序をまとめたものです。 4つのモジュールそれぞれについて、リストの番号はオブジェクトが発行される順序を示し、名前が付けられている COM インターフェイスは、オブジェクトが実装するインターフェイスを示します。

任意のモジュールで、ドライバーは、ポインターを保存し、そのオブジェクトに対して**AddRef**メソッドを呼び出すことによって、発行されたオブジェクトのうちの1つだけを保持する必要があります。 プラグインによってオブジェクトへの参照が格納された後、プラグインは S\_OK を返します。 コアドライバーは、発行インターフェイスを停止します。 このモデルは、以前の発行メカニズムとは大きく異なります。

UI コンテキストでは、オブジェクトはクラス id が CLSID\_クラスの**Iprintoemui**インターフェイスに発行されます。 レンダーコンテキストでは、オブジェクトは**IPrintOemPS**インターフェイスまたは**Iprintoemuni**インターフェイスに発行されます。

次の一覧のアスタリスク (\*) でマークされているオブジェクトは、 **IPrintOemPrintTicketProvider**インターフェイスに発行されます。

### <a href="" id="unidrv-ui-module-publishing-order"></a>Unidrv UI モジュールの発行順序

1.  **IUnknown**と \***Iprintcorehelper**と**iprintcorehelper uni**

2.  **IUnknown**および**Iprintoemdriverui**

### <a href="" id="unidrv-render-module-publishing-order"></a>Unidrv レンダーモジュールの公開順序

1.  **IUnknown**および**Iprintcorehelper**および**Iprintcorehelper peruni**

2.  **IUnknown**と**Iprintoemdriveruni**

### <a href="" id="pscript5-ui-module-publishing-order"></a>Pscript5 UI モジュールの発行順序

1.  **IUnknown**と \***Iprintcorehelper**と**iprintcorehelper ps**

2.  **IUnknown**と**IPrintCoreUI2**

3.  **IUnknown**および**Iprintoemdriverui**

### <a href="" id="pscript5-render-module-publishing-order"></a>Pscript5 Render モジュールの発行順序

1.  **IUnknown**および**Iprintcorehelper**と**iprintcorehelper ps**

2.  **IUnknown**と**IPrintCorePS2**

 

 





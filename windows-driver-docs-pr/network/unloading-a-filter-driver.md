---
title: フィルター ドライバーのアンロード
description: フィルター ドライバーのアンロード
ms.assetid: e7ef209f-ab61-4644-a641-2fef09023a24
keywords:
- フィルタードライバー WDK ネットワーク、アンロード
- NDIS フィルタードライバー WDK、アンロード
- フィルタードライバーのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a49602bb20d6c33e8104b84f2ef5be926f3ebc22
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843012"
---
# <a name="unloading-a-filter-driver"></a>フィルター ドライバーのアンロード





NDIS フィルタードライバーに関連付けられているドライバーオブジェクトは、 *Filterdriverunload*という[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンを指定します。 フィルタードライバーサービスが削除されたすべてのミニポートアダプターを使用すると、システムは*Filterdriverunload*ルーチンを呼び出すことができます。

[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)では、ドライバー固有のリソースを解放する必要があります。 フィルタードライバーによって作成されたすべてのデバイスオブジェクトを破棄する必要があります。 *Filterdriverunload*が返された後、システムはドライバーのアンロード操作を完了できます。

Unload 関数の機能はドライバーによって異なります。 一般的な規則として、 [*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)は、ドライバーの初期化中に実行された操作を元に戻す必要があります。 ドライバーの初期化の詳細については、「[フィルタードライバーの初期化](initializing-a-filter-driver.md)」を参照してください。

フィルタードライバーは、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)から[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)関数を呼び出す必要があります。 **NdisFDeregisterFilterDriver**は[*filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)を呼び出して、このフィルタードライバーに関連付けられている現在アタッチされているすべてのフィルターモジュールをデタッチします。

フィルタードライバーのアンロードの詳細については、「[ドライバースタックの停止](stopping-a-driver-stack.md)」を参照してください。

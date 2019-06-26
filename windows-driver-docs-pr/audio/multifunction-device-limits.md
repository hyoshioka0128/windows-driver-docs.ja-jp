---
title: 多機能デバイスの制限
description: 多機能デバイスの制限
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多機能オーディオ デバイス WDK、制限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a94fe1c2210cdf3800f08b7ed82cbe14ffc8188
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363224"
---
# <a name="multifunction-device-limits"></a>多機能デバイスの制限


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


多機能デバイスあたりのオーディオの関数の数は、次の要因によって制限されます。

-   アダプタのドライバを呼び出すと[ **PcAddAdapterDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddadapterdevice)、関数の 4 番目のパラメーター、 *MaxObjects*、ミニポート ドライバーの最大数のオブジェクトを指定します。ドライバーをサポートできます。 サンプル アダプターのドライバーで、Microsoft Windows Driver Kit (WDK) では、このパラメーターを設定する最大の整数の定数\_を小さな値 (5 個以下) は通常、ミニポートします。 複数のステレオのペアまたは他の種類のオーディオ サブデバイスをサポートする場合は、この値を大きく必要があります。

 

 





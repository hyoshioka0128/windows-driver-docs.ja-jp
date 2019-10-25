---
title: 多機能デバイスの制限
description: 多機能デバイスの制限
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多機能オーディオデバイス WDK、制限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc780ab2bd7c1684c0d520747e9977b9708217de
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832567"
---
# <a name="multifunction-device-limits"></a>多機能デバイスの制限


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


多機能デバイスごとのオーディオ関数の数は、次の要因によって制限されます。

-   アダプタードライバーが[**Pcaddadapterdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddadapterdevice)を呼び出すと、関数の4番目のパラメーター *maxobjects*によって、ドライバーがサポートできるミニポートドライバーオブジェクトの最大数が指定されます。 Microsoft Windows Driver Kit (WDK) のサンプルアダプタードライバーでは、このパラメーターを整数定数 MAX\_ミニポートに設定しています。これは通常、小さい値 (5 以下) になるように定義されています。 複数のステレオペアまたはその他の種類のオーディオサブデバイスをサポートする場合は、この値を大きくすることが必要になる場合があります。

 

 





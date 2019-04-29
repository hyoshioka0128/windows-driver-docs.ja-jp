---
title: 多機能デバイスの制限
description: 多機能デバイスの制限
ms.assetid: 9375c451-b83f-4655-b1e2-cbd693eaaf5f
keywords:
- 多機能オーディオ デバイス WDK、制限
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbaf4bd034826c29e6dc126416d452a40df0c8d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332300"
---
# <a name="multifunction-device-limits"></a>多機能デバイスの制限


## <span id="multifunction_device_limits"></span><span id="MULTIFUNCTION_DEVICE_LIMITS"></span>


多機能デバイスあたりのオーディオの関数の数は、次の要因によって制限されます。

-   アダプタのドライバを呼び出すと[ **PcAddAdapterDevice**](https://msdn.microsoft.com/library/windows/hardware/ff537683)、関数の 4 番目のパラメーター、 *MaxObjects*、ミニポート ドライバーの最大数のオブジェクトを指定します。ドライバーをサポートできます。 サンプル アダプターのドライバーで、Microsoft Windows Driver Kit (WDK) では、このパラメーターを設定する最大の整数の定数\_を小さな値 (5 個以下) は通常、ミニポートします。 複数のステレオのペアまたは他の種類のオーディオ サブデバイスをサポートする場合は、この値を大きく必要があります。

 

 





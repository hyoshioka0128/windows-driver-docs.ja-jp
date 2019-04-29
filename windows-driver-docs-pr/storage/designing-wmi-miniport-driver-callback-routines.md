---
title: WMI ミニポート ドライバー コールバック ルーチンの設計
description: WMI ミニポート ドライバー コールバック ルーチンの設計
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI される Srb WDK の記憶域、コールバック ルーチンの設計
- コールバック ルーチン WDK WMI される Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80e519a45d54adc5fe7f320593c4112c17a97b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331745"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>WMI ミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


SCSI ポート WMI ライブラリを使用するには、ミニポート ドライバーで、次のミニポート ドライバー コールバック ルーチンを実装する必要があります。

[**HwScsiWmiExecuteMethod**](https://msdn.microsoft.com/library/windows/hardware/ff557332)

[**HwScsiWmiFunctionControl**](https://msdn.microsoft.com/library/windows/hardware/ff557338)

[**HwScsiWmiQueryDataBlock**](https://msdn.microsoft.com/library/windows/hardware/ff557340)

[**HwScsiWmiQueryReginfo**](https://msdn.microsoft.com/library/windows/hardware/ff557344)

[**HwScsiWmiSetDataBlock**](https://msdn.microsoft.com/library/windows/hardware/ff557349)

[**HwScsiWmiSetDataItem**](https://msdn.microsoft.com/library/windows/hardware/ff557357)

次のセクションではする際に役立つ設計、 *HwScsiWmiExecuteMethod*コールバック ルーチンおよびデータ フィールドを管理するコールバック ルーチン。

[WMI クラスとメソッドを処理するミニポート ドライバー コールバック ルーチンの設計](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[データ フィールドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

 





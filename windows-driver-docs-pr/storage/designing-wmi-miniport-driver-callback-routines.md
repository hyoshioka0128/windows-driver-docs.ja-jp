---
title: WMI ミニポート ドライバー コールバック ルーチンの設計
description: WMI ミニポート ドライバー コールバック ルーチンの設計
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI される Srb WDK の記憶域、コールバック ルーチンの設計
- コールバック ルーチン WDK WMI される Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4c778abfebf2989516a8ff2b0ea7611aa56145a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368298"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>WMI ミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


SCSI ポート WMI ライブラリを使用するには、ミニポート ドライバーで、次のミニポート ドライバー コールバック ルーチンを実装する必要があります。

[**HwScsiWmiExecuteMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[**HwScsiWmiFunctionControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[**HwScsiWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[**HwScsiWmiQueryReginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[**HwScsiWmiSetDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[**HwScsiWmiSetDataItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)

次のセクションではする際に役立つ設計、 *HwScsiWmiExecuteMethod*コールバック ルーチンおよびデータ フィールドを管理するコールバック ルーチン。

[WMI クラスとメソッドを処理するミニポート ドライバー コールバック ルーチンの設計](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[データ フィールドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

 





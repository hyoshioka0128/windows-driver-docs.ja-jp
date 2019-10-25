---
title: WMI ミニポート ドライバー コールバック ルーチンの設計
description: WMI ミニポート ドライバー コールバック ルーチンの設計
ms.assetid: 3bf5b214-e09c-48bc-832b-d0efd3bc8875
keywords:
- WMI SRBs WDK storage、コールバックルーチンの設計
- コールバックルーチン WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7678735735af3ef98f64573a819fc2e0c399e89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845181"
---
# <a name="designing-wmi-miniport-driver-callback-routines"></a>WMI ミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_wmi_miniport_driver_callback_routines_kg"></span><span id="DDK_DESIGNING_WMI_MINIPORT_DRIVER_CALLBACK_ROUTINES_KG"></span>


SCSI ポート WMI ライブラリを使用するには、ミニポートドライバーに次のミニポートドライバーコールバックルーチンを実装する必要があります。

[**HwScsiWmiExecuteMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)

[**HwScsiWmiFunctionControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)

[**HwScsiWmiQueryDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)

[**HwScsiWmiQueryReginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)

[**HwScsiWmiSetDataBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_datablock)

[**HwScsiWmiSetDataItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)

次のセクションでは、 *HwScsiWmiExecuteMethod*コールバックルーチンと、データフィールドを管理するコールバックルーチンの設計について説明します。

[メソッドを使用して WMI クラスを処理するミニポートドライバーのコールバックルーチンを設計する](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

[データフィールドを含む WMI クラスを処理するミニポートドライバーコールバックルーチンの設計](designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-.md)

 

 





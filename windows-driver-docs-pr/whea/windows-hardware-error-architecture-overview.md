---
title: Windows Hardware Error Architecture の概要
description: Windows Hardware Error Architecture の概要
ms.assetid: 859caa70-371c-4191-baf9-52a38411164a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d1f2c9e5d18da89df498e8a7e38af71fec1e426c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826307"
---
# <a name="windows-hardware-error-architecture-overview"></a>Windows Hardware Error Architecture の概要

Windows 10 Version 1903 では、WHEA へのインターフェイスが簡単になりました。  詳細については、次のページを参照してください。

- [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
- [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
- [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
- [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
- [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
- [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
- [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

ここでは、次のトピックについて説明します。

[ハードウェアエラーとエラーソース](hardware-errors-and-error-sources.md)

[Microsoft Windows とシステムファームウェアの関係](relationship-between-microsoft-windows-and-the-system-firmware.md)

[Windows ハードウェアエラーアーキテクチャのコンポーネント](components-of-the-windows-hardware-error-architecture.md)

[エラー処理](error-processing.md)

[エラーレコード](error-records.md)

[エラーレコードの永続化メカニズム](error-record-persistence-mechanism.md)

[予測エラー分析 (PFA)](predictive-failure-analysis--pfa-.md)

[以前のバージョンの Microsoft Windows との違い](differences-from-previous-versions-of-microsoft-windows.md)

 

 





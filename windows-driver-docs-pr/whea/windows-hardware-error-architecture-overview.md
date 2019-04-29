---
title: Windows Hardware Error Architecture の概要
description: Windows Hardware Error Architecture の概要
ms.assetid: 859caa70-371c-4191-baf9-52a38411164a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bfeb0802333e7e3f1393be049dad71b98e8111d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323134"
---
# <a name="windows-hardware-error-architecture-overview"></a>Windows Hardware Error Architecture の概要

Windows 10、バージョンが 1903 WHEA に使いやすいインターフェイスが含まれています。  詳細については、次のページを参照してください。

- [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
- [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
- [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
- [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
- [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
- [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
- [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

ここでは、次のトピックについて説明します。

[ハードウェア エラーとエラーのソース](hardware-errors-and-error-sources.md)

[Microsoft Windows とシステム ファームウェア間のリレーションシップ](relationship-between-microsoft-windows-and-the-system-firmware.md)

[Windows ハードウェア エラーのアーキテクチャのコンポーネント](components-of-the-windows-hardware-error-architecture.md)

[エラー処理](error-processing.md)

[エラー レコード](error-records.md)

[エラー レコードの永続化メカニズム](error-record-persistence-mechanism.md)

[予測的な失敗の分析 (PFA)](predictive-failure-analysis--pfa-.md)

[Microsoft Windows の以前のバージョンとの違い](differences-from-previous-versions-of-microsoft-windows.md)

 

 





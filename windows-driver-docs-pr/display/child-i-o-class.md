---
title: 子 I/O クラス
description: 子 I/O クラス
ms.assetid: e467ef0c-a969-4cc1-a5b5-2416794051f2
keywords:
- 子 i/o クラス WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f531f6436bbc4bb709740bb57a49c96e63710691
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839809"
---
# <a name="child-io-class"></a>子 I/O クラス


Windows Display Driver Model (WDDM) では、子 i/o クラス関数のいずれかを再入可能な方法で呼び出すことは許可されていません。 つまり、最大で1つのスレッドは、特定の時点で子デバイスごとに次のいずれかの関数内で実行できます。

-   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)

-   [DxgkDdiQueryConnectionChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryconnectionchange)

-   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)

-   [*DxgkDdiDisplayDetectControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_displaydetectcontrol)

-   [*DxgkDdiI2CReceiveDataFromDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_i2c_receive_data_from_display)

-   [*DxgkDdiI2CTransmitDataToDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_i2c_transmit_data_to_display)

-   [*DxgkDdiOPMConfigureProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)

-   [*DxgkDdiOPMCreateProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)

-   [*DxgkDdiOPMDestroyProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

-   [*DxgkDdiOPMGetCertificate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)

-   [*DxgkDdiOPMGetCertificateSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)

-   [*DxgkDdiOPMGetCOPPCompatibleInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)

-   [*DxgkDdiOPMGetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)

-   [*DxgkDdiOPMGetRandomNumber*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)

-   [*DxgkDdiOPMSetSigningKeyAndSequenceNumbers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)

 

 






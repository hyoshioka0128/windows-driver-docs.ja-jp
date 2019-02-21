---
title: 子 I/O クラス
description: 子 I/O クラス
ms.assetid: e467ef0c-a969-4cc1-a5b5-2416794051f2
keywords:
- 子 I/O クラス WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e91ebf81f4592602da288afbfff84fbdd19fc5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535882"
---
# <a name="child-io-class"></a>子 I/O クラス


Windows Display Driver Model (WDDM) 許可されていません、子のいずれかへの呼び出しを I/O クラスの関数、再入可能な方法で。 つまりが最大で 1 つのスレッドできます以内に稼働する子デバイスごとに、次の関数のいずれかの特定の時点で。

-   [*DxgkDdiQueryChildStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_status)

-   [DxgkDdiQueryConnectionChange](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryconnectionchange)

-   [*DxgkDdiQueryDeviceDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)

-   [*DxgkDdiDisplayDetectControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_displaydetectcontrol)

-   [*DxgkDdiI2CReceiveDataFromDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_i2c_receive_data_from_display)

-   [*DxgkDdiI2CTransmitDataToDisplay*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_i2c_transmit_data_to_display)

-   [*DxgkDdiOPMConfigureProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)

-   [*DxgkDdiOPMCreateProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_create_protected_output)

-   [*DxgkDdiOPMDestroyProtectedOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)

-   [*DxgkDdiOPMGetCertificate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate)

-   [*DxgkDdiOPMGetCertificateSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_certificate_size)

-   [*DxgkDdiOPMGetCOPPCompatibleInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_copp_compatible_information)

-   [*DxgkDdiOPMGetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_information)

-   [*DxgkDdiOPMGetRandomNumber*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_get_random_number)

-   [*DxgkDdiOPMSetSigningKeyAndSequenceNumbers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_set_signing_key_and_sequence_numbers)

 

 






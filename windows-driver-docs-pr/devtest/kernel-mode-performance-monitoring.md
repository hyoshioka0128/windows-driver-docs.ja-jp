---
title: カーネル モードのパフォーマンスの監視
description: カーネル モードのパフォーマンスの監視
ms.assetid: 317d2f9d-db50-4513-8bbd-28f429236877
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447859191174145b0981b2ac2eb7a75b08b5258b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839543"
---
# <a name="kernel-mode-performance-monitoring"></a>カーネル モードのパフォーマンスの監視

Microsoft Windows オペレーティングシステムでは、システムコンポーネントとサードパーティがパフォーマンス[カウンター](https://go.microsoft.com/fwlink/p/?linkid=144442)を使用して、標準的な方法でパフォーマンスメトリックを公開できます。

ここでは、次のトピックについて説明します。

[カーネルモードのパフォーマンスカウンターについて](about-kernel-mode-performance-counters.md)

[カーネルモードのパフォーマンスカウンターの使用](using-kernel-mode-performance-counters.md)

カーネルモードパフォーマンスカウンターでは、次の DDIs を使用します。

## <a name="kernel-mode-performance-counter-provider-functions"></a>カーネルモードパフォーマンスカウンタープロバイダー関数

[PcwAddInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwaddinstance)

[PcwCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pcw_callback)

[PcwCloseInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwcloseinstance)

[PcwCreateInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwcreateinstance)

[PcwRegister](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)

[PcwUnregister 解除](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)

## <a name="kernel-mode-performance-counter-structures-and-enumerations"></a>カーネルモードのパフォーマンスカウンターの構造と列挙

[PCW_CALLBACK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_callback_information)

[PCW_CALLBACK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pcw_callback_type)

[PCW_COUNTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_descriptor)

[PCW_COUNTER_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_information)

[PCW_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_information)

[PCW_MASK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_mask_information)

[PCW_REGISTRATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_registration_information)

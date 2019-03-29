---
title: カーネル モードのパフォーマンスの監視
description: カーネル モードのパフォーマンスの監視
ms.assetid: 317d2f9d-db50-4513-8bbd-28f429236877
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09b71c8ab6452098ebe8a2012d23bb71641727d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581017"
---
# <a name="kernel-mode-performance-monitoring"></a>カーネル モードのパフォーマンスの監視

Microsoft Windows オペレーティング システムにより、システム コンポーネントとを使用して、標準的な方法でパフォーマンス メトリックを公開するサード パーティ[パフォーマンス カウンター](https://go.microsoft.com/fwlink/p/?linkid=144442)します。

セクションには、次のトピックが含まれています。

[カーネル モードのパフォーマンス カウンターについて](about-kernel-mode-performance-counters.md)

[カーネル モードのパフォーマンス カウンターの使用](using-kernel-mode-performance-counters.md)

カーネル モードのパフォーマンス カウンターは、次の Ddi の利用します。

## <a name="kernel-mode-performance-counter-provider-functions"></a>カーネル モードのパフォーマンス カウンター プロバイダー関数

[PcwAddInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwaddinstance)

[PcwCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pcw_callback)

[PcwCloseInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwcloseinstance)

[PcwCreateInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwcreateinstance)

[PcwRegister](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwregister)

[PcwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwunregister)

## <a name="kernel-mode-performance-counter-structures-and-enumerations"></a>カーネル モードのパフォーマンス カウンターの構造および列挙体

[PCW_CALLBACK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_callback_information)

[PCW_CALLBACK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pcw_callback_type)

[PCW_COUNTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_counter_descriptor)

[PCW_COUNTER_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_counter_information)

[PCW_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_counter_information)

[PCW_MASK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_mask_information)

[PCW_REGISTRATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_registration_information)

---
title: パラレル デバイスに関する情報の取得
description: パラレル デバイスに関する情報の取得
ms.assetid: a891718a-9e2c-4823-a0b9-5cbe770c3f85
keywords:
- デバイス情報の取得、WDK を並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1064069b7ae2f85bbaf664df819d7530ab243492
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358521"
---
# <a name="obtaining-information-about-a-parallel-device"></a>パラレル デバイスに関する情報の取得





加え[並列デバイスへの接続](connecting-to-a-parallel-device.md)クライアントは、次のデバイス制御要求を使用して並列デバイスに関する追加情報を取得します。

[**IOCTL\_IEEE1284\_GET\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode)

[**IOCTL\_PAR\_取得\_既定\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_get_default_modes)

[**IOCTL\_PAR\_取得\_デバイス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_get_device_caps)

[**IOCTL\_PAR\_IS\_ポート\_FREE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_is_port_free)

[**IOCTL\_PAR\_クエリ\_デバイス\_ID\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_device_id_size)

[**IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_device_id)

[**IOCTL\_PAR\_クエリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_information)

[**IOCTL\_PAR\_クエリ\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_location)

[**IOCTL\_PAR\_クエリ\_RAW\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_raw_device_id)

[**IOCTL\_シリアル\_取得\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_get_timeouts)

 

 





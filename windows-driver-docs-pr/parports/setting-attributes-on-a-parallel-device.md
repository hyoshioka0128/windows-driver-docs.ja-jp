---
title: パラレル デバイスの属性の設定
description: パラレル デバイスの属性の設定
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- デバイスの属性、WDK を並列します。
- デバイスの並列属性 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c7669bc15f4dda5d7c9f02e18995b5f390b192
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353591"
---
# <a name="setting-attributes-on-a-parallel-device"></a>パラレル デバイスの属性の設定





並列のデバイスの指定された操作を設定する次のデバイスに対する制御要求クライアントを使用します。

-   [**IOCTL\_PAR\_設定\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_set_information)並列デバイスを初期化します。

-   [**IOCTL\_シリアル\_設定\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)並列デバイス用のタイムアウトを設定します。

-   [**IOCTL\_PAR\_設定\_読み取り\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_set_read_address) ECP または並列デバイス アドレス (チャネル) を読み取る EPP を設定します。

-   [**IOCTL\_PAR\_設定\_書き込み\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_set_write_address) ECP または EPP 書き込み (チャネル) のアドレス、並列のデバイスを設定します。

 

 





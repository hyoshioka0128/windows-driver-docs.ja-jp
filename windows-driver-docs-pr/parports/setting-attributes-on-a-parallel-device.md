---
title: パラレル デバイスの属性の設定
description: パラレル デバイスの属性の設定
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- パラレルデバイス WDK、属性
- 属性 WDK の並列デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007e60936f79a7df1f037d780019d165d7cce148
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842319"
---
# <a name="setting-attributes-on-a-parallel-device"></a>パラレル デバイスの属性の設定





クライアントは、次のデバイス制御要求を使用して、並列デバイスに対して指定された操作を設定します。

-   [**IOCTL\_PAR\_設定\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_information)は、並列デバイスを初期化します。

-   [**IOCTL\_シリアル\_セット\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)は、並列デバイスのタイムアウトを設定します。

-   [**IOCTL\_PAR\_SET\_読み取り\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_read_address)は、パラレルデバイスの ECP または EPP 読み取りアドレス (チャネル) を設定します。

-   [**IOCTL\_PAR\_SET\_書き込み\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_write_address)は、パラレルデバイスの ECP または EPP 書き込みアドレス (チャネル) を設定します。

 

 





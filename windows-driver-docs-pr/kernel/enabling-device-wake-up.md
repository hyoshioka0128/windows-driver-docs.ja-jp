---
title: デバイス ウェイクアップの有効化
description: デバイス ウェイクアップの有効化
ms.assetid: 1c3b9ebc-cc77-4562-9c57-56f2c9a69772
keywords:
- Irp WDK 電源管理
- 復帰デバイス
- ウェイクアップ機能 WDK の電源管理
- デバイスのウェイクアップと WDK の電源管理
- IRP_MN_WAIT_WAKE
- IRP_MJ_POWER
- DEVICE_CAPABILITIES 構造体
- パワー WDK カーネルを復元しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a4e488c13fc3705d9b83cc8fa98e31714648fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836787"
---
# <a name="enabling-device-wake-up"></a>デバイス ウェイクアップの有効化





デバイスでウェイクアップがサポートされている場合は、そのデバイスの電源ポリシー所有者がウェイクアップを有効または無効にできる必要があります。 ドライバーを使用すると、 [**irp\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求を、マイナー関数コード[**IRP\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)正常に送信することによってウェイクアップできます。また、以前に送信された**irp\_完了\_待機をキャンセルすると、ウェイクアップが無効になり\___ のスリープ解除**。 1つのデバイスには、一度に保留 **\_ウェイク要求を待機\_** 1 つの IRP\_しか設定できません。

デバイスがウェイクアップをサポートしているかどうか、ウェイクアップできるデバイスの電源状態、およびデバイスがシステムをスリープ解除できるシステム電源の状態を確認するには、ドライバーは**Systemwake**、 **devicewake**、および **WakeFromD * * * を確認します。* [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造の x メンバー。

ドライバーのウェイクアップシグナルを有効化、無効化、および応答する方法の詳細については、「[ウェイクアップ機能を搭載したデバイスのサポート](supporting-devices-that-have-wake-up-capabilities.md)」を参照してください。

 

 





---
title: 電源 IRP の処理
description: 電源 IRP の処理
ms.assetid: 0fe4f27a-101d-41af-8f00-fb36da5dc793
keywords:
- 電源管理 WDK カーネル、Irp
- Irp WDK 電源管理
- 電源 Irp WDK カーネル、電源 Irp について
- IRP_MJ_POWER
- IRP_MN_QUERY_POWER
- IRP_MN_SET_POWER
- IRP_MN_WAIT_WAKE
- IRP_MN_POWER_SEQUENCE
- 電源状態 WDK カーネル
- 状態 WDK 電源管理
- 電源状態の変更 WDK カーネル
- power WDK カーネルを節約する
- スリープ電源管理 WDK カーネル
- 電源状態のクエリ
- スリープ状態のデバイス WDK 電源管理
- I/o 要求パケットの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec6ae561af2a1a93c1c0c8a1d1b2700f1a8f4de1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836487"
---
# <a name="handling-power-irps"></a>電源 IRP の処理





ドライバーは、 [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンの電源 irp を処理します。 すべての電源管理要求には、主な IRP コード[**irp\_MJ\_パワー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)と、次のいずれかのマイナーコードがあります。

[**IRP\_\_クエリ\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) -変更された電源状態を実現できるかどうかを判断するためのクエリ

[**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) -ある電源状態から別の電源状態への変更を要求します

[**IRP\_\_待機\_wake**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) -デバイスをスリープ状態にするかシステムを有効にすることを要求します

[**IRP\_\_電源\_シーケンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence) —特定のデバイスへの電源の復元を最適化するための情報を要求します

Irp\_がサポートされるようになり、POWER and Irp\_ **\_\_設定**されています。**クエリ\_電力**が必要です。 これらの Irp を処理するには、すべてのドライバーが準備されている必要があります。

外部信号への応答としてウェイクアップできる任意のデバイスのデバイススタック内のすべてのドライバーに対して、 **IRP\_\_待機\_ウェイク**が必要です。 ドライバーは、この IRP を送信して、デバイスのウェイクアップを有効にします。

**IRP\_\_電源\_シーケンス**のサポートはオプションです。 この IRP は、電力の復元に長い時間がかかるデバイスの最適化を提供します。

電源 IRP では、システムの電源操作またはデバイスの電源操作を指定できます。 次のセクションで説明するように、[個々のデバイスのシステムと電源 irp](power-irps-for-individual-devices.md) [の電源 irp](power-irps-for-the-system.md)は、デバイススタックを通じてわずかに異なるパスを使用します。

 

 





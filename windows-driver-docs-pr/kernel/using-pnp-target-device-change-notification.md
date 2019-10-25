---
title: PnP ターゲット デバイス変更通知の使用
description: PnP ターゲット デバイス変更通知の使用
ms.assetid: a56bda5c-e398-442d-bc90-2e63f8f7e6bf
keywords:
- 通知 WDK PnP、ターゲットデバイスの変更
- ターゲットデバイスの変更通知の WDK PnP
- Eventカテゴリ Targetdevicechange notification
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 54d1705748b38c3a6894baa2b9c143709e69f1a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835869"
---
# <a name="using-pnp-target-device-change-notification"></a>PnP ターゲット デバイス変更通知の使用

デバイスを削除しようとしているときにドライバーが通知を受けることができるように、ドライバーはデバイスで**Eventカテゴリ Targetdevicechange** notification に登録します。 たとえば、ドライバーがデバイスへのハンドルを開く場合、ドライバーはデバイスの**Eventカテゴリ Targetdevicechange** notification に登録する必要があります。これにより、PnP マネージャーがデバイスを削除する必要があるときにドライバーがハンドルを閉じることができるようになります。

ドライバーは、 **Eventカテゴリ Targetdevicechange** notification を使用してカスタム通知を作成することもできます。 (「 [PnP カスタム通知の使用」を](using-pnp-custom-notification.md)参照してください)。

> [!IMPORTANT]
> PnP ターゲットデバイスの変更通知の登録は、ターゲットデバイスの電源状態の変更についてリスナーに通知するためのものではありません。 ドライバーがターゲットデバイスの電源変更について認識する必要がある場合、ドライバーはデバイス間の電源関係を定義する必要があります。 
>
> 電源関係を定義するために、ドライバーは*Type*パラメーターを**powerrelations**に設定して[**IoInvalidateDeviceRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)を呼び出し、Powerrelations に対する PnP マネージャーの[IRP_MN_QUERY_DEVICE_RELATIONS](irp-mn-query-device-relations.md)クエリに応答します。正しい情報を使用します。

次のサブセクションでは、ターゲットデバイスの変更通知に登録する方法と、PnP 通知コールバックルーチンでターゲットデバイスの変更イベントを処理する方法について説明します。

[ターゲットデバイスの変更通知に登録しています](registering-for-target-device-change-notification.md)

[GUID\_ターゲット\_デバイスの処理\_クエリ\_削除イベント](handling-a-guid-target-device-query-remove-event.md)

[\_デバイスの GUID\_ターゲットの処理\_\_完了イベントの削除](handling-a-guid-target-device-remove-complete-event.md)

[\_ターゲット\_デバイスを処理して\_取り消されたイベントを削除\_](handling-a-guid-target-device-remove-cancelled-event.md)

 

 





---
title: PnP ターゲット デバイス変更通知の使用
description: PnP ターゲット デバイス変更通知の使用
ms.assetid: a56bda5c-e398-442d-bc90-2e63f8f7e6bf
keywords:
- 通知 WDK PnP、ターゲット デバイスの変更
- ターゲット デバイスの変更通知 PnP WDK
- EventCategoryTargetDeviceChange 通知
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1ec75ef243cc1b8dd7f6b6bb6dda05a4dc84ba3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391065"
---
# <a name="using-pnp-target-device-change-notification"></a>PnP ターゲット デバイス変更通知の使用

ドライバーの登録の**EventCategoryTargetDeviceChange**通知デバイス、デバイスが削除される直前にある場合、ドライバーに通知することができます。 たとえば、ドライバーがデバイスを識別するハンドルを開いた場合、ドライバーに登録する必要があります**EventCategoryTargetDeviceChange** PnP マネージャーがデバイスを削除する必要がある場合、ドライバーはそのハンドルを閉じることができますので、デバイスに通知します。

ドライバーを使用できるも**EventCategoryTargetDeviceChange**カスタム通知を通知します。 (を参照してください[PnP カスタム通知を使用して](using-pnp-custom-notification.md))。

> [!IMPORTANT]
> ターゲット デバイスの電源状態の変更をリスナーに通知する PnP ターゲット デバイスの変更通知を登録することはありません。 をドライバーがターゲット デバイスの電源の変更について知っておく必要がある場合、ドライバーは代わりにデバイスの電源関係を定義する必要があります。 
>
> 電源の関係では、ドライバーの呼び出しを定義する[ **IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)で、*型*パラメーターに設定**PowerRelations**、PnP マネージャーに応答し、 [IRP_MN_QUERY_DEVICE_RELATIONS](irp-mn-query-device-relations.md)照会**PowerRelations**適切な情報。

次のサブセクションでは、ターゲット デバイスの変更通知に登録する方法と PnP 通知コールバック ルーチンでは、ターゲット デバイスの変更イベントを処理する方法について説明します。

[ターゲット デバイスの変更通知を登録します。](registering-for-target-device-change-notification.md)

[GUID の処理\_ターゲット\_デバイス\_クエリ\_削除イベント](handling-a-guid-target-device-query-remove-event.md)

[GUID の処理\_ターゲット\_デバイス\_削除\_完了イベント](handling-a-guid-target-device-remove-complete-event.md)

[GUID の処理\_ターゲット\_デバイス\_削除\_キャンセル イベント](handling-a-guid-target-device-remove-cancelled-event.md)

 

 





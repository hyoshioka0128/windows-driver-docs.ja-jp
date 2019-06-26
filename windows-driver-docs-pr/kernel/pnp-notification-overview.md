---
title: PnP 通知の概要
description: PnP 通知の概要
ms.assetid: 134a1ea1-78c2-4bab-b5e9-ae21901772ea
keywords:
- カーネル WDK PnP 通知
- プラグ アンド プレイの WDK カーネル、通知
- WDK の通知については、PnP 通知
- イベント通知 PnP WDK
- EventCategoryDeviceInterfaceChange 通知
- EventCategoryTargetDeviceChange 通知
- EventCategoryHardwareProfileChange 通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a30ae03c7bc62f3f6b1334fb247de09f6e443fef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362932"
---
# <a name="pnp-notification-overview"></a>PnP 通知の概要





PnP マネージャーでは、ドライバーとアプリケーションを特定のイベントには、一般にする、特定のデバイスまたはシステムが発生したときに通知するためのメカニズムを提供します。 ドライバーは、次のカテゴリのイベントの通知を登録できます。

-   **EventCategoryDeviceInterfaceChange**

    このカテゴリのデバイスのインターフェイスでイベントの登録は、ドライバー、PnP マネージャーに、次のイベントのドライバーにより通知されます。

    <a href="" id="guid-device-interface-arrival"></a>GUID\_デバイス\_インターフェイス\_到着  
    指定したクラスのデバイスのインターフェイスが有効になっていることを示します。 たとえば、ユーザーがコンピューターに新しいディスクを追加し、ボリューム マネージャーには、新しいボリューム (「ボリューム」クラスのデバイス インターフェイス) が有効になっています。

    <a href="" id="guid-device-interface-removal"></a>GUID\_デバイス\_インターフェイス\_削除  
    指定したクラスのデバイスのインターフェイスが無効になっていることを示します。

    参照してください[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)および関連するデバイスのインターフェイスの詳細については、ルーチン。

-   **EventCategoryTargetDeviceChange**

    ドライバーは、このカテゴリのデバイス上のイベントの登録、デバイスで、次のイベントが発生した場合、ドライバーにより PnP マネージャーに通知されます。

    <a href="" id="guid-target-device-query-remove"></a>GUID\_ターゲット\_デバイス\_クエリ\_削除  
    デバイスのドライバーを削除するには、約 PnP マネージャーであることを示します。 いくつかの操作が、このイベントを発生など: ユーザーが、マシンから、指定されたデバイスを削除する要求またはユーザーがデバイス用のドライバーの更新要求を発行します。 この通知は、承認または間もなく削除操作を拒否するデバイスのドライバーを要求します。

    <a href="" id="guid-target-device-remove-complete"></a>GUID\_ターゲット\_デバイス\_削除\_完了  
    指定したデバイスがコンピューターから削除されたこと、またはユーザーがデバイスのドライバーを変更することを示します。

    <a href="" id="guid-target-device-remove-cancelled"></a>GUID\_ターゲット\_デバイス\_削除\_キャンセル  
    指定されたデバイス上の兆候の削除操作が取り消されたことを示します。

    <a href="" id="guid-xxx---custom-events-"></a>GUID\_*XXX* (カスタム イベント)  
    指定したデバイスのカスタム イベントが発生したことを示します。

    ドライバーのライターでは、デバイスのカスタム イベントを定義できます。 ドライバー (または別の関連するコンポーネント) カスタム イベントが発生した PnP マネージャーに通知、PnP マネージャーでは、ターゲット デバイスの登録されているすべてのコンポーネントの変更通知デバイスに通知します。

    見なすことができるインターフェイスの「パッシブ」関心、デバイス インターフェイスの変更の登録とは異なりのターゲット デバイスの変更を登録するデバイスに「アクティブ」の関心を示します。

-   **EventCategoryHardwareProfileChange**

    このカテゴリには、次のイベントが含まれています。

    <a href="" id="guid-hwprofile-query-change"></a>GUID\_HWPROFILE\_クエリ\_変更  
    ユーザーがコンピューターのハードウェア プロファイルを変更する要求されていることを示します。 PnP マネージャーでは、この通知を使用して、システムの操作を中断せず、ハードウェア プロファイルを変更ことかどうかを登録済みのコンポーネントに問い合わせてください。 通常、登録済みのコンポーネントには、これらのクエリ要求が成功します。

    <a href="" id="guid-hwprofile-change-complete"></a>GUID\_HWPROFILE\_変更\_完了  
    マシンのハードウェア プロファイルが変更されたことを示します。 プロファイルに固有の設定は、ドライバーは、ハードウェア プロファイルを変更した後、このようなドライバーはこれらの設定を更新する必要があります。

    <a href="" id="guid-hwprofile-change-cancelled"></a>GUID\_HWPROFILE\_変更\_キャンセル  
    間もなく、ハードウェア プロファイルの変更が取り消されたことを示します。

PnP 通知は、カーネル モードのコンポーネントのように動作します。

1.  ドライバーを呼び出すことによってイベントのカテゴリに関する通知の登録[ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)します。

    PnP 通知コールバック ルーチンは、ドライバーが明示的に登録を削除するまで、登録されているままになります。

2.  PnP マネージャーは、登録済みのカテゴリのイベントが発生したときに、ドライバーのコールバック ルーチンを呼び出します。

3.  ドライバーは、呼び出すことによって、コールバックの登録を削除します[ **IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)します。

ドライバーの同期イベントを生成または終了の処理中に発生するイベントを非同期に待機する必要がありますされません。

PnP 通知については、次のセクションを参照してください。

[PnP 通知コールバック ルーチンを記述するためのガイドライン](guidelines-for-writing-pnp-notification-callback-routines.md)

[PnP デバイス インターフェイスの変更通知を使用してください。](using-pnp-device-interface-change-notification.md)

[ターゲットの PnP デバイスの変更通知を使用してください。](using-pnp-target-device-change-notification.md)

[プラグ アンド プレイ ハードウェア プロファイルの変更通知を使用してください。](using-pnp-hardware-profile-change-notification.md)

[PnP カスタム通知を使用してください。](using-pnp-custom-notification.md)

 

 





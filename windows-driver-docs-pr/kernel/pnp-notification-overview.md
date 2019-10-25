---
title: PnP 通知の概要
description: PnP 通知の概要
ms.assetid: 134a1ea1-78c2-4bab-b5e9-ae21901772ea
keywords:
- PnP WDK カーネル、通知
- WDK カーネル、通知のプラグアンドプレイ
- 通知 WDK PnP、通知について
- イベント通知の WDK PnP
- EventCategoryDeviceInterfaceChange 通知
- Eventカテゴリ Targetdevicechange notification
- Eventカテゴリのハードウェアプロファイルの通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bdb8546b87ccc71e4bf5cca3a655dd900ba0d05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838506"
---
# <a name="pnp-notification-overview"></a>PnP 通知の概要





PnP マネージャーには、特定のデバイスまたはシステム上で特定のイベントが発生したときに、ドライバーおよびアプリケーションが通知を受けるためのメカニズムが用意されています。 ドライバーは、次のカテゴリのイベントの通知を登録できます。

-   **EventCategoryDeviceInterfaceChange**

    ドライバーがデバイスインターフェイスでこのカテゴリのイベントを登録すると、PnP マネージャーは次のイベントをドライバーに通知します。

    <a href="" id="guid-device-interface-arrival"></a>GUID\_デバイス\_インターフェイス\_到着  
    指定したクラスのデバイスインターフェイスが有効になっていることを示します。 たとえば、ユーザーが新しいディスクをマシンに追加し、ボリュームマネージャーが新しいボリューム (クラス "volume" のデバイスインターフェイス) を有効にしたとします。

    <a href="" id="guid-device-interface-removal"></a>GUID\_デバイス\_インターフェイス\_削除  
    指定したクラスのデバイスインターフェイスが無効になっていることを示します。

    デバイスインターフェイスの詳細については、「 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) and related ルーチン」を参照してください。

-   **Eventカテゴリ Targetdevicechange**

    ドライバーがデバイスでこのカテゴリのイベントを登録すると、デバイスで次のイベントが発生したときに、PnP マネージャーからドライバーに通知されます。

    <a href="" id="guid-target-device-query-remove"></a>GUID\_ターゲット\_デバイス\_クエリ\_削除  
    PnP マネージャーがデバイスのドライバーを削除しようとしていることを示します。 このイベントの原因として、ユーザーがコンピューターから特定のデバイスを削除するように要求した場合、またはユーザーがデバイスの更新プログラムドライバーの要求を発行した場合などがあります。 この通知により、デバイスのドライバーが、間もなく削除される操作を承認するか拒否するかを要求します。

    <a href="" id="guid-target-device-remove-complete"></a>\_ターゲット\_デバイス\_削除\_完了した GUID  
    指定したデバイスがコンピューターから削除されているか、デバイスのドライバーをユーザーが変更していることを示します。

    <a href="" id="guid-target-device-remove-cancelled"></a>\_削除\_削除される\_デバイスの GUID\_ターゲット  
    指定されたデバイスでの削除操作が取り消されたことを示します。

    <a href="" id="guid-xxx---custom-events-"></a>GUID\_*XXX* (カスタムイベント)  
    指定されたデバイスでカスタムイベントが発生したことを示します。

    ドライバーライターは、デバイスのカスタムイベントを定義できます。 ドライバー (または他の関連コンポーネント) が、カスタムイベントが発生したことを PnP マネージャーに通知すると、PnP マネージャーは、デバイス上のターゲットデバイス変更通知に登録されているすべてのコンポーネントに通知します。

    デバイスインターフェイスの変更を登録すると、インターフェイスに "パッシブな" ことを考えることができますが、ターゲットデバイスの変更を登録すると、デバイスに "アクティブ" が示されます。

-   **Eventカテゴリのハードウェアプロファイリング**

    このカテゴリには、次のイベントが含まれます。

    <a href="" id="guid-hwprofile-query-change"></a>GUID\_HWPROFILE\_クエリ\_変更  
    ユーザーがマシンのハードウェアプロファイルを変更するように要求したことを示します。 PnP マネージャーは、この通知を使用して、システム操作を中断せずにハードウェアプロファイルを変更できるかどうかを登録済みのコンポーネントに要求します。 通常、登録されたコンポーネントは、これらのクエリ要求に成功します。

    <a href="" id="guid-hwprofile-change-complete"></a>GUID\_HWPROFILE\_変更\_完了しました  
    コンピューターのハードウェアプロファイルが変更されたことを示します。 ドライバーがプロファイル固有の設定を保持している場合、ドライバーは、ハードウェアプロファイルの変更後に、これらの設定を更新する必要があります。

    <a href="" id="guid-hwprofile-change-cancelled"></a>GUID\_HWPROFILE\_変更\_取り消されました  
    ハードウェアプロファイルの変更が中止されたことを示します。

PnP 通知は、次のようなカーネルモードのコンポーネントで使用できます。

1.  ドライバーは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出すことによって、イベントのカテゴリに対する通知を登録します。

    PnP 通知コールバックルーチンは、ドライバーが明示的に登録を削除するまで登録されたままです。

2.  PnP マネージャーは、登録されたカテゴリのイベントが発生したときに、ドライバーのコールバックルーチンを呼び出します。

3.  ドライバーは、 [**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を呼び出すことによって、コールバックの登録を削除します。

ドライバーは、同期イベントを生成したり、終了処理中に非同期イベントが発生するのを待機したりすることはできません。

PnP 通知の詳細については、次のセクションを参照してください。

[PnP 通知コールバックルーチンの記述に関するガイドライン](guidelines-for-writing-pnp-notification-callback-routines.md)

[PnP デバイスインターフェイスの変更通知の使用](using-pnp-device-interface-change-notification.md)

[PnP ターゲットデバイスの変更通知の使用](using-pnp-target-device-change-notification.md)

[PnP ハードウェアプロファイルの変更通知の使用](using-pnp-hardware-profile-change-notification.md)

[PnP カスタム通知の使用](using-pnp-custom-notification.md)

 

 





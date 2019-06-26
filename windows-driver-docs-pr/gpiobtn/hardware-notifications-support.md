---
title: ハードウェア通知サポート
description: Windows 10 バージョン 1709 のインフラストラクチャ通知コンポーネントの Led と振動メカニズムなどのハードウェア依存のサポートを提供します。
ms.assetid: 48df55c4-aa5e-4157-8b90-65ad127d876b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6faf71ac702131f67d0921f4a5d209b0ff8db325
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360894"
---
# <a name="hardware-notifications-support"></a>ハードウェア通知サポート


**適用対象**

-   ドライバー開発者向けと Oem

**重要な API**

-   [ハードウェア通知リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

Windows 10 バージョン 1709 のインフラストラクチャ通知コンポーネントの Led と振動メカニズムなどのハードウェア依存のサポートを提供します。 このサポートは、クライアント ドライバーの迅速な開発を可能にするハードウェア通知コンポーネント専用のカーネルモード ドライバー フレームワーク (KMDF) クラスの拡張を導入することで提供されます。 KMDF クラスの拡張は、本質的には、特定のクラスのデバイス用に定義された機能セットを提供する KMDF ドライバーであり、Windows Driver Model (WDM) 内のポート ドライバーと同様です。 このセクションでは、ハードウェア通知クラスの拡張のアーキテクチャの概要を示します。 KMDF の詳細については、「[Using WDF to Develop a Driver (WDF を使用したドライバーの開発)](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)」をご覧ください。

## <a name="span-idhardwarenotificationclassextensionspanspan-idhardwarenotificationclassextensionspanspan-idhardwarenotificationclassextensionspanhardware-notification-class-extension"></a><span id="Hardware_notification_class_extension"></span><span id="hardware_notification_class_extension"></span><span id="HARDWARE_NOTIFICATION_CLASS_EXTENSION"></span>ハードウェアの notification クラスの拡張機能


ハードウェアの notification クラスの拡張機能は、ハードウェアの通知のドライバーのアーキテクチャの中核となるコンポーネントです。 クラスの拡張機能では、最小限に抑えるために必要な KMDF 対話および通知コンポーネントのコントロールの代わりに、シンプルなインターフェイスを提供する設計されています。 クラスの拡張機能などのタスクを処理します。

-   クライアント ドライバーの登録
-   割り当てとシステム リソースのクリーンアップ
-   クライアント ドライバーの PnP power コールバック関数の登録
-   クライアント ドライバーの I/O キューの登録
-   データの検証とエラー チェック
-   クライアント ドライバーのハードウェア要求の通信

次の図は、基本的なハードウェア notification クラスの拡張機能アーキテクチャを示しています。

![hwn clx アーキテクチャ](images/oem-hwnclx-arch.png)

## <a name="span-idhardwarenotificationclientdriverspanspan-idhardwarenotificationclientdriverspanspan-idhardwarenotificationclientdriverspanhardware-notification-client-driver"></a><span id="Hardware_notification_client_driver"></span><span id="hardware_notification_client_driver"></span><span id="HARDWARE_NOTIFICATION_CLIENT_DRIVER"></span>通知クライアント ドライバーのハードウェア


クライアント ドライバーは、通知のハードウェア コンポーネントので簡単にハードウェアの notification クラスの拡張機能を使用して生成できます。 クライアント ドライバーの唯一の役割は、KMDF の適切なエントリ ポイントを提供、定義されたクラスの拡張機能コールバック関数を実装、電源の状態を管理および制御する物理ハードウェアです。 具体的には、クライアント ドライバーを実装する必要があります、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)と[ *EVT\_WDF\_ドライバー\_デバイス\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) Windows Driver Foundation (WDF) を使用するためのコールバック関数と同様、クラス拡張の必要なコールバック関数。

次の図は、クライアント ドライバーの観点からの相互作用を示しています。

![クライアント ドライバーのアーキテクチャ](images/oem-hwnclx-clientarch.png)

 

 





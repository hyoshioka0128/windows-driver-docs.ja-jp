---
title: ハードウェア通知サポート
description: Windows 10 バージョン1709では、ハードウェアに依存しない通知コンポーネント (Led や振動メカニズムなど) のサポートのためのインフラストラクチャが提供されています。
ms.assetid: 48df55c4-aa5e-4157-8b90-65ad127d876b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f340e2d97cc6bff117d5908158c4ba239e4d3724
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824898"
---
# <a name="hardware-notifications-support"></a>ハードウェア通知サポート


**適用対象**

-   ドライバーの開発者と Oem

**重要な API**

-   [ハードウェア通知リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

Windows 10 バージョン1709では、ハードウェアに依存しない通知コンポーネント (Led や振動メカニズムなど) のサポートのためのインフラストラクチャが提供されています。 このサポートは、クライアント ドライバーの迅速な開発を可能にするハードウェア通知コンポーネント専用のカーネルモード ドライバー フレームワーク (KMDF) クラスの拡張を導入することで提供されます。 KMDF クラスの拡張は、本質的には、特定のクラスのデバイス用に定義された機能セットを提供する KMDF ドライバーであり、Windows Driver Model (WDM) 内のポート ドライバーと同様です。 このセクションでは、ハードウェア通知クラスの拡張のアーキテクチャの概要を示します。 KMDF の詳細については、「[Using WDF to Develop a Driver (WDF を使用したドライバーの開発)](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-framework-to-develop-a-driver)」をご覧ください。

## <a name="span-idhardware_notification_class_extensionspanspan-idhardware_notification_class_extensionspanspan-idhardware_notification_class_extensionspanhardware-notification-class-extension"></a><span id="Hardware_notification_class_extension"></span><span id="hardware_notification_class_extension"></span><span id="HARDWARE_NOTIFICATION_CLASS_EXTENSION"></span>ハードウェア通知クラスの拡張機能


ハードウェア通知クラス拡張は、ハードウェア通知ドライバーアーキテクチャの中心的なコンポーネントです。 クラス拡張は、KMDF との必要な対話を最小限に抑えるように設計されています。代わりに、通知コンポーネントを制御するための簡単なインターフェイスを提供します。 クラス拡張は、次のようなタスクを処理します。

-   クライアントドライバーの登録
-   システムリソースの割り当てとクリーンアップ
-   クライアントドライバー用の PnP 電源コールバック関数の登録
-   クライアントドライバーの i/o キューの登録
-   データの検証とエラーチェック
-   クライアントドライバーへのハードウェア要求の通信

次の図は、基本的なハードウェア通知クラス拡張アーキテクチャを示しています。

![hwn clx アーキテクチャ](images/oem-hwnclx-arch.png)

## <a name="span-idhardware_notification_client_driverspanspan-idhardware_notification_client_driverspanspan-idhardware_notification_client_driverspanhardware-notification-client-driver"></a><span id="Hardware_notification_client_driver"></span><span id="hardware_notification_client_driver"></span><span id="HARDWARE_NOTIFICATION_CLIENT_DRIVER"></span>ハードウェア通知クライアントドライバー


ハードウェア通知クラス拡張を使用して、ハードウェア通知コンポーネントのクライアントドライバーを簡単に生成できます。 クライアントドライバーは、KMDF に適切なエントリポイントを提供し、定義したクラス拡張コールバック関数を実装し、電源状態を管理し、物理ハードウェアを制御するだけです。 具体的には、クライアントドライバーは、 [*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)と[ *.evt\_WDF\_driver\_デバイス\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 、WINDOWS driver Foundation (WDF) によって使用されるコールバック関数の追加、および必要なコールバックを実装する必要があります。クラス拡張の関数。

次の図は、クライアントドライバーの観点からの相互作用を示しています。

![クライアントドライバーのアーキテクチャ](images/oem-hwnclx-clientarch.png)

 

 





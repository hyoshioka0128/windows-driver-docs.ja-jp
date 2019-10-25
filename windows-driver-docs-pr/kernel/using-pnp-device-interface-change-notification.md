---
title: PnP デバイス インターフェイス変更通知の使用
description: PnP デバイス インターフェイス変更通知の使用
ms.assetid: 2ed3518a-601f-4e9b-b375-a9fb62c937a9
keywords:
- 通知 WDK PnP、デバイスインターフェイスの変更
- EventCategoryDeviceInterfaceChange 通知
- デバイスインターフェイスの変更通知の WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b69a5e4fa089a4b02cff69ea6386d8406c909d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835879"
---
# <a name="using-pnp-device-interface-change-notification"></a>PnP デバイス インターフェイス変更通知の使用





ドライバーは、特定のクラスのデバイスインターフェイスが到着する (有効になっている) か、コンピューター上で削除 (無効) されたときにドライバーに通知できるように、 **EventCategoryDeviceInterfaceChange**通知を登録します。 たとえば、複合バッテリドライバーは、クラスバッテリのデバイスインターフェイスを通知するために登録する場合があります。これにより、使用可能な合計バッテリ電力に関する情報をオペレーティングシステムに提供できるようになります。

次のサブセクションでは、デバイスインターフェイスの変更通知を登録する方法と、PnP 通知コールバックルーチンでデバイスインターフェイスの変更イベントを処理する方法について説明します。

[デバイス インターフェイス変更の通知登録](registering-for-device-interface-change-notification.md)

[デバイスインターフェイス変更イベントの処理](handling-device-interface-change-events.md)

デバイスインターフェイスの詳細については、「 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) and related ルーチン」を参照してください。

 

 





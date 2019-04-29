---
title: PnP デバイス インターフェイス変更通知の使用
description: PnP デバイス インターフェイス変更通知の使用
ms.assetid: 2ed3518a-601f-4e9b-b375-a9fb62c937a9
keywords:
- WDK PnP、通知デバイス インターフェイスの変更
- EventCategoryDeviceInterfaceChange 通知
- デバイス インターフェイスの変更通知 PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b584bfdeeae4d3c46cb2389a2d5448e62efc619
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391069"
---
# <a name="using-pnp-device-interface-change-notification"></a>PnP デバイス インターフェイス変更通知の使用





ドライバーの登録の**EventCategoryDeviceInterfaceChange**通知、ドライバーは、特定のクラスのインターフェイスのデバイスが到着したときに通知することができます (有効になっている) またはコンピューターの削除 (無効)。 たとえば、複合バッテリ ドライバーは、合計使用可能なバッテリ電源に関する情報をオペレーティング システムを提供できるようにクラスのバッテリのインターフェイスのデバイスの通知の登録可能性があります。

次のサブセクションでは、デバイス インターフェイスの変更通知に登録する方法と、PnP 通知コールバック ルーチンでは、デバイス インターフェイスの変更イベントを処理する方法について説明します。

[デバイス インターフェイスの変更通知を登録します。](registering-for-device-interface-change-notification.md)

[デバイス インターフェイスの変更イベントの処理](handling-device-interface-change-events.md)

参照してください[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)および関連するデバイスのインターフェイスについてルーチン。

 

 





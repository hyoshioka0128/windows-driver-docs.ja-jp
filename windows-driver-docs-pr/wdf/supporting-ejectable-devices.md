---
title: 取り出し可能デバイスのサポート
description: 取り出し可能デバイスのサポート
ms.assetid: 7820bb71-7218-4c5f-af2b-f41e1b5f696d
keywords:
- PnP WDK KMDF、フロッピー デバイス
- プラグ アンド プレイ WDK KMDF、フロッピー デバイス
- 電源管理 WDK KMDF、フロッピー デバイス
- WDK KMDF のドッキング ステーション
- バス ドライバー WDK KMDF
- デバイス WDK KMDF の取り出し
- 取り出し関係 WDK KMDF
- 移動可能なリムーバブル デバイスの削除
- 移動可能なリムーバブル デバイス WDK KMDF を一覧表示します。
- WDK KMDF の移動可能なリムーバブル デバイスのロック
- WDK KMDF のポータブル デバイス
- モバイル デバイス、WDK KMDF
- リムーバブル デバイス WDK KMDF
- WDK のモバイル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f017f893bf5673b1e9fb307e62334922c59cd820
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382085"
---
# <a name="supporting-ejectable-devices"></a>取り出し可能デバイスのサポート


*移動可能なリムーバブル デバイス*デバイスがドッキング ステーションに挿入され、ドッキング ステーションから取り出すことができます。 通常、デバイスを削除する前に移動可能なリムーバブル デバイスのバスの電源は無効にする必要があります。

デバイスができる場合は、デバイスのバスのバス ドライバーを設定する必要があります、 **EjectSupported**メンバーで、デバイスの[ **WDF\_デバイス\_PNP\_機能** ](https://msdn.microsoft.com/library/windows/hardware/ff551257)構造体。

いずれかを呼び出す、バス ドライバーは、約を取り出すにその列挙子のデバイスのいずれかが判断した場合[ **WdfPdoRequestEject** ](https://msdn.microsoft.com/library/windows/hardware/ff548817)または[ **WdfChildListRequestChildEject**](https://msdn.microsoft.com/library/windows/hardware/ff545641)します。 たとえば、バス ドライバーは、ユーザーに取り出しボタンが押されたことを検出することがあります。

ドライバーを呼び出すと[ **WdfChildListRequestChildEject** ](https://msdn.microsoft.com/library/windows/hardware/ff545641)または[ **WdfPdoRequestEject**](https://msdn.microsoft.com/library/windows/hardware/ff548817)、PnP マネージャーを使用して、 [正しく削除](a-user-unplugs-a-device.md#orderly-removal)シナリオに、デバイスが削除されることをデバイスのドライバーに通知します。 フレームワークが呼び出された後、 [ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)フレームワークであるデバイスのバスのバス ドライバーでのコールバック関数呼び出す、バス ドライバーの[ *EvtDeviceEject* ](https://msdn.microsoft.com/library/windows/hardware/ff540863)を物理的にデバイスを取り出すために必要なすべての操作を実行するコールバック関数。

バス ドライバーのリストを維持できる追加のデバイスを取り出すにも発生すると、デバイスを取り出し、*取り出し関係*します。 ユーザーは、デバイスを削除するとき、PnP マネージャーは自分のデバイスも削除すること、リスト内のデバイスのドライバーを通知します。 取り出し関係の一覧を維持するために、バス ドライバーを使用して、 [ **WdfPdoAddEjectionRelationsPhysicalDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548770)、 [ **WdfPdoRemoveEjectionRelationsPhysicalDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548814)、および[ **WdfPdoClearEjectionRelationsDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff548771)メソッド。

バス ドライバーを設定する必要があります、ドッキング ステーションにデバイスをロックできる場合、 **LockSupported**メンバーで、デバイスの[ **WDF\_デバイス\_PNP\_機能** ](https://msdn.microsoft.com/library/windows/hardware/ff551257)構造体。 バス ドライバーを提供する必要がありますも、 [ *EvtDeviceSetLock* ](https://msdn.microsoft.com/library/windows/hardware/ff540909)の取り出しを無効にするデバイスをロックまたは取り出しを有効にするデバイスのロックを解除するコールバック関数。

 

 






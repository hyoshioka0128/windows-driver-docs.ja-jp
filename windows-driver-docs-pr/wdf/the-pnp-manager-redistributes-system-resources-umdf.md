---
title: PnP マネージャーがシステム リソースを再配布する
description: PnP マネージャーがシステム リソースを再配布する
ms.assetid: c8e6277b-b1e5-449f-b5a0-f5a46b46e56e
keywords:
- WDK UMDF 電源管理のシナリオ、PnP マネージャーは、システム リソースを再分配します。
- システム リソースのシナリオを WDK UMDF の再配布
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f61e2dc439300eb9186831a39fb0692a70988fc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571292"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP マネージャーがシステム リソースを再配布する


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ユーザーがシステムでは、デバイスを追加し、PnP マネージャーが別のデバイスに既に割り当てられているシステム リソースがデバイスに必要な場合、PnP マネージャーは、リソースを再割り当てを試みます。

このプロセス中には、PnP マネージャーは、デバイスを停止し、外の作業 (D0) 状態に移動します。 提供新しいリソースの一覧をデバイスに新しいリソースを使用して、再起動ができるようにします。

リソースを再頒布時に、PnP マネージャーは変更されません、デバイスのリソースの割り当て、デバイスの UMDF に基づいたドライバーのいずれかが提供されている場合、 [ **IPnpCallback::OnQueryStop** ](https://msdn.microsoft.com/library/windows/hardware/ff556811)コールバック関数、し、コールバック関数が再割り当てを拒否しました。

<a href="" id="power-down-sequence"></a>**シーケンスを電源**  
各 UMDF ベース関数とフィルター ドライバーを停止中でデバイスをサポートするために、フレームワークはシーケンス、ドライバー スタックの最上位である driver 以降では、一度に 1 つのドライバーで、次を行います。

1.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoSuspend** ](https://msdn.microsoft.com/library/windows/hardware/ff556790)コールバック関数。

2.  フレームワークは、すべてのデバイスの電源管理対象の I/O キューを停止します。

3.  フレームワークは、ドライバーの[ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803) (存在する) 場合、コールバック関数。

4.  フレームワークは、ドライバーの[ **IPnpCallbackHardware::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556768)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

次の手順を示す図を表示するには、図計画的な削除を参照してください。[ユーザーがデバイスから切り離し](a-user-unplugs-a-device.md)します。

<a href="" id="power-up-sequence-------"></a>**電源投入シーケンス**   
各 UMDF ベース関数とフィルター ドライバーのデバイスをサポートする、フレームワークは、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、シーケンスで、次を行います。

1.  フレームワークは、ドライバーの[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)コールバック関数 (存在する) 場合、PnP マネージャーがデバイスに割り当てられているハードウェア リソースの一覧を渡します。

2.  フレームワークは、ドライバーの[ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799) (存在する) 場合、コールバック関数。

3.  フレームワークは、すべてのデバイスの電源管理対象の I/O キューを再起動します。

4.  場合は、ドライバーは、自己管理型の I/O を使用して、フレームワークのドライバーの[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff556785)コールバック関数。

次の手順を示す図を表示するには、次を参照してください。[デバイスで、ユーザーのプラグ](a-user-plugs-in-a-device.md)します。

 

 






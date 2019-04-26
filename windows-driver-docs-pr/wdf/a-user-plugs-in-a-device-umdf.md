---
title: ユーザーがデバイスを接続する
description: ユーザーがデバイスを接続する
ms.assetid: 1968270b-ce57-4a8c-8b7a-bbd4a972435d
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスに接続します。
- WDK UMDF デバイスのシナリオで接続します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec90d539a15c59a2dad36a4fdff0b6bcd9eb0b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342155"
---
# <a name="a-user-plugs-in-a-device"></a>ユーザーがデバイスを接続する


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスをユーザーが接続されるときにフレームワークは UMDF ドライバーの PnP および電源管理のコールバック メソッドが到着したデバイスから、次の順序では、図の下部にある状態します。

![umdf ドライバーのデバイス列挙し、スタートアップ シーケンス](images/umdf-powerup-sequence.png)

フレームワークを呼び出してドライバーの開始[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)コールバック、ドライバーは、デバイス コールバック オブジェクトと、デバイスを表す framework デバイス オブジェクトを作成できるようにします。 フレームワークでは、ドライバーのコールバック ルーチンを呼び出すことによって、デバイスは稼働までのシーケンスを経由の進行が続行されます。

フレームワークは、UMDF 関数またはフィルター ドライバーごと、一度に 1 つのドライバーをドライバー スタックの最下位レベルである driver 以降では、デバイスをサポートするには、このシーケンスを処理します。

 

 






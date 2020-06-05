---
title: ユーザーがデバイスを接続する
description: ユーザーがデバイスを接続する
ms.assetid: 1968270b-ce57-4a8c-8b7a-bbd4a972435d
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスの接続
- デバイスシナリオでのプラグイン WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64c5ccdaa14cdee12c6250133683dc0ba1b79745
ms.sourcegitcommit: c6040377fd6dd99031e4085a60ffbab4e1052dc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84421381"
---
# <a name="a-user-plugs-in-a-device"></a>ユーザーがデバイスを接続する


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ユーザーがデバイスに接続すると、フレームワークは、次の順序で UMDF ドライバーの PnP および電源管理コールバックメソッドを呼び出します。これは、図の下部にあるデバイスが到着した状態から始まります。

![umdf ドライバーのデバイス列挙とスタートアップシーケンス](images/umdf-powerup-sequence.png)

このフレームワークは、まずドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバックを呼び出して、ドライバーがデバイスコールバックオブジェクトと、デバイスを表すフレームワークデバイスオブジェクトを作成できるようにします。 フレームワークは、デバイスが動作するまで順番を進めることで、ドライバーのコールバックルーチンの呼び出しを続けます。

フレームワークは、デバイスをサポートする各 UMDF 関数またはフィルタードライバーに対して、ドライバースタックで最も低いドライバーを使用して、一度に1つのドライバーを処理します。

 




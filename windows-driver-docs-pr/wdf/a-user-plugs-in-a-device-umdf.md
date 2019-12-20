---
title: ユーザーがデバイスを接続する
description: ユーザーがデバイスを接続する
ms.assetid: 1968270b-ce57-4a8c-8b7a-bbd4a972435d
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスの接続
- デバイスシナリオでのプラグイン WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a5c2b8336d3763cb5e11d0fb87f267d5113f323
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210078"
---
# <a name="a-user-plugs-in-a-device"></a>ユーザーがデバイスを接続する


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ユーザーがデバイスに接続すると、フレームワークは、次の順序で UMDF ドライバーの PnP および電源管理コールバックメソッドを呼び出します。これは、図の下部にあるデバイスが到着した状態から始まります。

![umdf ドライバーのデバイス列挙とスタートアップシーケンス](images/umdf-powerup-sequence.png)

このフレームワークは、まずドライバーの[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバックを呼び出して、ドライバーがデバイスコールバックオブジェクトと、デバイスを表すフレームワークデバイスオブジェクトを作成できるようにします。 フレームワークは、デバイスが動作するまで順番を進めることで、ドライバーのコールバックルーチンの呼び出しを続けます。

フレームワークは、デバイスをサポートする各 UMDF 関数またはフィルタードライバーに対して、ドライバースタックで最も低いドライバーを使用して、一度に1つのドライバーを処理します。

 

 






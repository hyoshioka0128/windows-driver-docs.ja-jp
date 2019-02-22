---
title: フレームワークの I/O キュー オブジェクト
description: フレームワークの I/O キュー オブジェクト
ms.assetid: b343c61a-8252-4e46-9013-bef29d9ec360
keywords:
- UMDF オブジェクト WDK、I/O の queue オブジェクトします。
- フレームワークは、WDK UMDF、I/O キューのオブジェクトをオブジェクトします。
- I/O キュー オブジェクト WDK UMDF
- IWDFIoQueue
- queue オブジェクトは WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d330be2bb9ada0d0c3844d421523e1c674379f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559749"
---
# <a name="framework-io-queue-object"></a>フレームワークの I/O キュー オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework I/O キュー オブジェクトが、ドライバーに公開される、 [IWDFIoQueue](https://msdn.microsoft.com/library/windows/hardware/ff558943)インターフェイス。 I/O 要求のコンテナーは、I/O キューを表します。 I/O キューをドライバーに要求のフローを制御します。 I/O 要求が到着するは、適切なキューに配置されます。 I/O キューのオブジェクトの子である[UMDF デバイス オブジェクト](framework-device-object.md)します。 ドライバーを呼び出すことができます、 [ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020) I/O キューのオブジェクトを作成します。 呼び出しで**IWDFDevice::CreateIoQueue**ドライバーは、キューが、既定のキューであるかどうかを指定できます。

ドライバーは、I/O キューを作成するときに、ドライバーへの要求の配信を制御するディスパッチ モデルを指定します。 詳細については、次を参照してください。 [I/O キューのディスパッチ モードを構成する](configuring-dispatch-mode-for-an-i-o-queue.md)します。

ドライバーは、I/O キューを作成するときに、インターフェイスに関連するイベントが発生した場合、ドライバーに通知するフレームワークから呼び出されるコールバック関数のインターフェイスを提供できます。 詳細については、次を参照してください。 [I/O キュー イベントのコールバック関数](i-o-queue-event-callback-functions.md)します。

 

 






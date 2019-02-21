---
title: バス ドライバー AddDevice ルーチン
description: バス ドライバー AddDevice ルーチン
ms.assetid: 70af7116-2f29-4d77-a6d5-c1e0417e6f81
keywords:
- バス ドライバー WDK カーネル
- AddDevice ルーチンの WDK カーネル、バス ドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1319496fd8c4bde1840c9ece931223f1ed1d85ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531103"
---
# <a name="adddevice-routines-in-bus-drivers"></a>バス ドライバー AddDevice ルーチン





PnP バス ドライバーには、 *AddDevice*ルーチンが、これは、バス ドライバーは、そのコント ローラーまたはアダプターの機能のドライバーとして機能しているときに呼び出されます。 たとえば、PnP マネージャーでは、USB ハブ バス ドライバーの*AddDevice*ルーチンをハブのデバイスを追加します。 ハブのドライバーの*AddDevice*ルーチンは、hub (ハブに接続するデバイス) の子に対しては呼び出されません。

 

 





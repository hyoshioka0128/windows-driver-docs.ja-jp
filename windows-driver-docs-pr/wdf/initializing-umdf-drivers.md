---
title: UMDF ドライバーの初期化
description: UMDF ドライバーの初期化
ms.assetid: b21ec019-1a80-4219-8aa8-3545ec3383b9
keywords:
- ユーザーモードドライバーフレームワーク WDK、ドライバーの初期化
- UMDF WDK, ドライバーの初期化
- ユーザーモードドライバー WDK UMDF、初期化
- ドライバーの初期化 WDK UMDF
- リフレクター WDK UMDF
- リフレクター WDK UMDF を読み込んでいます
- ドライバーホストプロセス WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cc52ae8cbb8632056be8ab806be1742f9451a28
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210044"
---
# <a name="initializing-umdf-drivers"></a>UMDF ドライバーの初期化


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

デバイスの UMDF ドライバーが初期化される前に、ドライバーマネージャーとリフレクターがオペレーティングシステムによって読み込まれ、ドライバーのホストプロセスが作成されます。 デバイスが正常に開始されるようにするために、ドライバーマネージャーが読み込まれ、リフレクターが初期化されるときに完全に初期化されます。

デバイスがインストールされている場合は、プラグアンドプレイ (PnP) サブシステムによってリフレクタが読み込まれます (まだ読み込まれていない場合)。 次に、リフレクターはドライバーマネージャーに問い合わせて、ドライバーホストプロセスを作成します。 新しく作成されたドライバーホストプロセス内のフレームワークは、まだ初期化されていない場合に、UMDF ドライバーを初期化するために、 [**Idriverentry:: OnInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-oninitialize)メソッドを呼び出します。

フレームワークは、ドライバーホストプロセスに読み込まれた各デバイスの新しいデバイスオブジェクトを追加します。 次のセクションでは、フレームワークが新しいデバイスを追加する方法について概要を説明し、詳細を示します。

-   [デバイスの追加の概要](adding-a-device-overview.md)
-   [デバイスの追加](adding-a-device.md)

 

 






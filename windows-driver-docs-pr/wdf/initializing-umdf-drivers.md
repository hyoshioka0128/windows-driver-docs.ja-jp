---
title: UMDF ドライバーの初期化
description: UMDF ドライバーの初期化
ms.assetid: b21ec019-1a80-4219-8aa8-3545ec3383b9
keywords:
- ユーザー モード ドライバー フレームワーク WDK は、ドライバーの初期化
- UMDF WDK、ドライバーの初期化
- ユーザー モード ドライバー WDK UMDF、初期化しています
- WDK UMDF ドライバーの初期化
- リフレクター WDK UMDF
- リフレクター WDK UMDF の読み込み
- ホストの WDK UMDF ドライバー プロセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a20f294192864106fceae48587ec8ba53e56bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371143"
---
# <a name="initializing-umdf-drivers"></a>UMDF ドライバーの初期化


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスの UMDF ドライバーが初期化される前に、ドライバー マネージャーと、reflector は、オペレーティング システムによって読み込まれ、ドライバーのホスト プロセスが作成されます。 デバイスを正常に、ドライバーを起動することを確認するには、マネージャーが読み込まれ、完全に初期化される時間、reflector を初期化します。

デバイスがインストールされているときに、プラグ アンド プレイ (PnP) サブシステム、reflector を読み込みます既に読み込まれていない場合。 次に、reflector、ドライバーのホスト プロセスを作成するドライバー マネージャーを接続します。 呼び出しを処理し、新しく作成されたドライバー ホスト内で、フレームワーク、 [ **IDriverEntry::OnInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-oninitialize)初期化されていない場合は、UMDF ドライバーを初期化します。

フレームワークは、各デバイス ドライバーのホスト プロセスに読み込まれた新しいデバイス オブジェクトを追加します。 次のセクションでは、概要を表示し、フレームワークが新しいデバイスを追加する方法の詳細を提供します。

-   [デバイスの概要を追加します。](adding-a-device-overview.md)
-   [デバイスを追加します。](adding-a-device.md)

 

 






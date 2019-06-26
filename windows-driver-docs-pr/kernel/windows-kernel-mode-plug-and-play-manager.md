---
title: Windows カーネルモード プラグ アンド プレイ マネージャー
description: Windows カーネルモード プラグ アンド プレイ マネージャー
ms.assetid: 43d06dbe-da66-4103-8be3-f27ff075a1b4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ce9ce5bbdfab223701b7d723d1c28bf890a80a32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374164"
---
# <a name="windows-kernel-mode-plug-and-play-manager"></a>Windows カーネルモード プラグ アンド プレイ マネージャー


プラグ アンド プレイ (PnP) がハードウェア テクノロジの組み合わせと、PC、デバイスを識別できるようにするソフトウェア手法がシステムに追加します。 PnP、システム構成を変更できますで、ユーザーからの入力をほとんどまたはまったくないです。 たとえば、USB ドライブを接続に、Windows がサム ドライブを検出し、ファイル システムに自動的に追加することができます。 ただし、これを行うには、ハードウェアが特定の要件を従う必要があります、ため、ドライバー必要があります。

詳細については、ドライバーの PnP を参照してください[プラグ アンド プレイ](implementing-plug-and-play.md)します。

PnP マネージャーは、実際には、I/O マネージャーのサブシステムです。 I/O マネージャーの詳細については、次を参照してください。 [Windows カーネル モードの I/O マネージャー](windows-kernel-mode-i-o-manager.md)します。

PnP ルーチンの一覧は、次を参照してください。[プラグ アンド プレイ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

PnP マネージャーに直接インターフェイスを提供するルーチンがないことに注意してください。つまりはありません"**Pp**"ルーチン。

Windows Driver Frameworks (WDF) は、一連の PnP 管理を容易になるようにライブラリを提供します。 WDF の詳細については、次を参照してください。[カーネル モード ドライバー フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)します。

 

 





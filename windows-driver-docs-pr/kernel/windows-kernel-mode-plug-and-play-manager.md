---
title: Windows カーネル モードのプラグ アンド プレイ マネージャー
description: Windows カーネル モードのプラグ アンド プレイ マネージャー
ms.assetid: 43d06dbe-da66-4103-8be3-f27ff075a1b4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e18d7d041d8ab26f7914165a88f0fe2c904b716a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539448"
---
# <a name="windows-kernel-mode-plug-and-play-manager"></a>Windows カーネル モードのプラグ アンド プレイ マネージャー


プラグ アンド プレイ (PnP) がハードウェア テクノロジの組み合わせと、PC、デバイスを識別できるようにするソフトウェア手法がシステムに追加します。 PnP、システム構成を変更できますで、ユーザーからの入力をほとんどまたはまったくないです。 たとえば、USB ドライブを接続に、Windows がサム ドライブを検出し、ファイル システムに自動的に追加することができます。 ただし、これを行うには、ハードウェアが特定の要件を従う必要があります、ため、ドライバー必要があります。

詳細については、ドライバーの PnP を参照してください[プラグ アンド プレイ](implementing-plug-and-play.md)します。

PnP マネージャーは、実際には、I/O マネージャーのサブシステムです。 I/O マネージャーの詳細については、[Windows カーネル モードの I/O マネージャー](windows-kernel-mode-i-o-manager.md)を参照してください。

PnP ルーチンの一覧は、[プラグ アンド プレイ ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff558809)を参照してください。

PnP マネージャーに直接インターフェイスを提供するルーチンがないことに注意してください。つまりはありません"**Pp**"ルーチン。

Windows Driver Frameworks (WDF) は、一連の PnP 管理を容易になるようにライブラリを提供します。 WDF の詳細については、[カーネル モード ドライバー フレームワークの概要](https://msdn.microsoft.com/library/windows/hardware/ff544296)を参照してください。

 

 





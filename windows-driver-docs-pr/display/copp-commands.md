---
title: COPP コマンド
description: COPP コマンド
ms.assetid: c745b7d9-be59-45f9-90f5-0a7ecef0a292
keywords:
- コピー防止 WDK COPP、コマンド
- ビデオコピー防止 WDK COPP、コマンド
- COPP WDK DirectX VA、コマンド
- protected video WDK COPP、コマンド
- コマンド WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6578507440d81690ee5f35dd3c58d4142c420f0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839037"
---
# <a name="copp-commands"></a>COPP コマンド


## <span id="ddk_copp_command_gg"></span><span id="DDK_COPP_COMMAND_GG"></span>


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

ビデオミニポートドライバーは、DirectX VA COPP デバイスに関連付けられている物理コネクタに対して操作を実行する要求を受け取ることができます。 ビデオミニポートドライバーの[*coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数には、実行する操作を指定する[**DXVA\_coppcommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand)構造体へのポインターが渡されます。 DXVA\_COPPCommand の**guidCommandID**および**commanddata**メンバーは、操作を指定します。 次の操作がサポートされています。

-   [保護レベルの設定](setting-the-protection-level.md)

-   [シグナルを保護する方法を指示する](instructing-how-to-protect-the-signal.md)

 

 






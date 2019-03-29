---
title: COPP コマンド
description: COPP コマンド
ms.assetid: c745b7d9-be59-45f9-90f5-0a7ecef0a292
keywords:
- コピー防止 WDK COPP、コマンド
- ビデオのコピー防止 WDK COPP、コマンド
- COPP WDK DirectX va なので、コマンド
- ビデオの WDK COPP、コマンドの保護
- WDK COPP コマンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28d5e6f35252a79b2c5475d6af8b81e6df56465b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574248"
---
# <a name="copp-commands"></a>COPP コマンド


## <span id="ddk_copp_command_gg"></span><span id="DDK_COPP_COMMAND_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

ビデオのミニポート ドライバーでは、DirectX VA COPP デバイスに関連付けられた物理コネクタに対して操作を実行する要求を受信できます。 ビデオのミニポート ドライバーの[ *COPPCommand* ](https://msdn.microsoft.com/library/windows/hardware/ff539642)関数へのポインターを渡される、 [ **DXVA\_COPPCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff563141)構造体実行する操作を指定します。 **GuidCommandID**と**CommandData**の DXVA メンバー\_COPPCommand が操作を指定します。 次の操作がサポートされています。

-   [保護レベルの設定](setting-the-protection-level.md)

-   [シグナルを保護する方法を指示します。](instructing-how-to-protect-the-signal.md)

 

 






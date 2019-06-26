---
title: 信号の保護方法の指示
description: 信号の保護方法の指示
ms.assetid: d55a3660-5b7c-43e9-b1c5-b61f8b997a1a
keywords:
- コピー保護 WDK COPP、シグナルの保護
- ビデオのコピー防止 WDK COPP、シグナルの保護
- COPP WDK DirectX va なので、シグナルの保護
- ビデオの WDK COPP、シグナルの保護が保護されています。
- シグナル保護 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f63729ecaa99487f5d4cc66f6a918803bb3a98d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379897"
---
# <a name="instructing-how-to-protect-the-signal"></a>信号の保護方法の指示


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

COPP コマンドでは、DirectX VA COPP デバイスに関連付けられた物理コネクタを通過する信号を保護する方法に関する指示を提供できます。 シグナル保護まで、ビデオのミニポート ドライバーの設定に[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数へのポインターを受け取る、 [ **DXVA\_COPPCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppcommand)構造体、 **guidCommandID**メンバーは、DXVA に設定\_COPPSetSignaling GUID と**CommandData**メンバーへのポインターに設定する[ **DXVA\_COPPSetSignalingCmdData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppsetsignalingcmddata)信号を保護する方法を指定する構造体。

 

 






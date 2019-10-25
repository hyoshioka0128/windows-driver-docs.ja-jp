---
title: 信号の保護方法の指示
description: 信号の保護方法の指示
ms.assetid: d55a3660-5b7c-43e9-b1c5-b61f8b997a1a
keywords:
- コピー防止 WDK COPP、シグナル保護
- ビデオコピー防止 WDK COPP、signal protection
- COPP WDK DirectX VA、シグナル保護
- 保護されたビデオ WDK COPP、シグナル保護
- シグナル保護 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4697f60565483f682f466a6a11bedc103f1c644f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840361"
---
# <a name="instructing-how-to-protect-the-signal"></a>信号の保護方法の指示


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

COPP コマンドは、DirectX VA COPP デバイスに関連付けられている物理コネクタを通過する信号を保護する方法についての指示を提供します。 シグナル保護を設定するために、ビデオミニポートドライバーの[*coppcommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数は、 **GUIDCOMMANDID**メンバーが DXVA\_COPPSETシグナリング GUID に設定された[**DXVA\_coppcommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppcommand)構造体へのポインターを受け取り、 **CommandData**メンバーが、シグナルの保護方法を指定する[**DXVA\_COPPSetSignalingCmdData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppsetsignalingcmddata)構造体へのポインターに設定されています。

 

 






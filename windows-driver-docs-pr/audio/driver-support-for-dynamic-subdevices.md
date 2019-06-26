---
title: 動的なサブデバイス用のドライバーのサポート
description: 動的なサブデバイス用のドライバーのサポート
ms.assetid: ca355dfc-46ad-4df2-ac48-f3a0780dc3d3
keywords:
- 動的なオーディオ サブデバイス WDK オーディオ
- 動的トポロジ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d7d124b9c69afa3aad725848a607538616e3311
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360105"
---
# <a name="driver-support-for-dynamic-subdevices"></a>動的なサブデバイス用のドライバーのサポート


コード例で[サブデバイス作成](subdevice-creation.md)を使用する方法を示しています、 **PcRegisterSubdevice**ルーチンをサブデバイスを登録します。 SB16 サンプル オーディオ ドライバー、Windows Driver Kit (WDK) では、使用する方法を示します、 **PcRegisterPhysicalConnection**サブデバイス同じのオーディオのアダプターに含まれている間の物理接続を登録するルーチン。

[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)と[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)インターフェイス補完、PcRegister*Xxx*ルーチン。 これらのインターフェイスは、ドライバーのサンプルを使用して、PcRegister への呼び出しによって以前登録されたデバイスの"登録"を解除するメソッドを含む*Xxx*ルーチン。 前述のように、これら 2 つのインターフェイスは Windows Server 2003 SP1 以降および Windows XP sp2、Windows の以前のバージョンではなくで使用できます。 したがって、以前の Windows バージョンは動的なトポロジのサポートを使用してホット フィックス パッケージを Windows Server 2003、Windows XP、および Windows 2000 を使用できますが、動的のトポロジのサポートが不足しています。

 

 





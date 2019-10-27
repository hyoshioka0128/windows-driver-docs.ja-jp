---
title: 動的なサブデバイス用のドライバーのサポート
description: 動的なサブデバイス用のドライバーのサポート
ms.assetid: ca355dfc-46ad-4df2-ac48-f3a0780dc3d3
keywords:
- 動的オーディオサブデバイス WDK オーディオ
- 動的トポロジ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc7cfb682404a8e68cb461e26854f0c10ac07c04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833809"
---
# <a name="driver-support-for-dynamic-subdevices"></a>動的なサブデバイス用のドライバーのサポート


[サブデバイス作成](subdevice-creation.md)のコード例では、 **pcregiのサブデバイス**ルーチンを使用してサブデバイスを登録する方法を示しています。 Windows Driver Kit (WDK) の SB16 sample audio driver は、 **Pcregiphysicalconnection**ルーチンを使用して、同じオーディオアダプターに含まれるサブデバイス間に物理接続を登録する方法を示しています。

[Iunregistersubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)インターフェイスと[Iunregistersubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)インターフェイスは、pcregisterルーチンを補完します。 これらのインターフェイスには、事前に PcRegister*Xxx*ルーチンの呼び出しによって登録されたデバイスの "登録を解除する" ためにサンプルドライバーが使用するメソッドが含まれています。 前述のように、これら2つのインターフェイスは、Windows Server 2003 SP1 以降および Windows XP SP2 で利用できますが、以前のバージョンの Windows では使用できません。 このため、以前のバージョンの Windows では動的トポロジがサポートされていませんが、Windows Server 2003、Windows XP、および Windows 2000 では、動的トポロジをサポートするホットフィックスパッケージを使用できます。

 

 





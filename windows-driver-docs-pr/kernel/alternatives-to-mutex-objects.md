---
title: ミュー テックス オブジェクトの代替
description: ミュー テックス オブジェクトの代替
ms.assetid: c3b78155-426a-449d-8678-5666a7a12cbd
keywords:
- カーネルのディスパッチャー オブジェクト WDK、ミュー テックス オブジェクト
- ディスパッチャー オブジェクト WDK カーネル、ミュー テックス オブジェクト
- ミュー テックス オブジェクトの WDK カーネル
- 高速なミュー テックス WDK カーネル
- 保護されたミュー テックス WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1109fc0c63923c954ac3ef43247e80a16bc72f69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369956"
---
# <a name="alternatives-to-mutex-objects"></a>ミュー テックス オブジェクトの代替


高速なミュー テックスと保護されたミュー テックスは、ミュー テックス オブジェクトの代わりとして使用できます。 高速なミュー テックスまたは保護されたミュー テックスを取得および解放、ミュー テックス オブジェクトよりも高速化が、次の制限があります。

-   ドライバーが使用することはできません、 [ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)または[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)ルーチンを高速または保護されたミュー テックスを待機します。 そのため、ドライバーを待機できません高速または保護されたミュー テックスとディスパッチャー オブジェクトを同時にします。

-   ドライバーは、高速または保護されたミュー テックスの再帰的を取得できません。 ドライバーが既に取得されている高速または保護されたミュー テックスを取得しようとすると、ドライバーにデッドロックが発生します。 ミュー テックス オブジェクトでは、ただし、獲得再帰的ができます。

高速で保護されたミュー テックスの詳細については、次を参照してください。[高速なミュー テックスと保護されたミュー テックス](fast-mutexes-and-guarded-mutexes.md)します。

 

 





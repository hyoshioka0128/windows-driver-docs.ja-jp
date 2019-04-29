---
title: クラッシュ ダンプと休止状態のサポート
description: クラッシュ ダンプと休止状態のサポート
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- クラッシュ ダンプ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 610511ead89eaf37ccfd68ebdbf2cf29b192402d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330316"
---
# <a name="crash-dump-and-hibernation-support"></a>クラッシュ ダンプと休止状態のサポート


Storport 仮想ミニポート ドライバーをサポートする必要があります、 [ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393) (SRB) 関数のコード SRB\_関数\_ダンプ\_ポインター。 DataBuffer SRB メンバーが指すミニポート ドライバーでは、この種類の SRB を受信すると、 [**ミニポート\_ダンプ\_ポインター** ](https://msdn.microsoft.com/library/windows/hardware/ff562247)構造体。 この SRB が、SRB のミニポート ドライバーから返された後にクラッシュ ダンプ データを保持するディスクを制御するために使用する仮想ミニポート ドライバーに送信される[ **HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396)ルーチン。

 

 





---
title: クラッシュ ダンプと休止状態のサポート
description: クラッシュ ダンプと休止状態のサポート
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- クラッシュ ダンプ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0340bb029588d6094487be86190c5f2c209e3910
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368324"
---
# <a name="crash-dump-and-hibernation-support"></a>クラッシュ ダンプと休止状態のサポート


Storport 仮想ミニポート ドライバーをサポートする必要があります、 [ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block) (SRB) 関数のコード SRB\_関数\_ダンプ\_ポインター。 DataBuffer SRB メンバーが指すミニポート ドライバーでは、この種類の SRB を受信すると、 [**ミニポート\_ダンプ\_ポインター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_miniport_dump_pointers)構造体。 この SRB が、SRB のミニポート ドライバーから返された後にクラッシュ ダンプ データを保持するディスクを制御するために使用する仮想ミニポート ドライバーに送信される[ **HwStorInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)ルーチン。

 

 





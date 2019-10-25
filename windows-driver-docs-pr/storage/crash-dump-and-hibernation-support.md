---
title: クラッシュ ダンプと休止状態のサポート
description: クラッシュ ダンプと休止状態のサポート
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- クラッシュダンプ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8f0aacf4662847cdb5038832dfa0c8738f58513
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844573"
---
# <a name="crash-dump-and-hibernation-support"></a>クラッシュ ダンプと休止状態のサポート


Storport 仮想ミニポートドライバーは、 [**SCSI\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) (SRB) 関数コード SRB\_関数\_\_ポインターをダンプするようにサポートしている必要があります。 ミニポートドライバーがこの種類の SRB を受信すると、DataBuffer SRB メンバーは[**ミニポート\_ダンプ\_ポインター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_miniport_dump_pointers)構造体を指します。 この SRB は、SRB がミニポートドライバーの[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)ルーチンからを返した後に、クラッシュダンプデータを保持するディスクを制御するために使用される仮想ミニポートドライバーに送信されます。

 

 





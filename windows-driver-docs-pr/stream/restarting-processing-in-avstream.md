---
title: AVStream での処理の再開
description: AVStream での処理の再開
ms.assetid: f60d4dbd-61e6-4ae2-aa43-9edc8f36c3ff
keywords:
- AVStream 処理の再開
- AVStream プロセスの再起動 (WDK)
- WDK AVStream の処理の再開
- 保留中のステータス WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f772fcee30e0d700014b93f184d47c27aae105dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844951"
---
# <a name="restarting-processing-in-avstream"></a>AVStream での処理の再開





次のいずれかの条件に該当する場合、AVStream は処理を停止します。

-   Pin 中心の環境では、pin で現在利用できるデータがありません。

-   フィルター中心の環境では、 [**kspin\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**FLAGS**メンバーが kspin\_フラグ\_フレームを設定していないため、\_の\_が必要\_\_処理中、処理を待機しているデータはありません。 既定では、このフラグは設定されていません。

-   ミニドライバーの処理ディスパッチコールバックルーチンは、フレームの可用性に関係なく、状態\_PENDING を返します。 ミニドライバーが[ピン中心](pin-centric-processing.md)の処理を実装しているか、[フィルター処理を中心](filter-centric-processing.md)とした処理を実装しているかによって、処理ディスパッチは[*avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)または[*avstrminifilterprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)のいずれかになることに注意してください。

AVStream は、新しいデータが以前の空のキューに到着したときに処理を開始します。 したがって、ミニドライバーの処理ディスパッチが、関連付けられたキューがいっぱいになったときに STATUS\_PENDING を返した場合、処理を再開するためにミニドライバーはで呼び出されません。 ミニドライバーが状態\_保留中に設定されている場合、ミニドライバーは[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)または[**KsFilterAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterattemptprocessing)を呼び出して処理を再開する必要があります。

ミニドライバーが実際にデータを処理しない場合は、処理ディスパッチから状態\_SUCCESS を返さないでください。 これにより、AVStream はすぐにミニドライバーを再び呼び出し、AVStream と処理ディスパッチの間に無限ループが発生します。

 

 





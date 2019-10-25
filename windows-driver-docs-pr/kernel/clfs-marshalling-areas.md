---
title: CLFS マーシャリング領域
description: CLFS マーシャリング領域
ms.assetid: 1153bcfd-43e9-43bd-b893-5ec044ea9584
keywords:
- WDK カーネルの共通ログファイルシステムマーシャリングの領域
- CLFS WDK カーネル、マーシャリング領域
- マーシャリング領域 WDK CLFS
- ログ i/o バッファー WDK CLFS
- ログ i/o バッファーの最大数 WDK CLFS
- メモリ割り当て (WDK CLFS)
- バッファー WDK CLFS
- レコードの追加 (WDK CLFS)
- 安定したストレージ WDK CLFS
- 揮発性メモリ WDK CLFS
- storage WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b3c0cae27f87d91ba4a251337406ebdb1dff8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828540"
---
# <a name="clfs-marshalling-areas"></a>CLFS マーシャリング領域





共通ログファイルシステム (CLFS) クライアントは、揮発性メモリの[*マーシャリング領域*](clfs-terminology.md#kernel-clfs-term-marshalling-area)にログレコードを追加します。 CLFS は、これらのレコードを定期的に安定したストレージに書き込みます。 マーシャリング領域は、ログ i/o バッファーのコレクションであり、それぞれが複数のログレコードを保持できます。 ログ i/o バッファーは、最近ストリームに書き込まれた (ただし、安定したストレージにフラッシュされていない可能性がある) レコードと、最近ストリームから読み取られたレコードを保持します。

マーシャリング領域を作成するには、 [**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)を呼び出します。この時点で、マーシャリング領域が使用するログ i/o バッファーのサイズと、それらのバッファーがページングプールと非ページプールのどちらにあるかを指定する必要があります。 マーシャリング領域内のすべてのログ i/o バッファーのサイズは同じであり、CLFS は、基になる安定したストレージメディアのセクターサイズの倍数であることを保証します。 つまり、CLFS は、要求されたサイズを取得し、必要に応じて、安定したストレージメディアとの間で i/o バッファーに互換性を持たせるように切り上げます。

CLFS は、必要に応じてログの i/o バッファーを割り当て、解放しますが、一度に割り当てることができる i/o バッファーの最大数を設定することもできます。 独自のバッファー割り当て関数と解放関数を提供するオプションもあります。

ログレコードを書き込むために一度に割り当てることができるログ i/o バッファーの最大数を指定するには、 **ClfsCreateMarshallingArea**関数の*cmaxwritebuffers*パラメーターを設定します。 バッファー数を制限すると、安定したストレージにフラッシュする頻度に影響します。バッファーが少なくなるほど、ログレコードを安定したストレージに頻繁に書き込む必要があります。 フラッシュの頻度を制御する必要がない場合は、 *Cmaxwritebuffers*を無限 (winbase. h で定義) に設定します。

ログレコードを読み取るために一度に割り当てることができるログ i/o バッファーの最大数を指定するには、 **ClfsCreateMarshallingArea**関数の*Cmaxreadbuffers*パラメーターを設定します。 割り当てられた読み取りバッファーの数を制御する必要がない場合は、 *Cmaxreadbuffers*を無限に設定します。

ログ i/o バッファーに対して独自のメモリ割り当てを行う場合は、独自の割り当て関数と解放関数を指すように、 **ClfsCreateMarshallingArea**関数の*pfnallocbuffer*パラメーターと*pfnallocbuffer*パラメーターを設定します。 次に、CLFS は、ログ i/o バッファーを作成または解放する必要があるときに、実際のメモリの割り当てと解放を実行する関数を呼び出します。

場合によっては、事前にマーシャリング領域に領域を予約することが必要になることがあります。 たとえば、10個のログレコードのセットを作成しようとしているときに、セット全体に十分な領域があることを確認する必要があるとします。 10個のレコードの領域を予約するには、レコードのサイズを保持する10要素配列を作成してから、その配列を*rgcbReservation*パラメーターの[**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)関数に渡します。 **ClfsReserveAndAppendLog**は、マーシャリング領域の領域を予約したり、ログレコードをストリームに追加したり、これらの両方をアトミックに処理したりする多目的関数です。 パラメーターを適切に設定することにより、 **ClfsReserveAndAppendLog**を呼び出して、実際にレコードをストリームに追加することなく、将来使用するための領域を予約できます。

 

 





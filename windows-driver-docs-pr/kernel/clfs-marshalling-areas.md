---
title: CLFS マーシャ リング領域
description: CLFS マーシャ リング領域
ms.assetid: 1153bcfd-43e9-43bd-b893-5ec044ea9584
keywords:
- 一般的なログ ファイル システムの WDK カーネルでは、領域をマーシャ リング
- CLFS WDK カーネルでは、領域をマーシャ リング
- WDK CLFS の領域をマーシャ リング
- ログの I/O バッファーの WDK CLFS
- ログの I/O の最大数は WDK CLFS をバッファー処理します。
- メモリ割り当て WDK CLFS
- WDK CLFS をバッファー処理します。
- WDK CLFS レコードを追加します。
- 安定したストレージ WDK CLFS
- 揮発性メモリ WDK CLFS
- 記憶域 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6202c5524e84a9bb4239c866643c694809d5f9d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553734"
---
# <a name="clfs-marshalling-areas"></a>CLFS マーシャ リング領域





Common Log File System (CLFS) クライアントへのログ レコードの追加、 [*領域をマーシャ リング*](clfs-terminology.md#kernel-clfs-term-marshalling-area)揮発性メモリは、CLFS は安定ストレージにそれらのレコードを定期的に書き込みます。 マーシャ リング領域は、それぞれがいくつかのログ レコードを保持できる、ログの I/O バッファーのコレクションです。 バッファーされている最近保留中のレコードのログの I/O ストリームに書き込まれます (ただし、場合によって、安定ストレージにフラッシュされません)、ストリームから読み取られた最近のレコードとします。

呼び出すことによって、マーシャ リング領域を作成する[ **ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)、ログ I/O のサイズのバッファーを指定する必要がある時にこれらのバッファーがかどうかであるおよびマーシャ リング領域が使用されますページまたは非ページ プール。 マーシャ リング領域内のすべてのログ I/O バッファーは、同じサイズと、CLFS によりサイズが、基になるの安定したストレージ メディア上のセクター サイズの倍数であるようになります。 CLFS は、要求されたサイズし、安定したストレージ メディアと互換性のある、I/O バッファーが必要になるとして切り上げます。

CLFS は、割り当ておよび、必要に応じて、ログ I/O バッファーを解放しますが、一度に 1 つ割り当てることができる I/O バッファーの最大数を設定するオプションがあります。 また、独自のバッファーの割り当てと解放の関数を提供するオプションがあります。

ログ レコードの書き込みの時点で割り当て可能なログの I/O バッファーの最大数を指定するには、設定、 *cMaxWriteBuffers*のパラメーター、 **ClfsCreateMarshallingArea**関数。 安定したストレージ; へのフラッシュの頻度に影響を与えるバッファーの数を制限します。少数のバッファーより多くの場合、安定したストレージにログ レコードを書き込まれなければなりません。 フラッシュの頻度を制御する必要がない場合は、設定*cMaxWriteBuffers*を INFINITE (Winbase.h で定義されている)。

ログ レコードを読み取るための 1 つの時点で割り当て可能なログの I/O バッファーの最大数を指定するには、設定、 *cMaxReadBuffers*のパラメーター、 **ClfsCreateMarshallingArea**関数。 割り当てられた読み取りバッファーの数を制御する必要がない場合は、設定*cMaxReadBuffers*を無限にします。

独自のログの I/O バッファー メモリの割り当てを行う場合は、設定、 *pfnAllocBuffer*と*pfnFreeBuffer*のパラメーター、 **ClfsCreateMarshallingArea**関数独自の割り当てと解放の関数を指すようにします。 CLFS は関数を呼び出して、作成またはログの I/O バッファーを解放する必要があるたびに、実際のメモリ割り当てと解放を実行します。

場合によっては、事前にマーシャ リング領域内の領域を予約する可能性があります。 たとえば、10 個のログ レコードのセットを作成しようとしているし、全体のマーシャ リング領域に十分な領域があることを確認することがわかっている場合があります。 10 個のレコードの領域を予約するの レコードのサイズを保持する 10 要素の配列を作成し、先の配列を渡す、 [ **ClfsReserveAndAppendLog** ](https://msdn.microsoft.com/library/windows/hardware/ff541723)で機能、 *rgcbReservation*パラメーター。 **ClfsReserveAndAppendLog**ストリームにログ レコードを追加またはものの両方をアトミックには、マーシャ リング領域の領域を確保する多目的関数です。 呼び出すことができます、パラメーターを適切に設定するには、 **ClfsReserveAndAppendLog**ストリームに実際にすべてのレコードを追加せずに将来使用するための領域を予約します。

 

 





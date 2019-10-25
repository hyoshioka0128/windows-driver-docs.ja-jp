---
title: ストリーム ミニドライバーの作成
description: ストリーム ミニドライバーの作成
ms.assetid: 83540dff-3774-4197-8ba1-d28e12b4e366
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、書き込み
- streaming ミニドライバー WDK Windows 2000 カーネル、書き込み
- ミニドライバー WDK Windows 2000 カーネルストリーミング、書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e0f8efce05454aa20a2de3822345bd227ef9981
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845142"
---
# <a name="writing-a-stream-minidriver"></a>ストリーム ミニドライバーの作成





Stream クラスドライバーの主な設計目標は、オペレーティングシステムの処理の両方を処理することです。これには、マルチプロセッサコンピューターのサポートの複雑さや、カーネルストリーミングセマンティクスのサポートなどが含まれます。 ミニドライバーは、実行する必要がある操作のデバイス固有の部分のみを処理する必要があります。 クラスドライバーは、ミニドライバーにメモリを割り当て、ミニドライバーが必要とする NT カーネルリソースのブックキーピングを実行します。また、必要に応じて、すべての同期の問題を処理します。

クラスドライバーは、ミニドライバーで提供される一連のコールバックを介してミニドライバーと通信します。 ストリーミングミニドライバーの作成作業のほとんどは、これらのコールバックを記述するときに行われます。

このドキュメントでは、ミニドライバーが提供する各種ルーチンを**Strminixxx**と呼びます。 ミニドライバーは、基になるハードウェアが実行できるさまざまな関数の数に応じて、各ルーチンの1つ以上のバージョンを提供することが必要になる場合があります。

ストリーミングドライバーは、通常、いくつかの異なるデータストリームをサポートできます。 たとえば、DVD プレーヤーでは、オーディオストリームとビデオストリームの両方が生成されます。 カーネルストリーミングのコンテキスト内では、データの各ストリームは[pin](ks-pins.md)で表されます。

Stream クラスドライバーは、ミニドライバーの各 pin を追跡します。 クラスドライバーの用語では、各 pin の種類は*ストリーム*です。 ピンの種類のようなストリームでは、複数のインスタンスが存在する場合があります。 ストリームは i/o 要求を受け取ることができるため、ドライバーは各ストリームにコールバックを提供する必要があります。

ミニドライバーが提供する必要があるルーチンは次のとおりです。 詳細については、リファレンスガイドで詳しく説明します。

**すべてのミニドライバーが提供するルーチン**

[*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)

[*StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)

[*StrMiniEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_event_routine)

[*StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)

**個々のストリームに対してミニドライバーが提供するルーチン**

[*StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)

[**StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85))

[*StrMiniEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_event_routine)

[*StrMiniClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_query_clock_routine)

ミニドライバーは、複数の異なるストリームに対して同じコールバックを使用することができます。 コールバックは、その代わりにパラメーターから呼び出されたストリームを特定できます。

ミニドライバーは、すべての WDM ドライバーと同様に、 **Driverentry**ルーチンも提供する必要があります。 ミニドライバーの**Driverentry**ルーチンの主なタスクは、ミニドライバーをクラスドライバーに登録することです。

クラスドライバーは、ミニドライバーの代わりにすべての i/o 要求を受信します。 要求を完了するために必要な情報を取得するために、クラスドライバーはストリーム要求ブロック (SRB) を作成し、その要求を**Strmini*XXX*パケット**ルーチンの1つに渡します。 クラスドライバーは、 [*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)ルーチンにデバイス全体の i/o 要求をディスパッチします。 このメソッドは、 [*StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) (カーネルストリームの読み取り要求と書き込み要求の場合) または[**StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85)) (他の要求の場合) に対する個々のストリームに要求を渡します。

通常、クラスドライバーは、要求をキューに置いて、一度に1つずつミニドライバーに渡します。 ミニドライバーは、必要に応じて独自の同期を行うことができます。ミニドライバーは、直ちに処理できない要求をキューに置いています。 詳細については、「[ミニドライバー Synchronization](minidriver-synchronization.md) 」を参照してください。

ミニドライバーは、ストリーム要求ブロックを操作するための2つの追加ルーチンを提供する必要があります。 クラスドライバーは、cancel IRP を受信したときに[*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)を呼び出し、特定のパケットをキャンセルするようにミニドライバーに指示する必要があります。 また、クラスドライバーは、ストリーム要求ブロックの処理を完了するためにミニドライバーが実行する時間を追跡します。 ミニドライバーの処理に時間がかかりすぎる場合、クラスドライバーは要求をタイムアウトし、ミニドライバーの[*Strminirequesttimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)ルーチンを呼び出します。

ハードウェアの割り込みが発生すると、オペレーティングシステムはクラスドライバーに通知します。その後、ミニドライバーの[*Strminiinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)ルーチンを呼び出して割り込みを処理します。

 

 





---
title: Stream ミニドライバーを作成します。
description: Stream ミニドライバーを作成します。
ms.assetid: 83540dff-3774-4197-8ba1-d28e12b4e366
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルでは、書き込み
- ミニドライバー WDK Windows 2000 のカーネルのストリーミング、書き込み
- ミニドライバー WDK Windows 2000 のカーネル ストリーム、書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50c00bcd9db95bd9e3ca27da17f8236685996e9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552129"
---
# <a name="writing-a-stream-minidriver"></a>Stream ミニドライバーを作成します。





ストリーム クラス ドライバーの主要な設計目標は、処理およびカーネル ストリーミング セマンティクスをサポートしているマルチプロセッサのコンピューターのサポートの複雑さを含むオペレーティング システムの両方の作業を処理するためにです。 任意の操作を実行する必要のデバイスに固有の部分のみを処理するミニドライバーが必要です。 クラス ドライバーは、ミニドライバーのメモリを割り当て、NT カーネル リソース、ミニドライバーは必要があり、(必要に応じて) すべての同期の問題を処理のブックキーピングを実行します。

クラス ドライバーは、一連のミニドライバーが指定したコールバックを通じてミニドライバーと通信します。 これらのコールバックの書き込みでのストリーミング ミニドライバーを作成する作業のほとんどが発生します。

このドキュメントでとしてミニドライバーで提供されるルーチンの種類ごとに言及**StrMiniXxx**します。 ミニドライバーは、どのように多くの異なる機能、基になるハードウェアを実行できるによって各ルーチンの 1 つまたは複数のバージョンを提供する必要があります。

ストリーミングのドライバーは通常、データのいくつかの異なるストリームをサポートできます。 たとえば、DVD プレーヤーは、オーディオとビデオ ストリームの両方を生成します。 によって表されるデータの各ストリームのカーネルのストリーミングは、コンテキスト内で、 [pin](ks-pins.md)します。

ストリーム クラス ドライバーは、ミニドライバー上の各ピンを追跡します。 クラスのドライバーの用語、暗証番号 (pin) の種類ごとでは、*ストリーム*します。 などのストリームの種類をピン留め、複数のインスタンスがあります。 ストリームは、I/O 要求を受信できる、ので、ドライバーは、各ストリームのコールバックを指定する必要があります。

次に示します、ルーチン、ミニドライバーは、提供する必要があります。 以下およびリファレンス ガイドより詳細に説明が。

**すべてのミニドライバーは、ルーチン**

[*StrMiniCancelPacket*](https://msdn.microsoft.com/library/windows/hardware/ff568448)

[*StrMiniReceiveDevicePacket*](https://msdn.microsoft.com/library/windows/hardware/ff568463)

[*StrMiniRequestTimeout*](https://msdn.microsoft.com/library/windows/hardware/ff568473)

[*StrMiniEvent*](https://msdn.microsoft.com/library/windows/hardware/ff568457)

[*StrMiniInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff568459)

**ルーチン、ミニドライバーは、それぞれ個別のストリームを提供します**

[*StrMiniReceiveStreamDataPacket*](https://msdn.microsoft.com/library/windows/hardware/ff568470)

[**StrMiniReceiveStreamControlPacket**](https://msdn.microsoft.com/library/windows/hardware/ff568467)

[*StrMiniEvent*](https://msdn.microsoft.com/library/windows/hardware/ff568457)

[*StrMiniClock*](https://msdn.microsoft.com/library/windows/hardware/ff568452)

いくつかの異なるストリームに、同じコールバックを使用するミニドライバーのことができます。 コールバックは、パラメーターから呼び出された対象のストリームを判断できます。

ミニドライバー、WDM ドライバーをすべてのようにも指定する必要あります、 **DriverEntry**ルーチン。 主なタスク、 **DriverEntry**ミニドライバーのルーチンは、クラス ドライバーを使用した、ミニドライバーを登録します。

クラス ドライバーは、ミニドライバーの代わりにすべての I/O 要求を受信します。 要求の完了に必要な情報を取得するクラス ドライバー ストリーム要求のブロック (SRB) をビルドし、いずれかに渡されます、 **StrMini*XXX*パケット**ルーチン。 クラス ドライバーを全体として、デバイスへの I/O 要求のディスパッチ、 [ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)ルーチン。 要求に個別のストリームに渡す、 [ *StrMiniReceiveStreamDataPacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568470) (ストリーミング カーネルは、読み取りおよび書き込み要求) についてまたは[ **StrMiniReceiveStreamControlPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff568467) (他の要求)。

通常、クラス ドライバー、その要求をキューを 1 つずつに渡します、ミニドライバーします。 ミニドライバーは、独自の同期を行うことができます必要に応じてミニドライバーはすぐに処理できない要求をキュー責任を負います。 参照してください[ミニドライバー同期](minidriver-synchronization.md)詳細についてはします。

ミニドライバーは、ストリーム要求のブロックを操作するため、2 つの追加ルーチンを提供する必要があります。 クラスのドライバー呼び出し[ *StrMiniCancelPacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568448)とキャンセル IRP を受信して、特定のパケットをキャンセルするミニドライバーを指示する必要があります。 クラスのドライバーもの追跡、ミニドライバーでストリーム要求のブロックの処理を完了にかかる時間。 クラスのドライバーが、要求がタイムアウトし、呼び出すようにミニドライバーのミニドライバーは時間がかかりすぎる場合[ *StrMiniRequestTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff568473)ルーチン。

ハードウェアの割り込みが発生した、オペレーティング システムが、クラス ドライバーを通知する呼び出しミニドライバーの[ *StrMiniInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff568459)割り込みを処理するルーチン。

 

 





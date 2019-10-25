---
title: ミニドライバーの同期
description: ミニドライバーの同期
ms.assetid: 2f560e7a-4717-4b3f-9513-e34fcb2b5e6c
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、同期
- streaming ミニドライバー WDK Windows 2000 カーネル、同期
- ミニドライバー WDK Windows 2000 カーネルストリーミング、同期
- 同期 WDK streaming ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39b17c806dabb15200927baa5030b938a5bf72e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842132"
---
# <a name="minidriver-synchronization"></a>ミニドライバーの同期





Streaming ミニドライバーの開発者は、クラスドライバーが同期を処理できるようにするオプションがあります。 ミニドライバーをクラスドライバーに登録すると、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)の**TurnOffSynchronization**メンバーを**FALSE**に設定することによって、クラスドライバーによって提供される同期を選択できます。

クラスドライバーは同期を処理するときに、ミニドライバーコードの2つの部分が同時に実行されないようにします。 クラスドライバーは、すべてのストリーム要求をキューに置いて、一度に1つのミニドライバーに渡します。

この同期の1つの目的は、ミニドライバーライターが、マルチタスク、再入、マルチプロセッサ環境でのドライバーの同期と要求キューの詳細をすべて処理する必要がないようにすることです。 ただし、一部のミニドライバーでは使用しないでください。 同期の[例](synchronization-examples.md)として、同期に関してミニドライバーが行う必要があることを示す2つの例があります。

ストリームクラスの同期をオフにすると、すべての要求がすぐにミニドライバーに非同期に呼び出され、送信スレッドのコンテキストでパッシブ\_レベルで呼び出されます。 上記のルールの例外は、HwCancelPacket、TimeoutHandler、および Timer ルーチンです。 これらはディスパッチ\_レベルで呼び出されます。 最後の例外は、DIRQL で呼び出される割り込みハンドラーです。

同期がオフの場合、ミニドライバーは、WDM モデルに準拠して同期を実行する役割を担います。 ミニドライバーがパッシブ\_レベルでコールバックされると、Dpc や割り込みなどの上位の IRQL イベントによって割り込まれる可能性があります。 同様に、ディスパッチ\_レベルでミニドライバーがコールバックされた場合、その後割り込みによって割り込まれる可能性があります。 共有リソースを操作するミニドライバー関数は、アクセスを同期する必要があります。

ストリームクラスの同期がオフになっている場合は、複数の要求を同じストリームまたは異なるストリームに同時に発行できます。 ミニドライバーは、独自の要求をキューに置いて、他のスレッドと ISR とのハードウェアの同期を処理する必要があります。 スピンロック、ミューテックス、および[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)は、ストリームクラスの同期なしで実行される stream ミニドライバーで使用できる同期オブジェクトの一部です。

 

 





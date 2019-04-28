---
title: ピン中心の処理
description: ピン中心の処理
ms.assetid: 0b6a02c2-e672-4568-a890-491c721ec3a7
keywords:
- 暗証番号 (pin) を中心としたフィルター WDK AVStream
- 暗証番号 (pin) を中心とした AVStream WDK をフィルター処理します。
- WDK AVStream の種類をフィルターします。
- AVStrMiniPinProcess
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c620769f218553577cedd85accf4b4bdbefcc3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362228"
---
# <a name="pin-centric-processing"></a>ピン中心の処理





2 つの処理パラダイムの 1 つを使用するフィルターを指定する、AVStream ミニドライバーを作成する場合: 暗証番号 (pin) を中心とした処理または[フィルターを中心とした処理](filter-centric-processing.md)します。

暗証番号 (pin) を中心とした処理は AVStream が新しいフレームがピン留めするキューに届いたときに、ミニドライバーの暗証番号 (pin) プロセスのディスパッチ ルーチンを呼び出すことを意味します。

フィルターを中心とした処理は AVStream がデータ フレームは使用可能なインスタンス化された各ピンの場合に、ミニドライバーのフィルター処理のディスパッチ ルーチンを呼び出すことを意味します。 これらの定義が既定の動作を指定することに注意してください。ミニドライバーはフラグを設定して、既定の動作を変更することができます、 [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。

一般に、ソフトウェアのフィルターがフィルターを中心とした処理を使用し、ハードウェア フィルターは、暗証番号 (pin) を中心とした処理を使用します。 たとえば、変換またはデータをレンダリングするハードウェアでは、暗証番号 (pin) を中心としたフィルターをデータを送信する可能性があります。 これらのロールが逆にしたまれなケースがあります。

暗証番号 (pin) を中心としたフィルターを指定する、ミニドライバーはへのポインターを提供します、 *AVStrMiniPinProcess*各コールバック ルーチン[ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)構造体処理のディスパッチを指定しない、 [ **KSFILTER\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff562554)構造体。

かどうか、ミニドライバーは、KSPIN フラグの設定を変更しません\_記述子\_AVStream がベンダーから提供されたを呼び出し構造、EX [ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)コールバック ルーチン次の 3 つの場合。

-   最小の処理状態にピン留めする遷移します。 フレームは、キューに既に存在する必要があり、暗証番号 (pin) する必要がありますからの切り替えに最低限の処理状態よりも小さい少なくとも最低限の処理状態です。

-   新しいフレームが到着します。 Pin に以上でなければなりません、最小の処理状態とフレームまたは前のリーディング エッジ必要があります。

-   ミニドライバーが明示的に呼び出す[ **KsPinAttemptProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff563494)します。

既定では、一時停止は、最小の処理状態です。

さらに、AVStream は呼び出しません暗証番号 (pin) プロセスのディスパッチ、pin の AND ゲートが閉じられました。 使用する場合、**KSGATE * * * Xxx*を追加するルーチンに pin の入力をオフのゲートなど、プロセス、ディスパッチは呼び出されません。

AVStream を呼び出すと*AVStrMiniPinProcess*、使用可能なデータを含む暗証番号 (pin) オブジェクトへのポインターを提供します。 ミニドライバーの処理のディスパッチを取得できます、[リーディング エッジ ポインター](leading-and-trailing-edge-stream-pointers.md)呼び出して[ **KsPinGetLeadingEdgeStreamPointer**](https://msdn.microsoft.com/library/windows/hardware/ff563513)します。 ミニドライバーが、データを使用してストリームを操作、[ストリーム ポインター](stream-pointers.md) API。

AVStream を呼び出すと、暗証番号 (pin) を中心とした処理を使用するミニドライバーは変更できます、 *AVStrMiniPinProcess*で関連するフラグを設定してディスパッチ[ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 フラグの説明、KSPIN で\_記述子\_リファレンス ページ EX、暗証番号 (pin) を中心としたフィルターを実装しているベンダーに特に関連します。

ミニドライバーが保持している場合は、試行の処理が失敗、[ミュー テックスを処理](processing-mutex-in-avstream.md)を通じて[ **KsPinAcquireProcessingMutex**](https://msdn.microsoft.com/library/windows/hardware/ff563488)します。 問題は、ミニドライバーを使用してのゲートを直接操作する場合にも発生する可能性、**KSGATE * * *\** 呼び出し。

[AVStream シミュレートされたハードウェア サンプル ドライバー (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083) Windows Driver Kit のサンプルでは、シミュレーションのハードウェア用のドライバーを暗証番号 (pin) を中心としたキャプチャします。 Avshws サンプルを実装する方法を示します[AVStream を通じて DMA](avstream-dma-services.md)します。

 

 





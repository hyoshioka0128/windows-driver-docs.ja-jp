---
title: ピン中心の処理
description: Pin 中心の処理
ms.assetid: 0b6a02c2-e672-4568-a890-491c721ec3a7
keywords:
- pin 中心のフィルター (WDK AVStream)
- AVStream pin 中心フィルター WDK
- フィルターの種類 WDK AVStream
- AVStrMiniPinProcess
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: d69d76534aff35568c25b96f580e6df06575d650
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073432"
---
# <a name="pin-centric-processing"></a>Pin 中心の処理

AVStream ミニドライバーを作成するときは、ピン中心の処理と[フィルター処理を中心](filter-centric-processing.md)とした処理の2つの処理パラダイムのいずれかを使用するフィルターを指定します。

ピン中心の処理とは、新しいフレームがピンキューに到着したときに AVStream がミニドライバーの pin プロセスディスパッチルーチンを呼び出すことを意味します。

フィルター中心の処理では、インスタンス化された各ピンで利用可能なデータフレームがある場合、AVStream はミニドライバーのフィルター処理ディスパッチルーチンを呼び出します。 これらの定義は既定の動作を指定することに注意してください。ミニドライバーは、 [**Kspin \_ 記述子 \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体でフラグを設定することによって、既定の動作を変更できます。

一般に、ソフトウェアフィルターはフィルター中心の処理とハードウェアフィルターを使用して、pin 中心の処理を使用します。 たとえば、データを変換またはレンダリングするハードウェアは、ピン中心のフィルターでデータをルーティングできます。 これらの役割が逆になる場合もまれにあります。

ピン中心のフィルターを提供するために、ミニドライバーは各[**Kspin \_ ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)構造体の*Avstrminipinprocess*コールバックルーチンへのポインターを提供します。 [**ksk フィルター \_ ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)構造体に処理ディスパッチを指定しないでください。

ミニドライバーが KSPIN 記述子 EX 構造体でフラグ設定を変更しない場合 \_ \_ 、avstream は、次の3つの状況でベンダーが提供する[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)コールバックルーチンを呼び出します。

- Pin は、最小処理状態に遷移します。 フレームは既にキューに存在している必要があります。また、ピンは、最小処理状態から最小処理状態に移行する必要があります。

- 新しいフレームが到着します。 Pin は、少なくとも最小処理状態である必要があります。また、先頭のエッジの前または前にフレームがなければなりません。

- ミニドライバーは、明示的に[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)を呼び出します。

既定では、pause は最小処理状態です。

また、ピンのおよびゲートが閉じている場合、AVStream は、ピンプロセスディスパッチを呼び出しません。 **Ksk ゲート**_Xxx_ルーチンを使用して、pin のおよびゲートに入力以外の入力を追加すると、プロセスディスパッチは呼び出されません。

AVStream は*Avstrminipinprocess*を呼び出すと、使用可能なデータを持つピンオブジェクトへのポインターを提供します。 ミニドライバーの処理ディスパッチは、 [**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出すことによって、[先頭のエッジポインター](leading-and-trailing-edge-stream-pointers.md)を取得できます。 ミニドライバーは、[ストリームポインター](stream-pointers.md) API を使用してストリームデータを操作します。

ピン中心の処理を使用するミニドライバーは、AVStream が*Avstrminipinprocess*ディスパッチを呼び出すときに、関連する[**kspin \_ DESCRIPTOR \_ EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体でフラグを設定することによって変更できます。 KSPIN 記述子 EX のリファレンスページのフラグの説明 \_ \_ は、ピン中心のフィルターを実装しているベンダーに特に関連しています。

ミニドライバーが[**KsPinAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquireprocessingmutex)を介して[処理ミューテックス](processing-mutex-in-avstream.md)を保持している場合、処理の試行が失敗することがあります。 ミニドライバーが**Ksk ゲート**呼び出しを使用してゲートを直接操作した場合にも、問題が発生する可能性があり _\*_ ます。

Windows Driver Kit のサンプルに含まれる Avstream のシミュレートされた[ハードウェアサンプルドライバー (AVSHwS)](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/)は、シミュレートされたハードウェア用のピン中心のキャプチャドライバーです。 Avshws サンプルは、 [AVStream を使用して DMA](avstream-dma-services.md)を実装する方法を示しています。

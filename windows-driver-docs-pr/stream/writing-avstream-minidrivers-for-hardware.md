---
title: ハードウェア用 AVStream ミニドライバーの作成
description: ハードウェア用 AVStream ミニドライバーの作成
ms.assetid: d7dc42d7-efd0-41ff-abab-d97c508a41e6
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- AVStrMiniDeviceStart
- フィルターグラフ WDK AVStream
- グラフ WDK AVStream
- グラフと WDK AVStream の間の干渉
- WDK AVStream のエンコード
- WDK AVStream をデコードしています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0bc22d1abc0399749de784eaf2768296c247ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844515"
---
# <a name="writing-avstream-minidrivers-for-hardware"></a>ハードウェア用 AVStream ミニドライバーの作成





ベンダーから提供された[*Avstrminidevicestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksdevicepnpstart)では、ハードウェアをサポートする avstream ミニドライバーはまずリソースリストを解析し、次に[**ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)を呼び出して、割り込みサービスルーチン (ISR) を登録する必要があります。

ドライバーがダイレクトメモリアクセス (DMA) をサポートしている場合は、追加の手順が必要です。 ドライバーが DMA を実装している場合は、「 [Avstream Dma サービス](avstream-dma-services.md)」を参照してください。

デバイスを使用して複数のアプリケーションが同時にフィルターグラフを作成する場合は、グラフ間の干渉を防ぐために注意する必要があります。 具体的には、デバイスを使用するアプリケーションでグラフを構築する場合、停止状態ではないデバイスを使用しているアプリケーションに干渉しないようにする必要があります。

グラフが KSK 状態に遷移した後にマイクロコードを読み込むことによって、干渉を回避できます\_取得します。 これにより、現在実行中のグラフが保護されます。これは、別のグラフが現在実行されている間に新しいグラフが Ksk 状態に移行して **\_取得**しないためです。 Pin 状態の変更の通知を受信するには、 [**Kspin\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)構造体に[*Avstrminipinsetdevicestate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)コールバックルーチンを指定します。

ただし、グラフの起動時間を最小限に抑えるには、グラフが KSSTATE\_取得する前にマイクロコードを読み込む必要があります。 この場合は、起動時に低優先度のバックグラウンドスレッドでマイクロコードを読み込むことを検討してください。 このソリューションは、他のアプリケーションと干渉したり、グラフの開始時間を短縮したりするわけではなく、非同期に実行する場合は起動時間を長くしないでください。

ただし、起動後、グラフが KSK 状態\_取得されるまで、マイクロコードを再読み込みしたり、ハードウェアレジスタを操作したりしないでください。

新しいグラフの接続が実行中のグラフにどのように影響するかを確認するには、エンコードとデコードをサポートするビデオキャプチャデバイスを検討しますが、これらのタスクは一度に1つだけ実行します。 ミニドライバーは、エンコードフィルターとデコードフィルターを公開します。

アプリケーションは、エンコードフィルターを含むフィルターグラフを構築します。 ミニドライバーは、pin 接続時にエンコード用のマイクロコードを読み込みます。 フィルターグラフが開始され、ハードウェアがエンコードを開始します。

ハードウェアがエンコードされている間、別のアプリケーションによってフィルターグラフにデコードフィルターが配置されます。 デコードピンが接続されているとき*に、ピンが状態を KSK 状態に変更\_取得する前に*、ミニドライバーはハードウェアをデコード用に構成しようとします。 この再構成により、現在アクティブなエンコードグラフが妨げられ、ドライバーが不安定になる可能性があります。

 

 





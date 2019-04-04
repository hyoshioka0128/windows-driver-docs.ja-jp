---
title: ハードウェアの AVStream ミニドライバーの書き込み
description: ハードウェアの AVStream ミニドライバーの書き込み
ms.assetid: d7dc42d7-efd0-41ff-abab-d97c508a41e6
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- AVStrMiniDeviceStart
- WDK AVStream のグラフをフィルター処理します。
- WDK AVStream のグラフ
- グラフ WDK AVStream の間で干渉
- WDK AVStream のエンコード
- WDK AVStream のデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9b539cd100ecdc94ec320bff8f103d74638ef0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551767"
---
# <a name="writing-avstream-minidrivers-for-hardware"></a>ハードウェアの AVStream ミニドライバーの書き込み





ベンダーから提供されたで[ *AVStrMiniDeviceStart*](https://msdn.microsoft.com/library/windows/hardware/ff556297)、AVStream ミニドライバー ハードウェアをサポートする必要があります最初に、リソースの一覧を解析し、呼び出す[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)割り込みサービス ルーチン (ISR) を登録します。

ドライバーは、ダイレクト メモリ アクセス (DMA) をサポートしている場合、追加の手順が必要です。 ドライバーは、DMA を実装する場合は、[AVStream DMA サービス](avstream-dma-services.md)を参照してください。

1 つ以上のアプリケーションでは、デバイスを同時に使用するフィルター グラフをビルド可能性がある場合、は、グラフ間の干渉を防ぐために考慮する必要があります。 具体的には、デバイスを使用してアプリケーションにグラフを作成している場合をする必要がありますに干渉しない非停止状態で、デバイスを使用するアプリケーション。

干渉 KSSTATE にグラフの遷移後マイクロ コードを読み込むことによって回避できます\_取得します。 新しいグラフに移行しないため、現在実行中のグラフを保護するこのは**KSSTATE\_ACQUIRE**もう 1 つのグラフが現在実行中にします。 暗証番号 (pin) の状態の変更の通知を受信するには、指定、 [ *AVStrMiniPinSetDeviceState* ](https://msdn.microsoft.com/library/windows/hardware/ff556359)コールバック ルーチンで、 [ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)構造体。

グラフのスタートアップ時間を最小限に抑えるには、ただし、たい場合があります、グラフ KSSTATE に達する前に、マイクロ コードを読み込む\_取得します。 この場合、起動中に優先度の低いバック グラウンド スレッドでのマイクロ コードの読み込みを検討してください。 このソリューションは他のアプリケーションに影響しない、グラフの開始時間が削減され、非同期的に完了とブート時間が長引いていない必要があります。

起動後、ただし、マイクロ コードを再読み込みしたりしないでグラフ KSSTATE に到達するまで、ハードウェア レジスタを操作\_取得します。

新しいグラフの接続が実行されているグラフに干渉する方法については、エンコーディングとデコーディングをサポートしますが、のみこれらのタスクのいずれかを一度に実行するビデオ キャプチャ デバイスを検討してください。 ミニドライバーは、フィルターをエンコードおよびデコード フィルターを公開します。

アプリケーションでは、エンコードのフィルターを含むフィルター グラフを作成します。 ミニドライバーは、暗証番号 (pin) の接続時にエンコードするためのマイクロ コードを読み込みます。 フィルターのグラフを起動し、ハードウェアがエンコードを開始します。

ハードウェアのエンコード中に別のアプリケーションは、フィルターのグラフでデコード フィルターを配置します。 デコード ピンが接続しているときに*ピン KSSTATE に状態を変更する前に\_ACQUIRE*、ミニドライバーはデコードのハードウェアを構成しようとしています。 この再構成に干渉現在アクティブなグラフをエンコードし、ドライバーの不安定になる可能性があります。

 

 





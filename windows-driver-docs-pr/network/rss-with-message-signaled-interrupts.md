---
title: メッセージ シグナル割り込みを使用した RSS
description: メッセージ シグナル割り込みを使用した RSS
ms.assetid: 3c1776cf-f870-4910-88b2-9b5a9544cdf8
keywords:
- 受信側のスケーリングの WDK ネットワー キング、メッセージ シグナル割り込み
- ネットワーク接続、メッセージ シグナル割り込み RSS WDK
- メッセージ シグナル割り込み WDK ネットワー キング、RSS
- Msi WDK ネットワー キング、RSS
- MSI X WDK ネットワー キング、RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4b52008ecac2d926e367b7322f09b6e87863bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359768"
---
# <a name="rss-with-message-signaled-interrupts"></a>メッセージ シグナル割り込みを使用した RSS





ミニポート ドライバーがサポートできるメッセージ シグナル割り込み RSS のパフォーマンスを向上させるには、(Msi)。 Msi には、受信したデータを処理する CPU の割り込みを要求する NIC が有効にします。 MSI の NDIS サポートの詳細については、次を参照してください。 [NDIS Msi-x](ndis-msi-x.md)します。

次の図では、RSS MSI X を示しています。

![msi x で rss を示す図](images/rssmsistack.png)

図では、破線の矢印は、別の接続での処理を表します。 MSI x RSS は、NIC の接続の適切な cpu 使用率を中断できます。

各割り込みに対する次のプロセスが繰り返されます。

1.  NIC:
    1.  DMA を使用して、受信したデータをバッファーに入力します。

        ミニポート ドライバーでは、初期化中に、受信バッファーを共有メモリが割り当てられます。

    2.  ハッシュ値を計算します。
    3.  CPU にバッファー キューに配置し、ミニポート ドライバーにキューの割り当てを提供します。 たとえば、NIC がいくつかのパケットが受信した後、手順 1-3 と DMA CPU 割り当ての一覧をループでした。 特定のメカニズムは、NIC の設計にままです。
    4.  MSI X を使用して、空でないキューに関連付けられている CPU を中断します。

2.  NIC を追加できる入力バッファーを受信して、いつでも、キューに追加を中断しません、CPU もう一度ミニポート ドライバーは、その CPU の割り込みを有効になるまでです。

3.  NDIS ミニポート ドライバーの ISR の呼び出し ( [ *MiniportInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff559395)) 現在の CPU にします。

4.  ISR では、現在の CPU の割り込みを無効にし、現在の CPU の DPC キューに入れます。

    その他の Cpu で DPC が現在の CPU で実行されているときに、中断が発生することができますも。

5.  NDIS 呼び出し、 [ *MiniportInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559398)の DPC キューごとに機能します。 各 DPC:
    1.  ビルドでは、そのキュー内のすべての受信バッファー記述子を受信し、ドライバー スタック上のデータを示します。 詳細については、次を参照してください。 [RSS の受信データのことを示す](indicating-rss-receive-data.md)します。
    2.  現在の CPU の割り込みを有効にします。 この割り込みが完了し、プロセスが再び開始します。 その他の Dpc の進行状況を追跡するためにアトミック操作が必要ないことに注意してください。

 

 






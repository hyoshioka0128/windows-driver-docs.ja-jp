---
title: RSS 以外の受信処理
description: RSS 以外の受信処理
ms.assetid: 9fe262c3-9ce5-4625-8d29-ff7dc4ccb90a
keywords:
- 受信側のスケーリング WDK ネットワーク、非 RSS の受信処理
- RSS の WDK ネットワーク、非 RSS の受信処理
- RSS 以外は受信 WDK RSS の処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a438d2a11f122be219c7433e04a7629b4c622d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527473"
---
# <a name="non-rss-receive-processing"></a>RSS 以外の受信処理





このトピックの説明に従って、RSS のハンドルをサポートしていないミニポート ドライバーは処理を受信します。

次の図は、RSS 以外の処理を受信します。

![rss を使用しない処理の送受信方法を示す図](images/rsslessstack.png)

図では、破線のパスは、送信のための代替パスを表すし、受信処理します。 システムでは、スケーリングを制御するため、処理は、最適なパフォーマンスを提供する、CPU 上で常に発生しません。 接続は、偶然でのみ、同じ CPU に、連続する割り込み経由で処理されます。

非 RSS 割り込みのサイクルごとに、次のプロセスが繰り返されます。

1.  NIC は、DMA を使用して、受信したデータをバッファーに入力して、システムの割り込みです。

    ミニポート ドライバーでは、初期化中に、受信バッファーを共有メモリが割り当てられます。

2.  NIC が塗りつぶしの追加を続行できますこの割り込みサイクルでいつでも受信バッファー。 ただし、ミニポート ドライバー割り込みを有効にするまでは、NIC は再度中断されることはされません。

    システムを 1 つの割り込みのサイクルで処理する受信バッファーは、多くのさまざまなネットワーク接続を関連付けることができます。

3.  NDIS ミニポート ドライバーの呼び出す[ *MiniportInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/ff559395)関数 (ISR) システムで決定された CPU にします。

    理想的には、ISR は、少なくともビジー状態の CPU に移動する必要があります。 ただし、一部のシステムで、システムは、使用可能な CPU または NIC に関連付けられている CPU に ISR を割り当てます

4.  ISR には、割り込みと NDIS を要求を受信したデータの処理に遅延プロシージャ呼び出し (DPC) のキューが無効にします。

5.  NDIS 呼び出し、 [ *MiniportInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559398)現在の CPU に (DPC) の関数。

6.  DPC ビルドでは、すべての受信バッファーの記述子が表示され、ドライバー スタック上のデータを示します。 詳細については、次を参照してください。[ネットワーク データの受信](receiving-network-data.md)します。

    複数の接続の多くのバッファーがあり、多くの処理を完了する可能性があります。 その他の Cpu では、後続の割り込みサイクルに関連付けられている受信したデータを処理できます。 特定のネットワーク接続の処理、送信は、別の CPU にも実行できます。

7.  DPC は、割り込みを使用できます。 この割り込みサイクルが完了し、プロセスが再び開始します。

 

 






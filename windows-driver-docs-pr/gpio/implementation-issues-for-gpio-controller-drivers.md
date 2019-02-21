---
title: GPIO コント ローラーのドライバーの実装の問題
description: GPIO フレームワーク拡張機能 (GpioClx) は、柔軟性に優れたデバイス ドライバー インターフェイス (DDI) を提供します。
ms.assetid: 303A6034-7ED7-4C21-86E5-076383AF3A5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d598c4cead43a200638525c5370333ba7fd5786
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528114"
---
# <a name="implementation-issues-for-gpio-controller-drivers"></a>GPIO コント ローラーのドライバーの実装の問題


GPIO フレームワーク拡張機能 (GpioClx) は、柔軟性に優れたデバイス ドライバー インターフェイス (DDI) を提供します。 この DDI では、代替のコールバック インターフェイスを選択することができます。 ドライバー開発者は、ターゲットの GPIO コント ローラー デバイスのハードウェア アーキテクチャに最適であるイベントのコールバック関数のセットを実装する必要があります。

たとえばからの読み取りと書き込み I/O の GPIO ピンを GPIO コント ローラー用ドライバーをサポートする場合、開発者は次のコールバック関数のペアの 1 つを実装するために選択できます。

[*クライアント\_ReadGpioPins* ](https://msdn.microsoft.com/library/windows/hardware/hh439404)と[*クライアント\_WriteGpioPins*](https://msdn.microsoft.com/library/windows/hardware/hh439439)
[*クライアント\_ReadGpioPinsUsingMask* ](https://msdn.microsoft.com/library/windows/hardware/hh439406)と[*クライアント\_WriteGpioPinsUsingMask* ](https://msdn.microsoft.com/library/windows/hardware/hh439445) 、*クライアント\_ReadGpioPins*と*クライアント\_WriteGpioPins*関数受信銀行番号、GPIO ピンの数値の配列、およびビット値のデータ バッファーから読み取りまたはこれらのピンに書き込まれます。 GPIO ピンの数が少ないは通常、読み取りまたは書き込み操作のアクセス、だけの場合、この 2 つのコールバックは、最適な実装を生じる可能性があります。 この実装が使用される通常の GPIO コント ローラーがハードウェアの登録がないメモリ マップトします。 ただし、いくつかの GPIO ピンが書き込み操作、または読み取り中にアクセスする可能性がある場合、または GPIO コント ローラーのハードウェアが並列で複数の GPIO ピンを効率的にアクセスできる場合は、他の 2 つのコールバック関数は、実装を生成可能性があります。

*クライアント\_ReadGpioPinsUsingMask*と*クライアント\_WriteGpioPinsUsingMask*コールバック関数が読み取りまたは 1 回の呼び出しで最大 64 個のピンの銀行を記述します。 *クライアント\_ReadGpioPinsUsingMask*関数は、64 ビット マスクに GPIO ピンの値を読み取ります。 *クライアント\_WriteGpioPinsUsingMask*関数は 2 つの 64 ビット マスクを使用します。 1 つのマスクを設定するには、どの GPIO ピンを示し、その他のマスクは、GPIO ピンをオフにすることを示します。 この実装は、メモリ マップト GPIO コント ローラーの通常使用されます。

 

 





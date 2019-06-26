---
title: WIA-TWAIN リスク
description: WIA-TWAIN リスク
ms.assetid: f202a0f6-ceec-4658-a499-b3024f6ebb71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921577b9164e62955d966dbf16be02fdf1a0ac9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364998"
---
# <a name="wia-twain-risks"></a>WIA-TWAIN リスク





WIA ドライバーの STI 部分で使用される TWAIN ドライバーがあればは、次の注意すべき必要があります。

1.  TWAIN データ ソースが呼び出す[ **IStiUSD::LockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-lockdevice)ドライバーにアクセスする前にします。 こうことまで、WIA ドライバーへの接続からの WIA アプリケーション[ **IStiUSD::UnLockDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-unlockdevice)が呼び出されます。 この問題を最小限に抑えるには、WIA クライアントが接続し、操作を実行できるように制限されたデバイスにアクセスしてください。 これは重要ですので、TWAIN アプリケーションとドライバーの間の一対一のリレーションシップを維持します。 WIA では、1 つの WIA ドライバーへの接続を複数のアプリケーションを許可します。 このため、TWAIN ドライバーへのアクセス、TWAIN アプリケーションを WIA アプリケーションをロックできます可能性があります。 これを回避するには、適切なロック手法を使用します。

2.  すべてのアプリケーションまたは STI インターフェイスのメソッドを使用するユーティリティは、WIA ドライバーにアクセスを防ぐことができます。 いくつかの例は、ボタンまたはデバイスの状態と、システム トレイの監視アプリケーションを監視するユーティリティです。

3.  WIA ドライバーへの呼び出しを確認する必要があります[ **IStiUSD::RawReadData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreaddata)、 [ **IStiUSD::RawWriteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritedata)、 [ **IStiUSD::RawReadCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawreadcommand)、 [ **IStiUSD::RawWriteCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-rawwritecommand)と[ **IStiUSD::Escape** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape)正しく検証され、適切なロックを使用して分離します。

ためだけに有効な入力方向の値を検証する、ドライバーの記述と、データは、デバイスに送信されます。

使用する場合は、適切な検証シーケンス**IStiUSD::Escape**を参照してください[IStiUSD エスケープ メソッドを使用して](using-the-istiusd-escape-method.md)します。 適切なロックに関する詳細については、次を参照してください。[ロックおよびロック解除のベスト プラクティス](locking-and-unlocking-best-practices.md)します。

 

 





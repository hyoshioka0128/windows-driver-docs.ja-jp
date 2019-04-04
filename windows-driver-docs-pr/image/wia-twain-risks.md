---
title: WIA-TWAIN リスク
description: WIA-TWAIN リスク
ms.assetid: f202a0f6-ceec-4658-a499-b3024f6ebb71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a909adfab1ad4e80d2498777bec2785ef3cb6aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582141"
---
# <a name="wia-twain-risks"></a>WIA-TWAIN リスク





WIA ドライバーの STI 部分で使用される TWAIN ドライバーがあればは、次の注意すべき必要があります。

1.  TWAIN データ ソースが呼び出す[ **IStiUSD::LockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543829)ドライバーにアクセスする前にします。 こうことまで、WIA ドライバーへの接続からの WIA アプリケーション[ **IStiUSD::UnLockDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543843)が呼び出されます。 この問題を最小限に抑えるには、WIA クライアントが接続し、操作を実行できるように制限されたデバイスにアクセスしてください。 これは重要ですので、TWAIN アプリケーションとドライバーの間の一対一のリレーションシップを維持します。 WIA では、1 つの WIA ドライバーへの接続を複数のアプリケーションを許可します。 このため、TWAIN ドライバーへのアクセス、TWAIN アプリケーションを WIA アプリケーションをロックできます可能性があります。 これを回避するには、適切なロック手法を使用します。

2.  すべてのアプリケーションまたは STI インターフェイスのメソッドを使用するユーティリティは、WIA ドライバーにアクセスを防ぐことができます。 いくつかの例は、ボタンまたはデバイスの状態と、システム トレイの監視アプリケーションを監視するユーティリティです。

3.  WIA ドライバーへの呼び出しを確認する必要があります[ **IStiUSD::RawReadData**](https://msdn.microsoft.com/library/windows/hardware/ff543834)、 [ **IStiUSD::RawWriteData**](https://msdn.microsoft.com/library/windows/hardware/ff543839)、 [ **IStiUSD::RawReadCommand**](https://msdn.microsoft.com/library/windows/hardware/ff543831)、 [ **IStiUSD::RawWriteCommand** ](https://msdn.microsoft.com/library/windows/hardware/ff543836)と[ **IStiUSD::Escape** ](https://msdn.microsoft.com/library/windows/hardware/ff543815)正しく検証され、適切なロックを使用して分離します。

ためだけに有効な入力方向の値を検証する、ドライバーの記述と、データは、デバイスに送信されます。

使用する場合は、適切な検証シーケンス**IStiUSD::Escape**を参照してください[IStiUSD エスケープ メソッドを使用して](using-the-istiusd-escape-method.md)します。 適切なロックに関する詳細については、[ロックおよびロック解除のベスト プラクティス](locking-and-unlocking-best-practices.md)を参照してください。

 

 





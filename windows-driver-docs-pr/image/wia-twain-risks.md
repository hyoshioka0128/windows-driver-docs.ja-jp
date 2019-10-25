---
title: WIA-TWAIN リスク
description: WIA-TWAIN リスク
ms.assetid: f202a0f6-ceec-4658-a499-b3024f6ebb71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d300da635a5e7267c66c7694fe3865df808f937a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840664"
---
# <a name="wia-twain-risks"></a>WIA-TWAIN リスク





WIA ドライバーの STI 部分を使用する TWAIN ドライバーがある場合は、次の点に注意する必要があります。

1.  TWAIN データソースは、ドライバーにアクセスする前に[**Ia usd:: LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)を呼び出します。 これにより、WIA アプリケーションは、 [**IUnLockDevice::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)が呼び出されるまで wia ドライバーに接続できなくなります。 この問題を最小限に抑えるには、デバイスへのアクセスを制限して、WIA クライアントが接続して操作を実行できるようにします。 これは、TWAIN はアプリケーションとドライバーの間に1対1の関係を維持するため、重要です。 WIA では、複数のアプリケーションを1つの WIA ドライバーに接続できます。 このため、TWAIN ドライバーにアクセスする TWAIN アプリケーションは、WIA アプリケーションをロックアウトする可能性があります。 これを回避するには、適切なロック方法を使用します。

2.  STI インターフェイスメソッドを使用するアプリケーションまたはユーティリティがあると、WIA ドライバーへのアクセスが妨げられる可能性があります。 たとえば、ボタンまたはデバイスの状態を監視するユーティリティや、システムトレイを監視するアプリケーションなどがあります。

3.  WIA ドライバーでは、 [**Istiusd:: RawReadData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)、istiusd:: [**rawwritedata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)、Istiusd:: [**rawwritedata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreadcommand)、Istiusd:: [**Rawwritedata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand) 、i usd:: [**Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)の呼び出しが適切に検証され、次によって分離されていることを確認する必要があります。適切なロックを使用します。

ドライバーを記述するときは、有効なデータのみがデバイスに送信されるように、受信値を確認します。

**Ib usd:: escape**を使用する場合の適切な検証シーケンスについては、「 [Ib usd Escape メソッドの使用](using-the-istiusd-escape-method.md)」を参照してください。 適切なロックの詳細については、「[ロックとロック解除のベストプラクティス](locking-and-unlocking-best-practices.md)」を参照してください。

 

 





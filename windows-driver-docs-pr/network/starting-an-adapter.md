---
title: アダプターの開始
description: アダプターの開始
ms.assetid: ff2c8914-2fc2-4182-b47e-685571508b33
keywords:
- ミニポート アダプタの WDK ネットワーク、開始
- アダプターの WDK ネットワーク、開始
- WDK のネットワークを一時停止の状態
- WDK ネットワークの状態を実行しています。
- MiniportRestart
- ミニポート アダプタの開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97fcf819feefa20e3c052c1bdccbfd3d81104b22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558133"
---
# <a name="starting-an-adapter"></a>アダプターの開始





NDIS ミニポート ドライバーを呼び出す[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)が一時停止状態にあるアダプターの再起動要求を開始する関数。 受信したことを示す、ドライバーを再開できます NDIS 呼び出しの後にすぐにデータ*MiniportRestart*し、同期または非同期ミニポートする前にドライバーが、再起動操作を完了します。

ミニポート ドライバーの呼び出し時に[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)関数、NDIS 渡しますへのポインター、 [ **NDIS\_再起動\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff567255)ミニポート ドライバーに構造体、 **RestartAttributes**のメンバー、 [ **NDIS\_ミニポート\_再起動\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566480)構造体。

再起動操作を非同期的に完了する*MiniportRestart*返します NDIS\_状態\_PENDING とドライバーを呼び出す必要があります、 [ **NdisMRestartComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563665)操作が完了した後に機能します。

再起動操作が完了した後、送信要求を受け入れる準備ができて、ミニポート ドライバーがあります。 NDIS は、再起動操作が完了するまで、停止、初期化、または一時停止要求などの他のプラグ アンド プレイ操作を開始しません。

ドライバーと送信を処理し、操作を受け取る準備ができて、アダプターが実行中の状態です。

 

 






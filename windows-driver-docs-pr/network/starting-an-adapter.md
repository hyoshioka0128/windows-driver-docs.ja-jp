---
title: アダプターの起動
description: アダプターの起動
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
ms.openlocfilehash: 05722fcc939cafc03e88a902446bbdf9e340cf0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377556"
---
# <a name="starting-an-adapter"></a>アダプターの起動





NDIS ミニポート ドライバーを呼び出す[ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)が一時停止状態にあるアダプターの再起動要求を開始する関数。 受信したことを示す、ドライバーを再開できます NDIS 呼び出しの後にすぐにデータ*MiniportRestart*し、同期または非同期ミニポートする前にドライバーが、再起動操作を完了します。

ミニポート ドライバーの呼び出し時に[ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)関数、NDIS 渡しますへのポインター、 [ **NDIS\_再起動\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_attributes)ミニポート ドライバーに構造体、 **RestartAttributes**のメンバー、 [ **NDIS\_ミニポート\_再起動\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_restart_parameters)構造体。

再起動操作を非同期的に完了する*MiniportRestart*返します NDIS\_状態\_PENDING とドライバーを呼び出す必要があります、 [ **NdisMRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismrestartcomplete)操作が完了した後に機能します。

再起動操作が完了した後、送信要求を受け入れる準備ができて、ミニポート ドライバーがあります。 NDIS は、再起動操作が完了するまで、停止、初期化、または一時停止要求などの他のプラグ アンド プレイ操作を開始しません。

ドライバーと送信を処理し、操作を受け取る準備ができて、アダプターが実行中の状態です。

 

 






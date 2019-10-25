---
title: アダプターの起動
description: アダプターの起動
ms.assetid: ff2c8914-2fc2-4182-b47e-685571508b33
keywords:
- ミニポートアダプター WDK ネットワーク、開始
- WDK ネットワークのアダプター、開始
- 一時停止状態 WDK ネットワーク
- 実行状態 WDK ネットワーク
- MiniportRestart
- ミニポートアダプターの開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e639ebbe263b6c0c803564ffa3a6c6213e34f91
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841830"
---
# <a name="starting-an-adapter"></a>アダプターの起動





NDIS は、ミニポートドライバーの[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出して、一時停止状態のアダプターに対する再起動要求を開始します。 ドライバーは、NDIS 呼び出し*Miniportrestart*の直後、およびミニポートドライバーが同期または非同期のいずれかで再起動操作を完了する前に、受信したデータを示すことができます。

ミニポートドライバーの[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出すと、ndis は ndis\_へのポインターを渡し、Ndis の**RestartAttributes**メンバーのミニポートドライバーに[ **\_属性構造を再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)し[ **\_ミニポート\_\_パラメーター構造を再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_restart_parameters)します。

再開操作を非同期に完了させるために、 *Miniportrestart*は NDIS\_STATUS\_PENDING を返し、操作が完了した後、ドライバーは[**NdisMRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismrestartcomplete)関数を呼び出す必要があります。

再開操作が完了したら、ミニポートドライバーは送信要求を受け入れる準備ができている必要があります。 再起動操作が完了するまで、NDIS は、halt、initialize、pause 要求などの他のプラグアンドプレイ操作を開始しません。

ドライバーが送受信操作を処理する準備が整うと、アダプターは Running 状態になります。

 

 






---
title: 待機/ウェイク IRP の送信
description: 待機/ウェイク IRP の送信
ms.assetid: ed582644-af51-4841-be59-6a3deb6d9de5
keywords:
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- Irp WDK の電源管理のウェイク/待機を送信します。
- 送信待機/ウェイク Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7682bcbc0d2fc5327067d49bfb68620f1fd2253
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364085"
---
# <a name="sending-a-waitwake-irp"></a>待機/ウェイク IRP の送信





マイナー power IRP コード[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)デバイスの起動時またはシステムをスリープ解除しています。 自分自身またはシステムをスリープ解除できるデバイスのドライバーの送信**IRP\_MN\_待機\_WAKE**要求。 システムは、送信**IRP\_MN\_待機\_WAKE**電源スイッチなど、システムを常にスリープ解除するデバイスのみに要求します。

ドライバーの送信、 **IRP\_MN\_待機\_WAKE** 2 つの理由の 1 つの要求。

1.  そのデバイスは、外部のウェイク アップ シグナルへの応答でスリープ状態から作業の状態に戻すできる必要があります。

    たとえば、モデムのドライバー可能性があります送信待機/ウェイク IRP エネルギーを節約するために D1 の電源状態で設定する前にします。 待機/ウェイク IRP では、着信呼び出しに応答するモデムを使用できます。

2.  そのデバイスは、ウェイク アップ シグナルへの応答でシステムをスリープ解除できる必要があります。

    システム スリープ状態になると、モデムが D1 の状態で残る可能性があります、 **IRP\_MN\_待機\_WAKE**保留中です。 ここでは、着信呼び出しは、モデムと同様に、システムにスリープ解除は。

デバイスがそれ自体またはシステムをスリープ解除する準備が完了するかどうか、アクションに関連するドライバーが実行する必要があります、同じです。 主な違いは、デバイスとシステム ハードウェアが初期のウェイク アップ信号に応答する方法にあります。 ドライバーの動作は、いずれの場合も同じです。

 

 





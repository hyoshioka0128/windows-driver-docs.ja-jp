---
title: CoNDIS WAN ミニポート ドライバー状態の表示
description: CoNDIS WAN ミニポート ドライバー状態の表示
ms.assetid: c12492d7-e25d-4c80-8f2d-1e89931577ed
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、状態
- 状態インジケーターの WDK ネットワー キング、いる CoNDIS WAN ミニポート ドライバー
- NDIS_STATUS_WAN_CO_LINKPARAMS
- NDIS_STATUS_WAN_CO_FRAGMENT
- WDK いる CoNDIS WAN の問題
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02b25983a82137ac9b73b3853a478bb4c47539bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578536"
---
# <a name="indicating-condis-wan-miniport-driver-status"></a>CoNDIS WAN ミニポート ドライバー状態の表示





いる CoNDIS WAN ミニポート ドライバーは呼び出し[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)を最大に状態の変更を示すためにプロトコル ドライバーをバインドします。 いる CoNDIS ミニポート ドライバーまたは MCM から状態を示す詳細については、[ミニポート ドライバーの状態を示す](indicating-miniport-driver-status.md)を参照してください。

バインドされているプロトコル ドライバーには、これらの状態インジケーターを無視できます。 ただし、通常これらの指示の処理は、プロトコル ドライバーおよびミニポート ドライバー パフォーマンスの向上に発生します。

NDISWAN 中間ドライバーでは、NDIS に状態インジケーターを転送します。 NDIS 呼び出し、 [ **ProtocolCoStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570258)バインド プロトコル ドライバーまたは configuration manager の関数。 これらのプロトコル ドライバーまたは configuration manager は、これらの問題のログし、可能性があるために必要な場合、是正措置を実行します。

いる CoNDIS WAN ミニポート ドライバーへの呼び出しに[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)いる CoNDIS WAN ミニポート ドライバーが各 WAN 固有の状態を示すことを除いてすべている CoNDIS ミニポート ドライバーの場合と同じです仮想接続 (VC)、ミニポート ドライバーの nic ミニポート ドライバー呼び出し**NdisMCoIndicateStatusEx**をこの VC を共有するプロトコル ドライバーにこれらの変更を示すために、明示的な VC ハンドルを使用します。 ドライバーが指定されている場合、**NULL * * * NdisVcHandle*ステータスに関連する NIC の状態の一般的な変更

各状態の表示では、2 つの基本的な情報を提供します。

-   全般的なステータスを示すステータス コード。 定義済みの全般的なステータス コードの数に制限があります。このリストは、将来の拡張が適用されます。

-   ステータス情報を格納するバッファー。 この状態情報は、NIC または NIC に VC 固有いる CoNDIS WAN ミニポート ドライバーの特定、します。 たとえば、バッファーには、2 つの倍数で減少最近 X.25 接続の新しい送信速度が含まれます。

いる CoNDIS WAN VC 状態のインジケーターは次のとおりです。

-   NDIS\_状態\_WAN\_CO\_LINKPARAMS

    いる CoNDIS WAN ミニポート ドライバーは呼び出し[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)を NIC にアクティブになっている特定の VC のパラメーターが変更されたことを示します。 この呼び出しで、ミニポート ドライバーに VC にハンドルを渡します、 *NdisVcHandle*パラメーター、NDIS\_状態\_WAN\_CO\_で LINKPARAMS、 *GeneralStatus*パラメーター、およびへのポインターを[ **WAN\_CO\_LINKPARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff565819)構造体、 *StatusBuffer*パラメーター。 WAN\_CO\_LINKPARAMS VC の新しいパラメーターをについて説明します。

-   NDIS\_状態\_WAN\_CO\_フラグメント

    いる CoNDIS WAN ミニポート ドライバーは呼び出し**NdisMCoIndicateStatusEx**を VC のエンドポイントから部分的なパケットを受信したことを示します。 この呼び出しで、ミニポート ドライバーに VC にハンドルを渡します、 *NdisVcHandle*パラメーター、NDIS\_状態\_WAN\_CO\_でフラグメント、 *GeneralStatus*パラメーター、およびへのポインター、 [ **NDIS\_WAN\_CO\_フラグメント**](https://msdn.microsoft.com/library/windows/hardware/ff559030)構造体、 *StatusBuffer*パラメーター。 NDIS\_WAN\_CO\_フラグメント部分のパケットが受信されたことの理由を説明します。

    この通知が発生した後、接続指向のクライアントは、VC の他の最後に、接続指向のクライアントにフレームを送信する必要があります。 反対側のエンドポイントが、タイムアウトが発生するまで待機する必要はありませんように、これらのフレームは、パケットの部分的な状況の反対側のエンドポイントに通知されます。

    NDISWAN モニターは、各 VC の兆候をフラグメントの数をカウントすることによってパケットを削除します。

 

 






---
title: SAN 接続のシャットダウン
description: SAN 接続のシャットダウン
ms.assetid: 1ef509e4-fc8c-4feb-ae65-3c0f19033f34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19858d4c05810c8203fee980eaf11afd20c0e5b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362010"
---
# <a name="shutting-down-a-san-connection"></a>SAN 接続のシャットダウン





Windows Sockets スイッチでは、そのセッション プロトコルを使用して、SAN ソケットへの接続をシャット ダウンします。 スイッチの処理は、 **WSPRecvDisconnect**、 **WSPSendDisconnect**、および**WSPShutdown**アプリケーションからの呼び出し。 スイッチは、SAN サービス プロバイダーにこれらの呼び出しを転送しません。 スイッチは、受信と SAN ソケット上のデータの送信を無効にするのに、セッション プロトコルを使用します。

 

 






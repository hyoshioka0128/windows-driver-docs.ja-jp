---
title: SAN の操作の同期
description: SAN の操作の同期
ms.assetid: 9bbceecc-652e-44a7-b969-57578d2ebe68
keywords:
- WDK の San の同期
- SAN 同期 WDK
- Windows Sockets 直接 WDK、SAN の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f45adf0dd200d4f31d33a3a2409a81232463cd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377965"
---
# <a name="synchronizing-operations-on-a-san"></a>SAN の操作の同期





Windows Sockets スイッチは、SAN サービス プロバイダーとアプリケーション間でほぼすべての同期を処理するために、そのセッション プロトコルを使用します。 つまり、ほとんどの処理、TCP/IP プロバイダーと組み合わせて、スイッチ**WSPAsyncSelect**、 **WSPEventSelect**、および**WSPSelect**アプリケーションからの呼び出し。 スイッチは、FD の指定以外の SAN サービス プロバイダーにこれらの呼び出しを転送しない\_ACCEPT と FD\_SAN への呼び出しで接続するネットワーク イベントのコードはサービス プロバイダーの[ **WSPEventSelect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566287(v=vs.85))関数は、」の説明に従って[SAN 接続の設定](setting-up-a-san-connection.md)します。

 

 






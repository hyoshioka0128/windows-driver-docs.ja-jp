---
title: 同期処理、SAN 上
description: 同期処理、SAN 上
ms.assetid: 9bbceecc-652e-44a7-b969-57578d2ebe68
keywords:
- WDK の San の同期
- SAN 同期 WDK
- Windows Sockets 直接 WDK、SAN の同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94ad5101a5ccea0d64749fa9a5e53b628584c14b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549218"
---
# <a name="synchronizing-operations-on-a-san"></a>同期処理、SAN 上





Windows Sockets スイッチは、SAN サービス プロバイダーとアプリケーション間でほぼすべての同期を処理するために、そのセッション プロトコルを使用します。 つまり、ほとんどの処理、TCP/IP プロバイダーと組み合わせて、スイッチ**WSPAsyncSelect**、 **WSPEventSelect**、および**WSPSelect**アプリケーションからの呼び出し。 スイッチは、FD の指定以外の SAN サービス プロバイダーにこれらの呼び出しを転送しない\_ACCEPT と FD\_SAN への呼び出しで接続するネットワーク イベントのコードはサービス プロバイダーの[ **WSPEventSelect**](https://msdn.microsoft.com/library/windows/hardware/ff566287)関数は、」の説明に従って[SAN 接続の設定](setting-up-a-san-connection.md)します。

 

 






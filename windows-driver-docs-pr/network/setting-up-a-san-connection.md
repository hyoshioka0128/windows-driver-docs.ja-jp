---
title: SAN 接続を設定します。
description: SAN 接続を設定します。
ms.assetid: f5d5e759-d77c-4db8-9b63-fb4c79344dff
keywords:
- Windows Sockets 直接 WDK、接続のセットアップ
- WDK San 接続
- SAN 接続のセットアップ WDK
- SAN 接続のセットアップに関する接続セットアップ WDK、SAN
- SAN サービス プロバイダーに接続のセットアップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc5330f637ae8d672220e1dcc59fc55dba08c30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529008"
---
# <a name="setting-up-a-san-connection"></a>SAN 接続を設定します。





接続のセットアップ中には、Windows Sockets スイッチは、どのサービス プロバイダーがサービスの TCP ソケットを決定します。 このプロバイダーでは、ソケットのほとんどの後続の操作を処理します。 スイッチが SAN サービス プロバイダーを選択するかどうかに関係なく TCP/IP プロバイダーは、いくつかの種類のセットアップ操作のみを処理します。

このセクションでは、SAN サービス プロバイダーを実行する接続のセットアップ操作と TCP/IP プロバイダーを処理する接続のセットアップ操作について説明します。 この情報は、次のトピックで提供されます。

[作成して SAN のソケットをバインドします。](creating-and-binding-san-sockets.md)

[接続を開始します。](initiating-a-connection.md)

[SAN 上の接続のリッスン](listening-for-connections-on-a-san.md)

[接続要求の受け入れ](accepting-connection-requests.md)

[SAN の操作にメモリを登録します。](registering-memory-for-operations-on-a-san.md)

[登録済みのメモリのキャッシュ](caching-registered-memory.md)

 

 






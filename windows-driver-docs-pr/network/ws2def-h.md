---
title: Ws2def.h
description: このセクションには、カーネル モードのネットワーク ドライバーに関する Ws2def.h ヘッダーが含まれています。
ms.assetid: D84A448E-5810-485F-9CAC-4366E4223DBE
keywords:
- Ws2def.h ネットワーク ドライバー
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e4592ef434b81aa984c8a530d96c79344bb926b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377942"
---
# <a name="ws2defh"></a>Ws2def.h

このセクションには、カーネル モードのネットワーク ドライバーに関する Ws2def.h ヘッダーが含まれています。 このヘッダーは、ユーザー モードのアプリケーション ネットワークと共有されても、Windows SDK に含まれます。

Ws2def.h ヘッダーには、Winsock2 仕様の定義が含まれています。 Winsock2.h で含まれています。 ユーザー モード アプリケーションには、直接 Ws2def.h を含むのではなく、Winsock2.h を含める必要があります。 また Winsock.h が含まれるモジュールによって Ws2def.h を含めることができません。

> [!IMPORTANT]
> このセクションのトピックには、定義、マクロ、Oid、状態インジケーター、およびネットワーク ドライバー リファレンス (構造体、列挙型、関数、およびコールバック) の一部ではないその他のデータ構造のページが含まれています。 
>
> このヘッダーのネットワーク ドライバー リファレンスの詳細については、次を参照してください。 [Ws2def.h (リファレンス)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))します。

## <a name="in-this-section"></a>このセクションの内容

* [AF_INET](af-inet.md)
* [AF_INET6](af-inet6.md)
* [SIO_ADDRESS_LIST_CHANGE](sio-address-list-change.md)
* [SIO_ADDRESS_LIST_QUERY](sio-address-list-query.md)
* [SO_BROADCAST](so-broadcast.md)
* [SO_CONDITIONAL_ACCEPT](so-conditional-accept.md)
* [SO_EXCLUSIVEADDRUSE](so-exclusiveaddruse.md)
* [SO_KEEPALIVE](so-keepalive.md)
* [SO_RCVBUF](so-rcvbuf.md)
* [SO_REUSEADDR](so-reuseaddr.md)




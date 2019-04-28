---
title: IPsec でのバック グラウンド読み取り
description: IPsec でのバック グラウンド読み取り
ms.assetid: b7316027-a66c-4630-88d4-fa3c66f735f8
keywords:
- WDK IPsec オフロード、ESP により保護されたパケットが読み取りをバック グラウンドします。
- WDK IPsec オフロード、AH で保護されたパケットが読み取りをバック グラウンドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25704a096c6a96693e7a238045a8c8b06050e1a3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367688"
---
# <a name="background-reading-on-ipsec"></a>IPsec でのバック グラウンド読み取り

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




このセクションを理解するには、次の Rfc および IP セキュリティ Working Group Internet Engineering Task Force (IETF) のによって公開された下書きで指定されているインターネット プロトコル セキュリティ (IPsec) を理解する必要があります。

-   [インターネット プロトコル (RFC 2401) のセキュリティ アーキテクチャ](https://go.microsoft.com/fwlink/p/?linkid=9845)

認証ヘッダー (AH):

-   [IP の認証ヘッダー (RFC 2402)](https://go.microsoft.com/fwlink/p/?linkid=9847)

-   [HMAC MD5-96 ESP および AH (RFC 2403) 内での使用](https://go.microsoft.com/fwlink/p/?linkid=9849)

-   [HMAC の SHA-1-96 ESP および AH (RFC 2404) 内での使用](https://go.microsoft.com/fwlink/p/?linkid=9998)

-   [再生防止 (RFC 2085) で HMAC MD5 IP の認証](https://go.microsoft.com/fwlink/p/?linkid=9850)

カプセル化セキュリティ ペイロード (ESP):

-   [IP セキュリティ ペイロード (ESP) (RFC 2406) をカプセル化します。](https://go.microsoft.com/fwlink/p/?linkid=9851)

-   [ESP Cbc 暗号アルゴリズム (RFC 2451)](https://go.microsoft.com/fwlink/p/?linkid=9853)

-   [明示的な IV (RFC 2405) と ESP DES-CBC 暗号アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=9854)

-   [NULL 暗号化アルゴリズムと IPsec (RFC 2410) での使用](https://go.microsoft.com/fwlink/p/?linkid=9855)

 

 






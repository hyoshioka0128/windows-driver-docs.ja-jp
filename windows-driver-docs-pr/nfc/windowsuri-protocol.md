---
title: WindowsUri プロトコル
description: WindowsUri プロトコル
ms.assetid: 79589ECE-9DF9-40C8-897D-95B432C4C9C8
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b8a7391cb55374115038552cfef7748b1d5a085
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843464"
---
# <a name="windowsuri-protocol"></a>WindowsUri プロトコル


"WindowsUri" プロトコルは、単純な URI 文字列のサブスクリプションを抽象化する手段です。 Windows は、ユーザーが必要としている可能性のある Uri の受信に関心があるドライバーに登録するために、この種類をサブスクライブします。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、"WindowsUri" サブスクライバーに対して、NULL で終わる UTF 16LE エンコードされた文字列として URI 文字列を返す必要があります。
-   ドライバーは、"WindowsUri" パブリケーションの入力ペイロードを、16LE でエンコードされた文字列として扱う必要があります。 ドライバーは、NULL 終端の入力または NULL で終わらない入力のいずれかを安全に受け入れる必要があります。
-   近接通信テクノロジが NFC として提供されている場合、ドライバーは "WindowsUri" 型のサブスクリプションを "NDEF: wkt 内の URI ペイロードのサブスクリプションと同等のものとして扱う必要があります。U "または" NDEF: wkt。Sp "メッセージ。
    -   また、ドライバーは "NDEF: wkt 内の URI ペイロードを含む" WindowsUri "サブスクリプションと一致する必要があります。Sp "メッセージ。 "NDEF: wkt" へのすべてのサブスクリプション。Sp "は、" NDEF: wkt "の完全なペイロードでいっぱいになっている必要があります。Sp "メッセージ。 NDEF メッセージにスマートポスターと入れ子になっていない URI レコードの両方が含まれている場合、URI レコードは無視する必要があります。
    -   ドライバーは、このメッセージの URI 文字列ペイロードのみをこの型のサブスクライバーに返す必要があります。 ドライバーは、この種類のサブスクライバーに完全な NDEF メッセージを返すことはできません。
-   近接通信テクノロジが NFC として提供されている場合、ドライバーは \[NFC URI\]で指定されているように、各 "WindowsUri" パブリケーションのペイロードを NDEF メッセージ内にカプセル化する必要があります。
-   プロバイダーは、他の互換性のあるスキームもサポートできます。

## <a name="publications-for-windowsuriwritetag"></a>"WindowsUri: WriteTag" のパブリケーション


これは、任意の書き込み可能なタグに URI を書き込むことができる特別な種類の WindowsUri パブリケーションです。

### <a name="required-actions"></a>必要なアクション

-   他の場所に記載されている一般的な "\*: WriteTag" の要件が適用されます。
-   上記の "WindowsUri" パブリケーション要件は、"WindowsUri: WriteTag" パブリケーションにも適用されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


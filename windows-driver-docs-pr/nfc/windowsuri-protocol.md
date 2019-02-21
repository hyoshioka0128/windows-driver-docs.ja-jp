---
title: WindowsUri プロトコル
description: WindowsUri プロトコル
ms.assetid: 79589ECE-9DF9-40C8-897D-95B432C4C9C8
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 797993c17701545864de6d0ee61fc4c202999b72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529961"
---
# <a name="windowsuri-protocol"></a>WindowsUri プロトコル


"WindowsUri"プロトコルは、単純な URI 文字列用のサブスクリプションを抽象化の手段です。 Windows は、Windows が興味を示している受信 Uri で起動でユーザーを利用することがありますをドライバーに登録するために、この型にサブスクライブします。

### <a name="required-actions"></a>必要な操作

-   ドライバーは、"WindowsUri"サブスクライバーに対して、NULL で終わる UTF 16LE でエンコードされた文字列として URI 文字列を返す必要があります。
-   ドライバーは、UTF 16LE でエンコードされた文字列として"WindowsUri"パブリケーションの入力ペイロードを扱う必要があります。 ドライバーは、NULL で終わるか、非 NULL で終わる入力を安全に受け入れる必要があります。
-   近接テクノロジが NFC としてアドバタイズされる場合、ドライバーする必要があります"WindowsUri"の種類のサブスクリプションとして扱う"NDEF:wkt 内の URI のペイロードのサブスクリプションに相当。U"または"NDEF:wkt します。Sp"メッセージです。
    -   ドライバーは、"NDEF:wkt 内の URI のペイロードを使用して"WindowsUri"サブスクリプションにも一致する必要があります。Sp"メッセージです。 すべてのサブスクリプションを"NDEF:wkt します。Sp"する必要がありますが、"NDEF:wkt の完全なペイロードで塗りつぶされます。Sp"メッセージです。 NDEF メッセージにスマート ポスターと URI に入れ子にされたレコードの両方が含まれる場合、URI レコードが無視する必要があります。
    -   ドライバーは、この種類のサブスクライバーに、URI 文字列のこのメッセージのペイロードのみを返す必要があります。 MUST NOT ドライバーでは、この種類のサブスクライバーに完全な NDEF メッセージを返します。
-   NFC、として近接テクノロジが提供されるかどうかは、ドライバーは、ペイロードで指定されている NDEF メッセージ内の各"WindowsUri"文書のカプセル化する必要があります\[NFC URI\]します。
-   プロバイダーも、他の互換性のあるパターンがサポート可能性があります。

## <a name="publications-for-windowsuriwritetag"></a>パブリケーション"WindowsUri:WriteTag"の場合


これは、特殊な種類の書き込み可能な任意のタグに書き込まれる URI を許可する WindowsUri パブリケーションです。

### <a name="required-actions"></a>必要な操作

-   一般的な"\*: タグ書き込み"他の場所で説明されている要件を適用します。
-   上記の"WindowsUri"パブリケーションの要件は、"WindowsUri:WriteTag"パブリケーションにも適用されます。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  


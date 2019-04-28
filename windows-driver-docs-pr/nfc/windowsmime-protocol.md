---
title: WindowsMime プロトコル
description: WindowsMime プロトコル
ms.assetid: 03C5A31F-269A-45B3-9359-B6FFF4823190
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f8aaf09f59956fea80fd3fece13b8c072dadef8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373586"
---
# <a name="windowsmime-protocol"></a>WindowsMime プロトコル


## <a name="windowsmime-subscriptions"></a>"WindowsMime"サブスクリプション


"WindowsMime"サブスクリプションは、すべての可能な MIME に型指定されたペイロードのサブスクリプションを抽象化の手段です。 Windows は、Windows を使用して、ユーザーを知りたい場合があります、MIME に型指定されたデータの受信に関心があるドライバーを使用した登録するために、この型にサブスクライブします。 これは、サブスクリプションのすべての可能な MIME に型指定されたペイロードであるため、ドライバーは、ペイロードと同様に、型を返す必要があります。

### <a name="required-actions"></a>必要な操作

-   ドライバーは、出力バッファーの最初の 256 バイト以内の ASCII でエンコードされ、NULL で終わる文字列としてのペイロードの MIME 型を返す必要があります。
-   ドライバーは、出力バッファーの最初の 256 バイトより後のメッセージ ペイロードを返す必要があります。
-   ドライバーは、256 + に完了した IRP の情報 フィールドを設定する必要があります**sizeof**(ペイロード)。
-   NFC として近接テクノロジが提供されると場合、ドライバーは 0x02 TNF フィールド値を持つすべての NDEF メッセージで"WindowsMime"のサブスクリプションと一致する必要があります。
    -   ドライバーは、この種類のサブスクライバーに一致した NDEF メッセージのペイロードのみを返す必要があります。
    -   MUST NOT ドライバーでは、この種類のサブスクライバーに完全なエンコード NDEF メッセージを返します。
-   プロバイダーも、他の互換性のあるパターンがサポート可能性があります。

## <a name="windowsmime-protocol"></a>"WindowsMime。" プロトコル


"WindowsMime。" パブリケーションは、MIME に型指定されたペイロードをピア デバイスに発行するだけの手段です。 "WindowsMime。" サブスクリプションは、特定の MIME の種類とペイロードをサブスクライブする手段です。 Windows は、単純な MIME に型指定されたメッセージをそのためには、ユーザーが指定したときに、近接デバイスに発行されます。

型の汎用例:"WindowsMime します。&lt;SomeMimeType&gt;"

具体的な例の種類:“WindowsMime.image/jpeg”

### <a name="required-actions"></a>必要な操作

-   NFC として近接テクノロジが提供されると場合、は、ドライバーが"WindowsMime のサブスクリプションが一致します。&lt;SomeMimeType&gt;「NDEF のメッセージを受信した 0x02 の TNF フィールド値を指定してと一致する型のフィールドが含まれている、のみ」&lt;SomeMimeType&gt;"で指定された等価性の規則に基づいて\[NDEF\]します。

    ドライバーは、この種類のサブスクライバーに一致する個々 の NDEF メッセージのペイロードのみを返す必要があります。

-   NFC として近接テクノロジが提供されると場合、ドライバーする必要がありますにカプセル化"WindowsMime します。&lt;SomeSubType&gt;"NDEF 内のパブリケーションは 0x02 TNF フィールド値を持つメッセージ。
    -   NDEF TYPE フィールドでの直接のマッピングを含める必要があります、 &lt;SomeSubType&gt;文字列のワイド文字が 1 バイトとして解釈されます。
    -   パブリケーションのメッセージ ペイロードの直接のバイナリ コンテンツを含める、NDEF ペイロード必要があります。

## <a name="windowsmimewritetag-publications"></a>"WindowsMime:WriteTag。" パブリケーション


"WindowsMime:WriteTag。" パブリケーションは、単に、タグに MIME 型指定されたペイロードの書き込みにアプリの手段です。

### <a name="required-actions"></a>必要な操作

-   一般的な"\*: タグ書き込み"他の場所で説明されている要件を適用します。
-   "WindowsMime します。&lt;SomeMimeType&gt;"他の場所で説明されているパブリケーションの要件に適用されます"WindowsMime:WriteTag&lt; 。SomeMimeType&gt;"のパブリケーション。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  


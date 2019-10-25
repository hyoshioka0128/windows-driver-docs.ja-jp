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
ms.openlocfilehash: 42d2988a61bb9a0770a8234c9eba329f156c888f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843287"
---
# <a name="windowsmime-protocol"></a>WindowsMime プロトコル


## <a name="windowsmime-subscriptions"></a>"WindowsMime" サブスクリプション


"WindowsMime" サブスクリプションは、MIME で型指定されたすべてのペイロードのサブスクリプションを抽象化する手段です。 Windows は、ユーザーが関心を持つ可能性のある MIME 型のデータを受信することに関心があるドライバーに登録するために、この種類をサブスクライブします。 これは、MIME で型指定されたすべてのペイロードのサブスクリプションであるため、ドライバーは、ペイロードと同様に型を返す必要があります。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、出力バッファーの最初の256バイト内で、ASCII エンコードの文字列として、および NULL で終わる文字列としてペイロードの MIME の種類を返す必要があります。
-   ドライバーは、出力バッファーの最初の256バイトの後にメッセージペイロードを返す必要があります。
-   ドライバーは、完了した IRP の Information フィールドを 256 +**sizeof**(ペイロード) に設定する必要があります。
-   近接通信テクノロジが NFC として提供されている場合、ドライバーは "WindowsMime" のサブスクリプションと TNF field 値0x02 を持つすべての NDEF メッセージを照合する必要があります。
    -   ドライバーは、この型のサブスクライバーに一致する NDEF メッセージのペイロードのみを返す必要があります。
    -   ドライバーは、この型のサブスクライバーに、完全にエンコードされた NDEF メッセージを返すことはできません。
-   プロバイダーは、他の互換性のあるスキームもサポートできます。

## <a name="windowsmime-protocol"></a>"WindowsMime" プロトコル


"WindowsMime" パブリケーションは、MIME 型のペイロードをピアデバイスに単純に発行する手段です。 "WindowsMime" サブスクリプションは、特定の MIME の種類を使用してペイロードをサブスクライブする手段です。 Windows は、ユーザーに指示されたときに、単純な MIME タイプのメッセージを近接デバイスに発行します。

一般的な型の例: "WindowsMime。&lt;SomeMimeType&gt;"

具体的な例の種類: "WindowsMime. image/jpeg"

### <a name="required-actions"></a>必要なアクション

-   近接通信テクノロジが NFC として提供されている場合、ドライバーは "WindowsMime" のサブスクリプションと一致している必要があります。&lt;SomeMimeType&gt;"は、TNF field 値が0x02 で、\[NDEF\]に指定されている等価性ルールに基づいて"&lt;SomeMimeType&gt;"に一致する型フィールドを持つ受信 NDEF メッセージのみです。

    ドライバーは、この型のサブスクライバーに、一致した個々の NDEF メッセージのペイロードのみを返す必要があります。

-   近接通信テクノロジが NFC として提供されている場合、ドライバーは各 "WindowsMime をカプセル化する必要があります。TNF field 値が0x02 の NDEF メッセージ内の&lt;SomeSubType&gt;"publication。
    -   NDEF TYPE フィールドには、各ワイド文字が1バイトとして解釈される、&lt;SomeSubType&gt; 文字列の直接マッピングが含まれている必要があります。
    -   NDEF ペイロードには、パブリケーションメッセージペイロードの直接バイナリコンテンツが含まれている必要があります。

## <a name="windowsmimewritetag-publications"></a>"WindowsMime: WriteTag" レプリケーション


"WindowsMime: WriteTag" publication は、アプリがタグに MIME 型のペイロードを簡単に書き込むための手段です。

### <a name="required-actions"></a>必要なアクション

-   他の場所に記載されている一般的な "\*: WriteTag" の要件が適用されます。
-   "WindowsMime.&lt;SomeMimeType&gt;"に記載されている発行の要件は、「WindowsMime: WriteTag」に適用されます。&lt;SomeMimeType&gt;"パブリケーション。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


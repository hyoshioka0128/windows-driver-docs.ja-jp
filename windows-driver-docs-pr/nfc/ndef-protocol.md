---
title: NDEF プロトコル
description: NDEF プロトコル
ms.assetid: 5AF082EC-70D6-4117-BFCE-B28A8DBAC210
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac16b40f415f4bfd381a47b4133e8396678a1bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383589"
---
# <a name="ndef-protocol"></a>NDEF プロトコル


"NDEF"プロトコルは、NFP プロバイダーのパブリッシュ/サブスクライブ モデルを使ってマップとして直接 NFC フォーラム デバイスと対話する手段です。 このプロトコルを使用して任意のクライアントは、エンコードおよび NDEF パケットをデコードする方法を理解する必要があります。 公開メッセージは、クライアントは単なる種類を指定"NDEF"として NDEF メッセージ自体の中に他の型情報が埋め込まれているため。 "NDEF"型の発行により、クライアントはほぼパススルーに直接アクセスする NFC NDEF メッセージを送信します。 ニュースレターを購読するクライアントは"NDEF"の後に、指定は、':' (コロン)。

コロンは、6 つのレコードの種類の 1 つです。

-   空
-   ext
-   MIME
-   URI
-   wkt
-   Unknown

プロバイダーでは、このセクションに記載 NDEF プロトコル固有の要件と基本的なプロバイダーの要件に従って NDEF をサポートしています。

"NDEF:wkt など、サポートされている型のいずれかにこれらの NDEF メッセージをリッスンするには、クライアントが定期受信します。Sp"。 プロバイダーは、種類に対応する NDEF メッセージが検出されるたびに、(まだ NDEF でエンコード) NDEF メッセージ全体がサブスクライブしているクライアントに配信されます。 内での規則に従って\[NDEF\]、NDEF メッセージの最初の NDEF レコードで指定された型のフィールドは、NDEF メッセージに一致する 'type' です。 もう一度、NDEF メッセージを送信するクライアントは"NDEF"のプロトコルを指定する、完全な NDEF メッセージを発行します。

すべて NDEF メッセージにサブスクライブするためのメカニズムがあります。これは、"NDEF"をサブスクライブすることによって実現されます。

## <a name="common-ndef-protocol-driver-requirements"></a>一般的な NDEF プロトコル ドライバーの要件


NDEF NFP の NFC が有効なプロバイダーのすべてのドライバー サポートについての一般的ないくつかの要件は。

### <a name="required-actions"></a>必要な操作

-   ドライバーがで指定されている NDEF メッセージ内の最初の NDEF レコードの TNF と種類のフィールドに基づいてサブスクリプションを受信した NDEF メッセージと一致する必要があります\[NDEF\]します。
-   1 つ以上の場合"\*: タグ書き込み"パブリケーションが有効になっているし、ドライバーが使用できるか、MUST NOT タグの既存のペイロードで読み取られるその他のサブスクリプションに一致する目的で十分な領域を持つ書き込み可能なタグを検出します。 これにより、他のアプリまたはタグでメッセージをサブスクライブがサービスの切断をタグの記述アプリです。
-   MUST NOT ドライバーの送信 NFP の NFC が有効なプロバイダーは、"\*: タグ書き込み"パブリケーション (、NFC フォーラム タグ) ではなく、NFC フォーラムのデバイスに接続するとします。
-   1 つ以上の場合"\*: タグ書き込み"パブリケーションは、ドライバーが、ペイロードの少なくとも 1 つの使用可能な十分な領域を持つ書き込み可能なタグを検出した時点で有効になっている、ドライバーに書き込む必要が、ペイロードの 1 つだけタグ。 o は、複数のパブリケーションはアクティブ、小さくすれば、タグに書き込むことが最も最近作成または有効になっている"\*: タグ書き込み"パブリケーションは書き込まれる 1 つである必要があります。
-   場合、"\*: タグ書き込み"場合でもに、ドライバーが既に説明したとおりに、ドライバーする必要がありますをタグに、ペイロードを書き込むパブリケーションが作成または処理中、ドライバーがペイロードの使用可能な十分な領域を持つ書き込み可能なタグとの通信を有効になっている、タグ。
-   ドライバーは、以前の内容が上書きされるようにタグを記述する必要があります。
-   場合、"\*: タグ書き込み"ペイロードが正常に作成、タグに、ドライバーをトリガーする必要があります、 [ **IOCTL\_NFP\_取得\_次\_送信\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)そのパブリケーション (上で指定した) として処理します。

## <a name="publications-for-ndefwritetag"></a>パブリケーション"NDEF:WriteTag"の場合


これは、特殊な種類の NFC フォーラム タグに書き込まれる 1 つ以上の NDEF メッセージを許可するパブリケーションです。

### <a name="required-actions"></a>必要な操作

-   一般的な"\*: タグ書き込み"他の場所で説明されている要件を適用します。
-   NFC フォーラム タグは、複数の NDEF メッセージを含めることができます、ため、ドライバーは複数の連結された NDEF メッセージ ペイロードとしてから成る"NDEF:WriteTag"パブリケーションを正しく同意する必要があります。

## <a name="publications-for-settagreadonly"></a>パブリケーション"SetTagReadOnly"の場合


このパブリケーションは、読み取り専用にタグをロックするクライアントで許可します。 既に書式設定された NDEF 読み取り/書き込みタグは、プロバイダーによって読み取り専用にのみ変換する必要があります。

### <a name="required-actions"></a>必要な操作

-   ドライバーでは、NDEF 準拠しているかどうか、接続されているタグには確認する必要がありますまずします。
-   1 つ以上の場合"\*: です。タグの書き込み"パブリケーションが有効になっているし、ドライバーが書き込み可能なタグを検出、ドライバー書き込む必要がありますをタグに最初に、共通に準拠する"\*: タグ書き込み"の要件には、その他の場所が記載されているし、変換、NDEF 読み取り/書き込みタグを読み取り専用です。

## <a name="empty-ndef-record-ndefempty"></a>空の NDEF レコード:"NDEF:Empty"


種類、ID、またはこのメッセージのペイロードはありません。 "NDEF:Empty"の種類によるサブスクリプションは、Windows クライアントの観点から意味を行わないようです。

### <a name="required-actions"></a>必要な操作

この種類のパブリケーションまたはサブスクリプションは、ステータスの近接プロバイダー ドライバーによって拒否する必要があります\_無効な\_パラメーター。

## <a name="subscriptions-for-all-ndef-types-ndef"></a>NDEF 型のすべてのサブスクリプション:"NDEF"


クライアントは、すべての受信 NDEF メッセージをサブスクライブできます。 通常、アプリケーションは、対象のメッセージの種類を知っている場合にサブスクライブその型に具体的には。 ただし、各 NDEF メッセージにサブスクライブすると便利ですがあります。 たとえば、アプリケーションをコピーし、重複 NDEF タグを書き込むことがこれに役に立ちます。

### <a name="required-actions"></a>必要な操作

ドライバーは、各 NDEF メッセージを受信"NDEF"のサブスクリプションと一致する必要があります。

## <a name="subscriptions-for-external-ndef-rtd-types-ndefext"></a>外部の NDEF RTD の種類のサブスクリプション:"NDEF:ext。"


ベンダーは、独自のメッセージのコンテンツを定義するのに、カスタムの拡張可能な RTD 名前空間を使用できます。 これにより、RTD の NFC フォーラムではなく、アプリまたはサード パーティで定義されている外部の型を購読するクライアント。

型の汎用例:"NDEF:ext.&lt;SomeExternalType&gt;"

具体的な例の種類:"NDEF:ext.contoso.com:mytype"

### <a name="required-actions"></a>必要な操作

ドライバーがのサブスクリプションと一致する必要があります"NDEF:ext.&lt;SomeExternalType&gt;「NDEF のメッセージを受信した 0x04 TNF フィールドの値があるしに一致する型のフィールドが含まれている、のみ」&lt;SomeExternalType&gt;"指定された等価性の規則に基づいて\[NFC RTD\]します。

## <a name="subscriptions-for-ndefmime"></a>サブスクリプションの"NDEF:MIME"


メッセージは、MIME 名前空間を使用して、メッセージの内容を定義します。

型の汎用例:"NDEF:MIME します。&lt;SomeMimeType&gt;"

具体的な例の種類:"NDEF:MIME.image/jpeg"

### <a name="required-actions"></a>必要な操作

ドライバーは"NDEF:MIME のサブスクリプションと一致する必要があります。&lt;SomeMimeType&gt;「NDEF のメッセージを受信した 0x02 の TNF フィールド値を指定してと一致する型のフィールドが含まれている、のみ」&lt;SomeMimeType&gt;"で指定された等価性の規則に基づいて\[NDEF\]します。

## <a name="subscriptions-for-ndefwkt"></a>サブスクリプションの"NDEF:wkt"


メッセージは、NFC フォーラムの既知の型の名前空間を使用して、メッセージの内容を定義します。

### <a name="required-actions"></a>必要な操作

-   ドライバーは"NDEF:wkt のサブスクリプションと一致する必要があります。&lt;SomeWellKnownType&gt;「NDEF のメッセージを受信した 0x01 の TNF フィールド値を指定してに一致する型のフィールドが含まれている、のみ」&lt;SomeWellKnownType&gt;"で指定された等価性の規則に基づきます。\[NDEF\]します。
-   MUST NOT ドライバーは、ドライバーの更新を必要とせず、NFC フォーラムで将来のよく知られている型を定義することができますを既知の型を検証します。

## <a name="subscriptions-for-unknown-ndef-type-ndefunknown"></a>不明な NDEF の種類のサブスクリプション:"NDEF:Unknown"


これにより、データの型指定されていないのペイロードをサブスクライブするクライアント。

### <a name="required-actions"></a>必要な操作

ドライバーは"NDEF:Unknown"のみで指定されている 0x05 の TNF フィールド値を持つ NDEF メッセージのサブスクリプションと一致する必要があります\[NDEF\]します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  


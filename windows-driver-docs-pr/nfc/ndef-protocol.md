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
ms.openlocfilehash: 629406a5711bfdbdf5504388cc1bea39b6dfc972
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844691"
---
# <a name="ndef-protocol"></a>NDEF プロトコル


"NDEF" プロトコルは、NFP プロバイダーの pub/sub モデルによってマップされたように、NFC フォーラムデバイスと直接対話する手段です。 このプロトコルを使用しているクライアントは、NDEF パケットをエンコードおよびデコードする方法を理解する必要があります。 メッセージを公開する場合、クライアントは型を "NDEF" として指定するだけです。これは、型情報の残りの部分が NDEF メッセージ自体に埋め込まれるためです。 "NDEF" 型を公開すると、クライアントはほぼ直接パススルーアクセスを使用して、NDEF メッセージを NFC 経由で送信できます。 サブスクライブするために、クライアントは "NDEF" の後に ': ' (コロン) を指定します。

コロンの後に続くのは、6種類のレコードのうちの1つです。

-   空
-   ext
-   MIME
-   URI
-   wkt
-   不明

プロバイダーは、このセクションに記載されている NDEF プロトコル固有の要件に加えて、プロバイダーの基本要件に従うことで NDEF をサポートしています。

これらの NDEF メッセージをリッスンするために、クライアントは、"NDEF: wkt" のようなサポートされている型のいずれかにサブスクライブします。Sp "。 プロバイダーは、型に一致する NDEF メッセージを検出するたびに、NDEF メッセージ全体 (NDEF でエンコード済み) をサブスクライブしているクライアントに配信します。 \[NDEF\]の規則に従って、NDEF メッセージの照合対象となる ' type ' は、NDEF メッセージの最初の NDEF レコードで指定された TYPE フィールドです。 ここでも、NDEF メッセージを送信するために、クライアントは、"NDEF" というプロトコルを指定する完全な NDEF メッセージを公開します。

すべての NDEF メッセージをサブスクライブするメカニズムもあります。これは、"NDEF" をサブスクライブすることで実現されます。

## <a name="common-ndef-protocol-driver-requirements"></a>一般的な NDEF プロトコルドライバーの要件


NFC 対応のすべての NFP プロバイダーのドライバーでの NDEF サポートに共通するいくつかの要件があります。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、\[NDEF\]で指定された NDEF メッセージ内の最初の NDEF レコードの TNF および TYPE フィールドに基づいて、受信した NDEF メッセージをサブスクリプションに一致させる必要があります。
-   1つ以上の "\*: WriteTag" パブリケーションが有効になっていて、十分な空き領域がある書き込み可能なタグがドライバーによって検出された場合、他のサブスクリプションと照合するために、タグの既存のペイロードを読み取ることはできません。 これにより、タグ書き込みアプリは、タグのメッセージにサブスクライブされている他のアプリやサービスをプリエンプトできます。
-   NFC が有効になっている NFP プロバイダーの場合、ドライバーは、nfc フォーラムタグとは対照的に、NFC フォーラムデバイスに接続しているときに "\*: WriteTag" パブリケーションを送信しないようにする必要があります。
-   少なくとも1つのペイロードに対して十分な空き領域がある書き込み可能なタグをドライバーが検出した時点で、1つ以上の "\*: WriteTag" パブリケーションが有効になっている場合、ドライバーは、そのタグにペイロードの1つだけを書き込む必要があります。 o 複数のパブリケーションがアクティブで、タグに書き込むのに十分な数のパブリケーションが存在する場合、最後に作成された、または有効になっている "\*: WriteTag" パブリケーションが書き込まれたものである必要があります。
-   ドライバーがペイロード用に十分な空き領域を持つ書き込み可能なタグと現在通信しているときに "\*: WriteTag" パブリケーションが作成または有効になっている場合、ドライバーは、以前にタグに書き込んだ場合でも、ドライバーはペイロードをタグに書き込む必要があります。
-   ドライバーは、前の内容が上書きされるようにタグに書き込む必要があります。
-   "\*: WriteTag" ペイロードがタグに正常に書き込まれた場合、ドライバーは、そのパブリケーションに対して指定されているように、次\_送信\_メッセージ処理 (前述のとおり) を使用して、 [**IOCTL\_NFP\_\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)する必要があります。

## <a name="publications-for-ndefwritetag"></a>"NDEF: WriteTag" のパブリケーション


これは、1つまたは複数の NDEF メッセージを NFC フォーラムタグに書き込むことができる特別な種類のパブリケーションです。

### <a name="required-actions"></a>必要なアクション

-   他の場所に記載されている一般的な "\*: WriteTag" の要件が適用されます。
-   NFC フォーラムタグには複数の NDEF メッセージを含めることができるため、ドライバーは、複数の連結された NDEF メッセージをペイロードとして使用する "NDEF: WriteTag" パブリケーションを正しく受け入れる必要があります。

## <a name="publications-for-settagreadonly"></a>"SetTagReadOnly" のパブリケーション


このパブリケーションでは、クライアントがタグを読み取り専用にロックできます。 プロバイダーは、既にフォーマットされた NDEF 読み取り/書き込みタグを読み取り専用に変換する必要があります。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、接続されたタグが NDEF に準拠しているかどうかを最初に確認する必要があります。
-   1つ以上の "\*:WriteTag "パブリケーションが有効になっていて、ドライバーが書き込み可能なタグを検出した後、ドライバーはまずタグに書き込み、他の場所で説明した一般的な"\*: WriteTag "の要件に準拠し、NDEF の読み取り/書き込みタグを読み取り専用に変換する必要があります。

## <a name="empty-ndef-record-ndefempty"></a>空の NDEF レコード: "NDEF: Empty"


このメッセージには、型、ID、またはペイロードがありません。 "NDEF: Empty" 型のサブスクリプションは、Windows クライアントの観点からは意味がないようです。

### <a name="required-actions"></a>必要なアクション

この種類のサブスクリプションまたはパブリケーションは、ステータス\_無効な\_パラメーターを使用して、近接プロバイダーのドライバーによって拒否される必要があります。

## <a name="subscriptions-for-all-ndef-types-ndef"></a>すべての NDEF 型のサブスクリプション: "NDEF"


クライアントは、受信したすべての NDEF メッセージをサブスクライブできます。 通常、関心のあるメッセージの種類をアプリケーションが認識している場合は、その型に特にサブスクライブします。 ただし、すべての NDEF メッセージをサブスクライブすると便利な場合があります。 たとえば、重複する NDEF タグをコピーして書き込むことができるアプリケーションは、このような場合に便利です。

### <a name="required-actions"></a>必要なアクション

ドライバーは、受信した各 NDEF メッセージと "NDEF" のサブスクリプションを一致させる必要があります。

## <a name="subscriptions-for-external-ndef-rtd-types-ndefext"></a>外部の NDEF RTD 型のサブスクリプション: "NDEF: ext"


ベンダーはカスタムの拡張可能な RTD 名前空間を使用して、独自のメッセージの内容を定義できます。 これにより、クライアントは、NFC フォーラムではなく、アプリまたはサードパーティによって定義された RTD 外部型をサブスクライブできます。

一般的な例型: "NDEF: ext.&lt;、&gt;"

具体的な例の種類: "NDEF: mytype"

### <a name="required-actions"></a>必要なアクション

ドライバーは、"NDEF: ext.&lt;中 Externaltype&gt;" のサブスクリプションと一致する必要があります。これは、TNF field の値が0x04 で、等価性に基づいて "&lt;ある Externaltype&gt;" と一致する TYPE フィールドを持つ受信 NDEF メッセージのみです。\[NFC RTD\]で指定された規則。

## <a name="subscriptions-for-ndefmime"></a>"NDEF: MIME" のサブスクリプション。


メッセージでは、MIME 名前空間を使用してメッセージの内容を定義できます。

一般的な型の例: "NDEF: MIME。&lt;SomeMimeType&gt;"

具体的な例の種類: "NDEF: MIME. image/jpeg"

### <a name="required-actions"></a>必要なアクション

ドライバーは、"NDEF: MIME" のサブスクリプションと一致している必要があります。&lt;SomeMimeType&gt;"は、TNF field 値が0x02 で、\[NDEF\]に指定されている等価性ルールに基づいて"&lt;SomeMimeType&gt;"に一致する型フィールドを持つ受信 NDEF メッセージのみです。

## <a name="subscriptions-for-ndefwkt"></a>"NDEF: wkt" のサブスクリプション。


メッセージでは、NFC フォーラムの既知の型の名前空間を使用して、メッセージの内容を定義できます。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、"NDEF: wkt" のサブスクリプションと一致している必要があります。&lt;SomeWellKnownType&gt;"は、TNF field 値が0x01 で、\[NDEF\]で指定された等価性ルールに基づいて"&lt;SomeWellKnownType&gt;"に一致する TYPE フィールドを持つ受信 NDEF メッセージのみです。
-   ドライバーは既知の型を検証する必要がないため、将来の既知の型は、ドライバーの更新を必要とせずに、NFC フォーラムで定義できます。

## <a name="subscriptions-for-unknown-ndef-type-ndefunknown"></a>不明な NDEF の種類のサブスクリプション: "NDEF: 不明"


これにより、クライアントはデータの型指定されていないペイロードをサブスクライブできます。

### <a name="required-actions"></a>必要なアクション

ドライバーが "NDEF: Unknown" のサブスクリプションと一致する必要があるのは、\[NDEF\]で指定されているように TNF field 値が0x05 の NDEF メッセージのみです。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


---
title: 双方向の要求と応答のスキーマ
description: 双方向の要求と応答のスキーマは、アプリケーションとプリンター間の双方向通信に使用できる、XML 形式のクエリと応答のセットを提供します。
ms.assetid: C005D90D-DCDB-410C-BD6F-83111849547E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a593d030c6109b5553975700e728cde159b2caec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841647"
---
# <a name="bidirectional-request-and-response-schemas"></a>双方向の要求と応答のスキーマ


双方向の要求と応答のスキーマは、アプリケーションとプリンター間の双方向通信に使用できる、XML 形式のクエリと応答のセットを提供します。 アプリケーションでは、これらのクエリを使用して、[双方向通信スキーマ](bidirectional-communication-schema.md)に従って保存されているプリンター構成と状態データを取得できます。 また、書き込み可能なプリンターのプロパティを設定することもできます。 [**IBidiSpl2:: SendRecvXMLStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)関数または[**IBidiSpl2:: SendRecvXMLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)関数のいずれかを使用して、プリンターと通信できます。

要求スキーマと対応する応答スキーマがいくつかあります。 各の正式な定義とそれぞれの例については、次のトピックを参考にしてください。

[要求と応答のスキーマを取得する](get-request-and-response-schemas.md)

[EnumSchema の要求と応答のスキーマ](enumschema-request-and-response-schemas.md)

[要求スキーマと応答スキーマを設定する](set-request-and-response-schemas.md)

[GetWithArgument の要求と応答のスキーマ](getwithargument-request-and-response-schemas.md)

要求または応答のルート要素は、その型を識別します。 &lt;EnumSchema&gt; の要求と応答は、アクセス可能なプリンターのプロパティの一覧を取得するために使用されます。 &lt;Get&gt; と &lt;&gt; 要求によって複数のクエリが許可されます。 "Query"&gt; &lt;セットは、設定するプロパティとそれに書き込む値を識別するだけです。

各 &lt;クエリ&gt; には、読み取り/書き込み対象のプロパティまたはプロパティ値を指す schema = 属性があります。 これらの schema = 属性の値は、双方向通信スキーマのツリー内のパスです。

たとえば、各 &lt;Get&gt; response は、クエリの元のセットを繰り返し、それぞれに結果を追加します。 各 &lt;セット&gt; 応答は、"クエリ" の元のセットを繰り返しますが、成功したクエリについては、それ以上のことはできません。 &lt;Get&gt; または &lt;&gt; 要求に対していずれかのクエリが失敗した場合、結果はエラーメッセージになります。

要求の構築の詳細については、「 [Bidi 通信スキーマクエリの構築](constructing-a-bidi-communication-schema-query.md)」を参照してください。

双方向通信スキーマの詳細については、[双方向通信スキーマ階層](bidirectional-communication-schema-hierarchy.md)と[Bidi 通信](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)スキーマのリファレンスに関するトピックを参照してください。

 

 





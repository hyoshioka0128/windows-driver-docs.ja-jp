---
title: WISPr 認証の概要
description: WISPr 認証の概要
ms.assetid: 49782d7f-c2f9-408d-971c-1af4d93d4d8d
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: c88a20513570bbe0b87407bd43961785ca70fc45
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608545"
---
# <a name="wispr-authentication-overview"></a>WISPr 認証の概要


ワイヤレス インターネット サービス プロバイダー ローミング (WISPr)-対応のホット スポットにはは、次のようなその captive portal のページで、ペイロードが含まれています。

``` syntax
<HTML> 
<!--
    <?xml version=”1.0” encoding=”UTF-8”?>
    <WISPAccessGatewayParam xmlns:xsi=”http://www.w3.org/2001/XMLSchema-instance”
      xsi:noNamespaceSchemaLocation=”http://www.acmewisp.com/WISPAccessGatewayParam.xsd”>
      <Redirect>
        <AccessProcedure>1.0</AccessProcedure>
        <AccessLocation>Hotel Contoso Guest Network</AccessLocation>
        <LocationName>Hotel Contoso</LocationName>
        <LoginURL>https://captiveportal.com/login</LoginURL>
        <MessageType>100</MessageType>
        <ResponseCode>0</ResponseCode>
      </Redirect>
    </WISPAccessGatewayParam>
--> 
</HTML>
```

Windows などのスマート クライアント (HTML コメントの表示が、顧客を回避するために含まれる) がこの XML を解釈し、については、ユーザーの資格情報を送信する必要があります。

顧客は、手動で WISPr 対応のネットワークに接続するときは、次のプロンプトが参照してください。

![wispr プロンプト](images/fig1-mb-wispr-auth-prompt.jpg)

選択したお客様**いいえ、サインアップする必要があります**captive portal に送信されます。 選択したお客様**はい、ユーザー名とパスワードを入力しますは**資格情報を入力するように求められます。 これらの資格情報は、web サイトに提供され、正常に認証した後、ユーザーが接続されています。

モバイル ブロード バンド アプリが自動的に資格情報を指定または調整された購入または認証フローを使用して、資格情報プロンプトを置換できます。 これには、ネットワークが WISPr をサポートすることと、ユーザーがネットワークに接続する前に、アプリをインストールすることが必要です。

ネットワークでは、特定の UserAgent 文字列を使用してクライアントに WISPr を提供する場合、ユーザーはこのプロンプトは表示されませんし、資格情報を手動で入力することはできません。 ただし、アプリは、ネットワーク プロファイルを作成するときに、適切な UserAgent を含めることによって WISPr 認証に参加もできます。

次のトピックがこのセクションに含まれます。

-   [ホット スポット認証のプロビジョニング](provisioning-for-hotspot-authentication.md)

-   [膨大な数の Ssid の処理](handling-large-numbers-of-ssids.md)

-   [ホット スポット認証イベントの処理](handling-the-hotspot-authentication-event.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ホット スポット認証方法](hotspot-authentication-methods.md)

 

 







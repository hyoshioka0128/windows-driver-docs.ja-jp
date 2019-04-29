---
title: ホットスポット認証のプロビジョニング
description: ホットスポット認証のプロビジョニング
ms.assetid: bfb4e1ec-9887-4b25-bfcc-be642b1a0101
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7c4492aa45e671f3ab9edc36c43169f2463bb01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391038"
---
# <a name="provisioning-for-hotspot-authentication"></a>ホットスポット認証のプロビジョニング


ホット スポット認証プロセスに参加するアプリでは、最初に Wi-fi ホット スポットの 1 つまたは複数のプロファイルを作成があります。 ここで説明されているエージェントのプロビジョニングのインターフェイスを使用してでは[メタデータを使用して、モバイル ブロード バンド エクスペリエンスを構成する](using-metadata-to-configure-mobile-broadband-experiences.md)します。 ホット スポットがオープン認証を使う必要があるあり、含める必要があります、 **HotspotProfile**要素。 プロビジョニング ファイルの次のサンプルは、SSID をアプリに関連付ける方法を示しています。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi___33</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
        <ExtAuth>
          <ExtensionId>YourAppIdGoesHere</ExtensionId>
        </ExtAuth>
        <TrustedDomains>
          <TrustedDomain>www.mycaptiveportal.com</TrustedDomain>
        </TrustedDomains>
        <UserAgent>contoso</UserAgent>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

ExtensionId フィールドには、ホット スポットの資格情報を生成するアプリのパッケージ ファミリ名が含まれています。 パッケージ ファミリ名は、Visual Studio によって自動的に生成します。 アプリケーションのパッケージ ファミリ名を検索して開く、 **package.appxmanifest** Visual Studio ソリューションでファイルを開き、[パッケージ] ウィンドウに移動します。

プロビジョニング ファイルが処理された後は、パッケージ ファミリ名"YourAppIdGoesHere"を持つアプリがホット スポット認証イベントの登録する必要があります。 必要なプロビジョニングのファイルがこのイベントを指定したアプリへのアクセス許可を最初に処理されます。 アプリでは、このイベントの 1 つのハンドラーを登録できます。 イベントの登録は、対応するアプリを参照するには少なくとも 1 つのプロファイルがある限り有効です。

## <a name="span-idsignspanspan-idsignspansign-the-provisioning-file"></a><span id="sign"></span><span id="SIGN"></span>プロビジョニング ファイルを署名します。


プロビジョニング後、ユーザーが終了またはでもアプリをアンインストール後も維持されるシステムの設定を変更するので、検証のより厳密なメジャーはほとんどの Api よりも必要です。 この検証は、オペレーターの特定のハードウェア (SIM)、暗号署名、およびユーザーの確認の組み合わせによって提供されます。 次の表では、確認の要件を示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>SIM の存在</th>
<th>ソースのプロビジョニング</th>
<th>署名の要件</th>
<th>ユーザーの確認の要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい、MB プロバイダー</p></td>
<td><p>モバイル ブロード バンド アプリ</p></td>
<td><p>なし</p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p>はい、MB プロバイダー</p></td>
<td><p>演算子の web サイト</p></td>
<td><p>証明書が必要です。</p>
<ul>
<li><p>信頼されたルート CA にチェーン</p></li>
<li><p>APN データベースでのモバイル ブロード バンド ハードウェアと関連付けるまたはメタデータが発生します。</p></li>
</ul></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p>いいえ、Wi-fi プロバイダー</p></td>
<td><p>モバイル ブロード バンド アプリまたは web サイト</p></td>
<td><p>証明書が必要です。</p>
<ul>
<li><p>信頼されたルート CA にチェーン</p></li>
<li><p>拡張された検証対象としてマークされます。</p></li>
</ul></td>
<td><p>ユーザーは、証明書が使用されます。 最初の時刻を確認するように求められます。その後 none です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WISPr 認証](wispr-authentication.md)

 

 







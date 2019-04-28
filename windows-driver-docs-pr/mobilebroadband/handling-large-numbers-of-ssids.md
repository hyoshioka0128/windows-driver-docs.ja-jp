---
title: 大きな数値の SSID の処理
description: 大きな数値の SSID の処理
ms.assetid: 52bcfbd4-98f6-43e3-b697-c632f6660717
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e69275cd0077265dacde979e24e4ddb50b4298a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380158"
---
# <a name="handling-large-numbers-of-ssids"></a>大きな数値の SSID の処理


このトピックでは、Ssid の多数の要求を処理する方法について説明します。

Windows 8.1 および Windows 10、1 つの WLAN プロファイルで構成できます。 Ssid の量を増やすことで Ssid の数が多いためサポートを大幅に向上します。 WLAN プロファイルは、最大 10,000 個の Ssid を含めるようになりましたことができます。 さらに、WLAN プロファイルは、SSID のプレフィックスをサポートします。

このトピックでは、次のセクションが含まれています。

-   [プロファイルごとの複数の Ssid](#multssidpro)

-   [セカンダリの Ssid](#secssd)

-   [プレフィックス](#prefixes)

-   [プロファイルの例](#example)

## <a name="span-idmultssidprospanspan-idmultssidprospanmultiple-ssids-per-profile"></a><span id="multssidpro"></span><span id="MULTSSIDPRO"></span>プロファイルごとの複数の Ssid


複数の Ssid に接続するには、Windows 8、Windows 8.1、または Windows 10 をプロビジョニングする場合は、プロファイルごとの複数の Ssid を指定することをお勧めします。 これが大幅にプロビジョニング ファイルのサイズを縮小し、コンピューターの応答性が向上します。

を使用するネットワークをマークする Api を使用する場合は、これらのアクションが同じプロファイルによってカバーされるすべての Ssid に適用されるを認識します。 そのため、これは 1 つのプロファイルに関連する Ssid をグループ化することをお勧めします。

可能性のある各 25 のプライマリ Ssid Windows 8 および Windows 8.1 で 10,000 Ssid 最大 10 個のプロファイルの最大ことができます。 Windows 8.1 では、別の 2 つの XML 名前空間の Ssid があります。 V1 名前空間には、Windows 8 のように最大 25 個の Ssid がサポートしています。 V2 名前空間には、最大 10,000 個の Ssid がサポートしています。 プロファイルは、v1 名前空間の 1 つ以上の SSID を指定する必要があり、合計で最大 10,000 個の Ssid を持つことができます。

## <a name="span-idsecssdspanspan-idsecssdspansecondary-ssids"></a><span id="secssd"></span><span id="SECSSD"></span>セカンダリの Ssid


Windows 8 には、プロファイルを対象となる Ssid の量が拡大する WLAN プロファイルの HotspotAuth セクション内のセカンダリ Ssid の概念が導入されました。 これは、Windows 8.1 および Windows 10 では、引き続きサポートしますが、セクションを使用して、SSID WLAN プロファイルの代わりをサポートすることをお勧めします。 自動接続のシナリオ。

プロファイルあたり 25 以上の Ssid を構成するには、Windows 8 で HotspotAuth セクションの SSIDConfig のでご注意くださいプロファイルごとにセカンダリの Ssid を指定できます。 これにより、これらのネットワークの追加のプロファイルを作成できませんが、その SSID とプロファイルのホット スポットの設定を関連付けます。

ユーザーが手動で今後接続し、新しいプロファイルを作成、このプロファイルのホット スポットの設定は、ユーザーが作成したプロファイルと自動的に関連付けします。 セカンダリの Ssid 自動的なので、接続ユーザー手動で接続するとに 1 回、しない限り、これら、ほとんどのユーザーが発生しない小さい共通のネットワークがあります。

最大 250 のセカンダリ Ssid プロファイルごとのことができます。

## <a name="span-idprefixesspanspan-idprefixesspanprefixes"></a><span id="prefixes"></span><span id="PREFIXES"></span>プレフィックス


Ssid の特に大規模なまたは動的なセットを関連付けるには、SSID の一覧は静的 Ssid だけでなく、プレフィックスを含めることができます。 これにより、4 つ以上のオクテットを共通の SSID の先頭にある Ssid の広範なセットと、モバイル ブロード バンドのアプリを関連付けることができます。

Windows 8、SSID のプレフィックスは、セカンダリの SSID リストのみでサポートされています。 Windows 8.1 および Windows 10 では、SSID のプレフィックスは、v2 名前空間を使用して、WLAN プロファイルの SSIDConfig セクションでサポートされます。

## <a name="span-idexamplespanspan-idexamplespanexample-profile"></a><span id="example"></span><span id="EXAMPLE"></span>プロファイルの例


このセクションでは、v1 と v2 と名前空間ごと、SSID のプレフィックスの SSID を格納しているプロファイルの例を示します。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1"
             xmlns:v2="http://www.microsoft.com/networking/CarrierControl/WLAN/v2">
  <name>SampleProfile</name>
  <SSIDConfig>
    <SSID>
        <name>MySSID1</name>
    </SSID>
    <v2:SSID>
        <v2:name>MySSID2</v2:name>
    </v2:SSID>
    <v2:SSIDPrefix>
        <v2:name>MySSIDPrefix</v2:name>
    </v2:SSIDPrefix>
  </SSIDConfig>
  <MSM>
    <security>
        <authEncryption>
            <authentication>open</authentication>
            <encryption>none</encryption>
            <useOneX>false</useOneX>
        </authEncryption>
    </security>
  </MSM>
</WLANProfile>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WISPr 認証](wispr-authentication.md)

 

 







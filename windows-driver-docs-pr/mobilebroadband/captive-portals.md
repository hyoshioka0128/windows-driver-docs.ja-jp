---
title: Captive ポータル
description: Captive ポータル
ms.assetid: 6f710440-3012-4bf4-92cc-3743b0f4fd34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a014465c600787e2c878dd17a3c572607a338128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549361"
---
# <a name="captive-portals"></a>Captive ポータル


ほとんどのホット スポットでは、制限されたネットワーク接続するすべてのクライアントの HTTP 要求がプロバイダーの web サイトにリダイレクトされます、captive portal を使用する顧客との対話を実装します。 Web サイトでは、オペレーターの条項および条件に同意するユーザー、お支払い情報を入力するかを以前の支払の並べ替え方法を確認します。 資格情報を入力し、ことができます。

いくつかの問題は、このようなエクスペリエンスを使用してが存在します。

-   (メール クライアント) などの他のアプリケーションもリダイレクトします。 ユーザーが最初に web ブラウザー以外のアプリを使用しようとすると、これらが問題を解決する方法を知らなくてもエラーが発生します。

-   最初の接続試行がセキュリティで保護されたソケット レイヤー (SSL) 経由で行われた場合、ブラウザーは captive portal にユーザーをリダイレクトする前に、ユーザーにセキュリティ警告を表示します。 接続するためにセキュリティの警告を無視する必要がありますので、ユーザーの混乱を招くエクスペリエンスが作成されます。

Windows 8、Windows 8.1、および Windows 10、captive portal が検出された場合、すぐに web ブラウザーを開き、captive portal のネットワークをサポートします。 Captive portal を使用して認証を実行する必要があります、どのような操作を理解するに役立つ、各自のデバイスのフォア グラウンドで、ブランド化された web ページが表示されます。

Windows では、ユーザーが以降の接続試行で captive ポータルをバイパスできるできるメカニズムを提供します。 ただし、captive portal は、初めてユーザーが遭遇するエクスペリエンスでは常にします。

このトピックでは、専用のポータルを使用するための次のベスト プラクティスについて説明します。

-   [一貫性のある接続の処理](#cch)

-   [タッチ操作に適した web ページ](#touchfr)

-   [購入後にプロビジョニングします。](#pap)

-   [プランのアプリのインストール](#appinst)

## <a name="span-idcchspanspan-idcchspanconsistent-connection-handling"></a><span id="cch"></span><span id="CCH"></span>一貫性のある接続の処理


Windows をクライアントが最初に、ネットワークに接続するときにインターネット接続および captive portal のステータスを確認するには、一連のネットワーク テストを実行します。 これらのテストの接続先サイトが**msftncsi.com**接続をテストするためだけに使用される予約済みのドメインであります。 Captive portal が検出されると、これらのテストは定期的に繰り返されます captive portal がリリースされるまで。

False の正の値または false ネガティブ テスト結果を避けるためには、captive portal が、以下を実行します。

- アクセスを許可する<strong>www.msftncsi.com</strong>ときに、ユーザーがインターネットにアクセスします。

- クライアントに表示される captive portal の動作を変更します。 たとえばは一部の要求をリダイレクトされず、他の要求をドロップ認証が成功するまで、すべての要求をリダイレクトする続行する必要があります。

  **注:**  
  クライアント、クライアントあたりの試行の数またはすべてのクライアントからの合計試行しないあたりの試行の頻度に基づいて、サービスの軽減策の拒否する必要があります。

     

## <a name="span-idtouchfrspanspan-idtouchfrspantouch-friendly-web-pages"></a><span id="touchfr"></span><span id="TOUCHFR"></span>タッチ操作に適した web ページ


Windows 8、Windows 8.1、および Windows 10 エクスペリエンスはタッチ ファーストに設計されています。 これは、web ページに拡張されます。 タッチ ユーザーより大規模でターゲットへのコントロールと、web ページをレイアウトするために検討してください。 過剰なにスクロールすると、対話を必要としないようにし必要に応じて、複数のページにフローを中断するレイアウトを使用します。 タッチ操作に適した web デザインの詳細については、[タッチ入力のための設計](https://msdn.microsoft.com/library/windows/apps/hh465415.aspx)を参照してください。

## <a name="span-idpapspanspan-idpapspanprovision-after-purchase"></a><span id="pap"></span><span id="PAP"></span>購入後にプロビジョニングします。


アプリによって適用される同じプロビジョニング ファイルは、web サイトによっても適用できます。 Web ページの JavaScript での可用性の確認、 [ **window.external.msProvisionNetworks** ](https://msdn.microsoft.com/library/dn529170)メソッド。 存在する場合、ブラウザーは、オペレーティング システムにプロビジョニング ファイルを中継できます。 参照してください[メタデータを使用して、モバイル ブロード バンド エクスペリエンスを構成する](using-metadata-to-configure-mobile-broadband-experiences.md)このプロビジョニング ファイルを生成する方法の詳細について。

**注**   web サイトまたはモバイル ブロード バンド アプリではないアプリで提供されているときに、このプロビジョニング ファイルを署名する必要があります。

 

XML を渡すプロビジョニング ファイルにより、別のサービス セット識別子 (Ssid) がある場合でも、ユーザーのサービスに含まれている他のネットワークに自動的に接続するオペレーティング システムです。 静的ワイヤレス インターネット サービス プロバイダー ローミング (WISPr) の資格情報を使用するでは、今後、Windows は、これらの資格情報で認証できる自動的にあるために、そのより滑らかな接続エクスペリエンスもできます。

## <a name="span-idappinstspanspan-idappinstspanoffer-app-installation"></a><span id="appinst"></span><span id="APPINST"></span>プランのアプリのインストール


Windows 8、Windows 8.1、および Windows 10 の豊富なエクスペリエンスでは、モバイル ブロード バンド アプリを使用することです。 ユーザーのインターネット接続を取得する前に、アプリをインストールすることはできませんので captive ポータルは、Microsoft Store での 1 つだけのアプリへのアクセスを許可することはできません。 ただし、ユーザーが認証されると、モバイル ブロード バンド アプリをインストールする Microsoft Store に転送することを検討します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ホット スポット認証方法](hotspot-authentication-methods.md)

 

 







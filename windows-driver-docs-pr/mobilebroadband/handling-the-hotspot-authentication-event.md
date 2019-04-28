---
title: ホットスポット認証イベントの処理
description: ホットスポット認証イベントの処理
ms.assetid: e293757e-de4b-4669-a6c4-a57fff157cf4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c31bc322f1d13a0df31179eec2459c63e64a1bd4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380157"
---
# <a name="handling-the-hotspot-authentication-event"></a>ホットスポット認証イベントの処理


Windows 8、Windows 8.1、および Windows 10 ローミング (WISPr) をホット スポット認証イベント ワイヤレス インターネット サービス プロバイダーをサポートする専用ポータルを検出したときにトリガーします。

受信側のアプリがすぐに呼び出す必要があります、イベントの発生時に、 [ **Windows.Networking.NetworkOperator.HotspotAuthentication.TryGetAuthenticationContext** ](https://msdn.microsoft.com/library/windows/apps/hh758381)イベント トークンを使用して関数イベント ハンドラーへの引数として提供されます。 この関数は、ホット スポット認証の試行を管理するオブジェクトを返します。 関数が失敗したこと、イベント ハンドラーを追加アクションを実行せず終了する必要があります。

オブジェクトのプロパティは、次の項目を取得するようアプリを許可します。

-   ワイヤレス ネットワークの SSID です。

-   ホット スポットに接続されているネットワーク アダプターに関する詳細です。

-   WISPr メッセージを含む URL。

-   WISPr メッセージの XML ペイロード。

-   認証 URL は、資格情報を指定します。

その他の Api は、次の項目を取得するが存在します。

-   ワイヤレス ネットワークの BSSID (を参照してください[ **Windows.Networking.Connectivity 名前空間**](https://msdn.microsoft.com/library/windows/apps/br207308))。

-   ネットワークの DHCP のパラメーター (を参照してください[Win32 および COM UWP アプリの](https://msdn.microsoft.com/library/windows/apps/br205757))。

この情報と、アプリがローカル システムまたはネットワークから取得する必要があるその他の情報を使用して、資格情報を生成できます。 オブジェクトには、続行するかホット スポット認証を完了するアプリを許可するメソッドも含まれています。

次のセクションでは、このトピックで使用できるとおりです。

-   [問題の資格情報](#issuecred)

-   [認証を中止します。](#abortauth)

-   [代替の認証方法を使用します。](#altauth)

-   [ユーザーと対話します。](#userint)

## <a name="span-idissuecredspanspan-idissuecredspanissue-credentials"></a><span id="issuecred"></span><span id="ISSUECRED"></span>問題の資格情報


最も簡単なケースでは、アプリは、または取得した情報に基づいて資格情報を生成します。 たとえば、ユーザー名とパスワードが WISPr ペイロード内の情報と、ネットワーク アダプターに関する情報を使用して生成されます。

アプリ側で生成または資格情報の取得に必要なすべてのアクションを実行した後、 [ **IssueCredentials** ](https://msdn.microsoft.com/library/windows/apps/hh758375)メソッドを[ **HotspotAuthenticationContext**](https://msdn.microsoft.com/library/windows/apps/hh758372)オブジェクト。 このメソッドは、次を指定するアプリを許可します。

-   WISPr *UserName*パラメーター

-   WISPr*パスワード*パラメーター

-   WISPr 応答に含める任意の標準パラメーター

-   エラー発生時の動作

サーバーは、アプリによって提供された資格情報を拒否する場合 Windows はネットワークから切断し、現在のユーザー セッション内の接続を再試行しません。 最終的なフラグでは、資格情報が成功した場合は、Windows はこのプロファイルを使用して接続を自動的に再試行する必要がありますを指定するアプリケーションを使用します。

この API の 2 つのバリエーションがあります。 [ **IssueCredentials** ](https://msdn.microsoft.com/library/windows/apps/hh758375)メソッドは、パラメーターには、Windows とすぐに戻ります。 この API では、認証の試行の結果は提供されません。 [ **IssueCredentialsAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266072) Windows 8.1 で導入されたメソッドは、アプリケーションは、認証の試行の結果を取得できるようにする非同期バージョン。

## <a name="span-idabortauthspanspan-idabortauthspanabort-authentication"></a><span id="abortauth"></span><span id="ABORTAUTH"></span>認証を中止します。


現在のネットワークの資格情報を生成できないことに、アプリが検出された場合 (ローミングの契約が変更されているため、情報が使用不可能、またはその他の理由)、呼び出す必要があります、 [ **AbortAuthentication**](https://msdn.microsoft.com/library/windows/apps/hh758373)メソッドを[ **HotspotAuthenticationContext** ](https://msdn.microsoft.com/library/windows/apps/hh758372)オブジェクト。

Windows では、ネットワークから切断し、現在のユーザー セッション内の接続を再試行しません。 この関数は、Windows を示すフラグは、このプロファイルを使用して接続を再試行する自動的に受け入れます。

**注**  このメソッドは、システムから、プロファイルを削除およびアプリ問い合わせることができる資格情報をもう一度、ユーザーが手動でネットワークに接続を試行かどうか。 プロファイルが完全に削除すると、アプリは関連付けられているプロファイルを削除する新しいプロビジョニング ファイルを指定する必要があります。

 

## <a name="span-idaltauthspanspan-idaltauthspanuse-alternate-authentication-methods"></a><span id="altauth"></span><span id="ALTAUTH"></span>代替の認証方法を使用します。


WISPr 以外の方法を使用して、アプリを認証できる場合に、行うことがあります。 代替のメソッドを使用して、ネットワークに認証が成功、呼び出すことによって、接続を完了にする必要があります、 [ **SkipAuthentication** ](https://msdn.microsoft.com/library/windows/apps/hh758379)メソッドを[ **HotspotAuthenticationContext** ](https://msdn.microsoft.com/library/windows/apps/hh758372)オブジェクト。 このメソッドが呼び出されると、Windows はユーザー インターフェイス (UI) を正しく認証された状態を反映するを支援し、インターネットへの接続を再検出します。

**注**  ホット スポットが WISPr プロトコルのサポートをアドバタイズしません、HotspotAuthentication イベントは呼び出されません。 ただし、これにより、応答に使用する別のプロトコルを選択するアプリまたは必要な場合は、WISPr のカスタム バージョンを使用します。

 

## <a name="span-iduserintspanspan-iduserintspaninteract-with-the-user"></a><span id="userint"></span><span id="USERINT"></span>ユーザーと対話します。


認証を続行する前に、ユーザーの介入が必要な場合、アプリを呼び出す必要があります、 [ **TriggerAttentionRequired** ](https://msdn.microsoft.com/library/windows/apps/hh758380)メソッドを[ **HotspotAuthenticationContext** ](https://msdn.microsoft.com/library/windows/apps/hh758372)オブジェクト。 このメソッドでは、次の状況で役立ちます。

-   ユーザーに、アプリケーションに資格情報を保存しましたが、サインインする必要があります。

-   ユーザーのクレジット カードまたはその他のアカウントに課金される接続の完了そのため、続行する前に同意が必要です。

-   ユーザーのアカウントのクレジットがなく、新しく購入が必要です。

このメソッドは、認証を完了できません。 このメソッドが呼び出されたときに、指定された引数を使用して、フォア グラウンドで開く、アプリを要求します。 イベントのトークンは、取得できるように、フォア グラウンド アプリケーションに渡す必要があります、 [ **HotspotAuthenticationContext** ](https://msdn.microsoft.com/library/windows/apps/hh758372)その他の 3 つを使用して、もう一度オブジェクトと認証メソッド。

アプリの要求をフォア グラウンドで開くを成功させるのには保証されません。 HotspotAuthentication イベントは、自動接続により、コンピューターがコネクト スタンバイの間に発生します。 コンピューターがコネクト スタンバイになってがロックを解除されたおよびがまだワイヤレス ネットワークに接続されている場合にのみ、アプリが起動します。 インターネットにアクセスできるユーザー、コンピューターのロックを解除するまで遅延ため、資格情報を自動的に生成するたびにこの状態が回避する必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WISPr 認証](wispr-authentication.md)

 

 







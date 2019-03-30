---
title: デスクトップ COSA/APN データベースの設定
description: デスクトップ COSA/APN データベースの設定
ms.assetid: 860B8587-1D70-466A-A6E7-836380AA4DFA
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 35cd4a2c3c52ad09012a316ada8a1da7a35842c1
ms.sourcegitcommit: bb4f9c8dab2f4cb7a57ebd30457f427d909c928f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2019
ms.locfileid: "58624777"
---
# <a name="desktop-cosaapn-database-settings"></a>デスクトップ COSA/APN データベースの設定

このトピックでは、デスクトップ COSA で使用できる設定と APN データベース (apndatabase.xml) について説明します。

デスクトップ COSA/APN データベースの送信処理に関する詳細については、次を参照してください。[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。

COSA に関する詳細については、次を参照してください。 [COSA 概要](cosa-overview.md)します。

APN データベースに関する詳細については、次を参照してください。 [APN データベースの概要](apn-database-overview.md)します。

## <a name="apn-database-only-settings"></a>APN データベース専用の設定

スプレッドシートの次の設定は、APN データベースのみに適用されます。 これらのエントリは、Windows 8、Windows 8.1、または Windows 10、Windows 10 バージョン 1703 より前に、のバージョンを対象としている場合に使用されます。

| 設定名 | 説明 | 省略可能または必須 | メモ |
| --- | --- | --- | --- |
| CDMA ProviderID | 5 桁の番号で、デバイスによって報告された (SID とも呼ばれます) CDMA プロバイダー ID に一致する必要があります。 | 省略可能 | |
| CDMA ProviderName | デバイスによって報告された CDMA プロバイダー名と同じ 36 個の文字の文字列。 この設定は、大文字小文字を区別します。 | 省略可能 | |
| CertIssuerName | 演算子の XML のプロビジョニングに使用される署名証明書の証明書の発行者名。 | 省略可能 | 指定した場合は、証明書のサブジェクト名とキャリアの GUID を指定する必要がありますもします。 |
| CertSubjectName | 演算子の XML のプロビジョニングに使用される署名証明書の証明書のサブジェクト名。 | 省略可能 | 指定した場合は、証明書の発行者名とキャリアの GUID を指定する必要がありますもします。 |
| 通信事業者 GUID | 自己割り当てられた GUID ですが演算子 XML プロビジョニング パッケージでは将来使用します。 | 省略可能 | 指定した場合は、証明書のサブジェクト名と発行者の証明書名を指定する必要がありますもします。 |
| GSM ProviderName | デバイスによって報告された GSM プロバイダー名と同じ 36 個の文字の文字列。 この設定は、大文字小文字を区別します。 | 省略可能 | この設定は、Windows 8.1 および Windows 10、Windows 10 バージョン 1703 より前に、のバージョンでのみサポートされます。 |
| 購入 | APN のプロビジョニングする場合ははいまたは no の値を記述するまたは購入。 | 必須 | 設定可能な値: <ul><li>**Y** APN のプロビジョニングまたは購入する場合。</li><li>**N** APN がプロビジョニングまたは購入ではない場合。</li></ul> <p>場合**購入フラグ**設定は**Y**、**接続フラグ**設定である必要があります**N**します。</p> |
| 接続 | APN のプロビジョニングする場合ははいまたは no の値を記述するまたは購入。 | 必須 | 設定可能な値: <ul><li>**Y** APN のプロビジョニングまたは購入する場合。</li><li>**N** APN がプロビジョニングまたは購入ではない場合。</li></ul> <p>場合**接続フラグ**設定は**Y**、**購入フラグ**設定である必要があります**N**します。</p> |

## <a name="apn-database-and-desktop-cosa-settings"></a>APN データベースおよびデスクトップ COSA の設定

次のエントリは、APN データベースとデスクトップ COSA の両方に適用されます。 COSA のために必要な Windows のサポートされる最小バージョンは最後の列に示されます。


| 設定名 | 説明 | 省略可能または必須 | メモ | COSA のサポートされる最小の Windows バージョン |
| --- | --- | --- | --- | --- |
| 更新の種類 | APN データベースのエントリは、新しいまたは変更されたかどうかについて説明します。 | 必須 | 設定可能な値: <ul><li>**追加**– 新しいエントリ</li><li>**変更**– 既存のエントリの更新</li><li>**保持**– エントリを変更しないでください</li><li>**削除**– エントリを削除します</li></ul> | Windows 10 Version 1703 |
| 国/地域 | 国またはリージョン APN エントリの。 | 必須 | このエントリは、特定の国または地域に Windows の参照を一致するように変更可能性があります。 |  Windows 10 Version 1703 |
| 演算子 | オペレーターの名前。 このフィールドに国または地域を含める必要はありません。 | 必須 | 同じスペルおよび大文字と小文字、APN エントリの更新を送信するたびに使用することを確認します。 | Windows 10 Version 1703 |
| MCC | GSM IMSI 送信するため、3 桁の MCC 値。 | ICCID の範囲内の省略可能です。 |  | Windows 10 Version 1703 |
| MNC | GSM IMSI 送信に使用する 2 桁または 3 桁 mnc も値。 | ICCID の範囲内の省略可能です。 |  | Windows 10 Version 1703 |
| IMSI 範囲 - 開始 | 数の先頭の MCC + mnc も含む 15 桁の数。 | 省略可能 | 数は、00 で終了する必要があります。 <p>場合この設定と**IMSIRange - 終了**設定は空白のままが、 **MCC**と**mnc も**エントリを指定すると、MCC + mnc も範囲全体をカバーします。</p> | Windows 10 Version 1703 |
|  IMSI 範囲の終了  | 数の先頭の MCC + mnc も含む 15 桁の数。 | 省略可能 | 数が 99 で終わる必要があります。 <p>場合この設定と**IMSI 範囲 - 開始**設定は空白のままが、 **MCC**と**mnc も**エントリを指定すると、MCC + mnc も範囲全体をカバーします。</p> | Windows 10 Version 1703 |
| ICCID の範囲の開始 |  89 (ICCID 発行者の識別番号) で始まる 19 や 20 桁の数。 | 省略可能 | 数は、00 で終了する必要があります。  | Windows 10 Version 1703 |
| ICCID の範囲の終了  |  89 (ICCID 発行者の識別番号) で始まる 19 や 20 桁の数。 | 省略可能 | 数が 99 で終わる必要があります。  | Windows 10 Version 1703 |
| AccountExperienceURL |  Windows 接続マネージャーでは、ユーザーは、アクティブなプランがありません、ネットワークに接続しようとする場合に使用されます。  | 省略可能 | プランの購入エクスペリエンスを向上させることです。 <p>場合**両方**AppID と AccountExperienceURL が指定されて、AppID は、優先順位の高いを受け取るし、UX は**いない**AccountExperienceURL を表示します。</p> | Windows 10 Version 1703 |
| FriendlyName | 分かりやすく、意味のあるサブスクライバーには、この APN エントリの名前。 | 省略可能 | Windows ことはできません、ネットワークに自動的に接続されている場合、Windows 接続マネージャーで表示されます。 | Windows 10 Version 1703 |
| AccessString | GSM ネットワークでは、これは、APN data.contoso.com などです。 CDMA ネットワークでは、これは #777 またはネットワーク アクセス識別子などの特殊なダイヤル コードをなどが含まれるアクセス文字列example@contoso.comします。 | 必須 |  | Windows 10 Version 1703 |
| UserName | ユーザー名が、APN に接続するために使用します。 この設定は、大文字小文字を区別します。  | 省略可能 |  | Windows 10 Version 1703 |
| パスワード |  APN への接続に使用するパスワード。 この設定は、大文字小文字を区別します。  | 省略可能 |  | Windows 10 Version 1703 |
| AuthProtocol | パケット データ プロトコル (PDP) コンテキストのアクティブ化に使用する認証プロトコルを指定します。 | 省略可能 | 設定可能な値: <ul><li>**NONE** – 認証プロトコルは不要です</li><li>**PAP** – PAP 認証が必要です。</li><li>**CHAP** – CHAP 認証が必要です。</li><li>**MsCHAPV2** – MSCHAPv2 では、認証が必要です。</li></ul> <p>この設定は、Windows 8.1 および Windows 10、Windows 10 バージョン 1703 より前に、のバージョンでのみサポートされます。</p> | Windows 10 Version 1703 |
| 圧縮 | ヘッダーとデータ転送の圧縮を使用データ リンクではかどうかを指定します。  | 省略可能 | 設定可能な値: <ul><li>**有効にする**– 圧縮が有効になっています。</li><li>**無効にする**– 圧縮が有効になっていません</li></ul> <p>この設定は、Windows 8.1 および Windows 10、Windows 10 バージョン 1703 より前に、のバージョンでのみサポートされます。</p> | Windows 10 Version 1703 |
| AutoConnectOrder | Windows では、オペレーターによって提供され、「自動接続」APN データベースまたは COSA まで、モバイル、ネットワークに接続が成功としてマークされている APNs への接続を試みます。 すべてを自動接続試行の失敗、Windows でユーザーが、APN を選択するか、カスタム APN を入力できるように、プロンプトが表示されます。 | 省略可能 | 演算子の 1 つ以上のアクセス文字列をした場合、この設定は、1 から始まる必要があります。 これは Windows IMSI 範囲、ICCID 範囲、CDMA プロバイダーの ID、または CDMA を共有するいくつかの APN エントリを試みる必要、ユーザー接続を試みたときに、プロバイダー名。 | Windows 10 Version 1809 |

## <a name="desktop-cosa-only-settings"></a>デスクトップ COSA 専用の設定

次の設定は、デスクトップ COSA のみに適用されます。 これらのエントリは、Windows 10 バージョン 1703 以降を対象としている場合に使用されます。

| 設定名 | 説明 | 省略可能または必須 | メモ | 最小のサポートされている Windows バージョン |
| --- | --- | --- | --- | --- |
| SupportDataMarketplace | プロファイルのエントリが Mobile 計画をサポートしているかどうかを説明する true または false の文字列。 | 省略可能 | <p>この設定を有効にする前に確認してください、モバイル オペレーターが Mobile プラン プログラムの一部であります。</p><p>"False"というかどうか、空白の既定値</p> | Windows 10 Version 1703 |
| SPN (SPN) | サービス プロバイダー名 (SPN) の識別子の文字列 | 省略可能 | 月/MVNO のネットワークを識別するのに役立ちます。 空白の場合は、既定値は空の文字列とは何も行いません。 | Windows 10 Version 1703 |
| AlwaysOn | 接続が常にでかどうかについて説明します。 | 必須 | かどうか、空白が"true"にします既定値。 | Windows 10 Version 1703 |
| PurposeGroups | 目的の値を表す Guid のコンマ区切りリストで、接続の目的を指定する文字列。 | 必須 | 次の目的の値を使用できます。 <ul><li>**インターネット**</li><li>**MMS**</li><li>**IMS**</li><li>**SUPL**</li><li>**購入**</li><li>**管理**</li><li>**アプリケーション**</li><li>**esim 状のプロビジョニング**</li></ul> <p> 「インターネット」場合、空白の既定値。</p> | Windows 10 Version 1703 |
| | | 省略可能 | 次の省略可能な目的のグループ値提供されています。 <ul><li>**LTE をアタッチします。** </li></ul> LTE 接続を指定する COSA を通じて APN 通常必要はありません接続情報は、通常、基になるモデムのハードウェアで直接管理されるためです。 ただしでモデムのハードウェアには、APN の値をアタッチ、LTE はありませんし、ネットワークが、UE を 1 つの割り当ての対応がない場合、MO 必要に応じて指定できます LTE がユーザーに値を手動で入力することがなく、UE は LTE アタッチできるように、情報をアタッチします。 | Windows 10、バージョンが 1903 |
| IPType | 接続のネットワーク プロトコルを指定する文字列。 | 省略可能 | 設定可能な値: <ul><li>IPv4</li><li>IPv6</li><li>IPv4v6</li></ul> <p>かどうかは空白、既定値は"IPv4"にします。</p> | Windows 10 Version 1703 |
| BrandingName | 通常、モバイル ブロード バンド デバイスは、Windows、Windows 接続マネージャーを表示するオペレーター名を提供します。 この名前は、メタデータにカスタム名を指定することによってオーバーライドできます。 | 省略可能 | 空白の場合は、既定値は空の文字列とは何も行いません。 | Windows 10 バージョン 1709 |
| BrandingIcon | ネットワーク エントリの横にある Windows 接続マネージャーに表示されるカスタム ロゴです。 | 省略可能 | 透明な背景と縁を滑らかにアイコンがあります。 ライトとダーク テーマにアイコンをテストすることをお勧めします。 次の形式とサイズ要件も満たす必要があります。 <ul><li>256 x 256:+ 32 ビットのアルファ</li><li>48 x 48:+ 32 ビットのアルファ</li><li>48 x 48:8 ビット 256 色</li><li>48 x 48:4 ビットの 16 色</li><li>32 x 32:+ 32 ビットのアルファ</li><li>32 x 32:8 ビット 256 色</li><li>32 x 32:4 ビットの 16 色</li><li>24 x 24:+ 32 ビットのアルファ</li><li>24 x 24:8 ビット 256 色</li><li>24 x 24:4 ビットの 16 色</li><li>16 x 16:+ 32 ビットのアルファ</li><li>16 x 16:8 ビット 256 色</li><li>16 x 16:4 ビットの 16 色</li></ul> | Windows 10 バージョン 1709 |
| UseBrandingNameOnRoaming | ブランド化は、ローミングやローミングされていない中に表示されるかどうかを決定します。 | 省略可能 | 設定可能な値: <ul><li>**0** -ホーム ネットワークに接続するときに使用</li><li>**1** -ホーム ネットワークや国内のローミングに接続するときに使用</li><li>**2** -ホーム ネットワーク、国内の移動、および海外ローミングに接続するときに使用</li></ul><p> かどうかは空白、既定値は 0。</p> | Windows 10 バージョン 1709 |
| Roaming | 接続のアクティブ化するローミングの条件を指定します。 | 省略可能 | 設定可能な値: <ul><li>0:ホーム ネットワークのみ</li><li>1:ローミングのすべての条件 (ホームおよび移動)</li><li>2:ホームと国内のみローミング</li><li>3:国内のみローミング</li><li>4:非国内でのみローミング</li><li>5:のみローミング</li></ul> 1 (すべてのローミング条件) かどうか、空白の既定値します。 | Windows 10 バージョン 1709 |
| DataMarketplaceRoamingUIEnabled | この設定は、SIM またはプランのモバイル サービスの一部である esim 状の移動 UI を表示する必要があるかどうかを制御します。 | 省略可能 | この設定の連携、 **SupportDataMarketPlace**設定します。 設定できる値は次のとおりです。 <ul><li>0:ローミングのインジケーターは**決して**表示されます。</li><li>1:他の国で、デバイスがローミング時に、ローミングのインジケーターが表示されます。</li></ul> <p>既定で空白の場合**1**します。</p> | Windows 10 バージョン 1709 |
| UIName | ターゲット条件の値 (SPN、MCC、mnc も、IMSI 範囲、ICCID 範囲など) は、一意のエントリを示すことはできない場合、COSA は手動で使用するどの月の接続値の選択を有効にするには、エンドユーザーにこの名前が表示されます。 | 省略可能 | たとえば、 **ContosoMVNO** MVNO です。 メインの MO ネットワークからそれ自体を区別するために使用できる一意の値がない**Contoso**します。 この場合、 **UIName**ことができ、手動で使用する設定をプロビジョニングする月を選択するユーザーを有効にすると、Windows の設定 UI に表示されます。 | Windows 10 バージョン 1709 |
| UIOrder | コントロールのインデックス、 **UIName**値のドロップダウン リスト ピッカーの位置。 | 場合に、必ず**UIName**を指定します。それ以外の場合 (省略可能) | 指定しない場合、既定値は**0**します。 | Windows 10 バージョン 1709 |
| ESIM_PROV | プロファイルがプロビジョニング プロファイル、eSIM と見なされるかどうかを示す true または false の文字列。 | **重要な**省略可能、MO サポートしていない限り、esim 状のプロビジョニング プロファイルの場合はの指定が必要です。 | <p>"False"というかどうか、空白の既定値</p> <p>プロビジョニング プロファイル、eSIM とは、単一目的のためのプロファイルです。 EUICC がインストールされていると、は、通常、運用の eSIM のプロファイルを購入するには高いガーデニングの月の限られた接続を確立するために、ユーザーの機器ができます。</p> | Windows 10 バージョン 1709 |
| AppID | 通信事業者の UWP コンパニオン アプリのアプリケーション ID、パッケージ ファミリ名 (PFN) を記述する文字列。 | 省略可能 | Windows 10、バージョン 1803 以降で**AppID**それぞれのコンパニオン アプリと共に MOs の識別に使用します。 **AppID**形式で宣言する必要があります。 <p>**PFN!AppId**</p><p>**注**この形式は大文字小文字を区別します。</p><p>アプリの PFN とアプリ Id を取得するには、次の手順に従います。<ol><li>PFN を取得で指定した[ビュー アプリ Id の詳細](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)します。</li><li>開き、ソリューションの AppId を見つける*AppManifest.XML*ファイルとアプリケーション ID の appxmanifest ファイルの照会</li></ol> <p>UWP MOs のコンパニオン アプリに関する詳細については、次を参照してください。 [UWP モバイル ブロード バンド アプリ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/windows-store-mobile-broadband-apps)します。</p> | Windows 10 バージョン 1803 |
| ホット スポット | 個人用のホット スポットとして、モバイル ブロード バンド接続を共有するユーザーを許可するかどうかを決定します。 | 省略可能 | 設定可能な値: <ul><li>しない</li><li>常に </li><li>EntitlementCheckRequired</li></ul> <p>常にします"場合、空白の既定値。</p> <p>*EntitlementCheckRequired*権利チェックは、Windows 通知イベントのハンドラーを必要とすると、ホット スポットを共有するユーザーを有効にします。 このオプションが選択されている場合は、権限チェックの要求を処理するために月 UWP コンパニオン アプリを開発する必要があります。</p> <p>UWP MOs のコンパニオン アプリに関する詳細については、次を参照してください。 [UWP モバイル ブロード バンド アプリ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/windows-store-mobile-broadband-apps)します。</p><p>EntitlementCheck API についての詳細については、次を参照してください。 その[UWP API のリファレンス ページ](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.tetheringentitlementchecktriggerdetails)します。</p> | Windows 10 バージョン 1803 |
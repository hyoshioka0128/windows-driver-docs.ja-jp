---
title: サービス メタデータ
description: サービス メタデータ
ms.assetid: daf5db05-cf39-4ff2-a2f1-0ffd718c638e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b779bff8cc0e66a374077dae21e552ebabf45a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571814"
---
# <a name="service-metadata"></a>サービス メタデータ

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

作成し、Windows と緊密に統合されているエクスペリエンスを作成するためのサービス メタデータ パッケージを送信できます。 オペレーターのサービス メタデータ パッケージと一致するモバイル ブロード バンド ハードウェアが検出されると、Windows サービスのメタデータと、指定したモバイル ブロード バンド アプリが自動的にダウンロードします。

サービス メタデータには、次を含む、サービスを記述する情報が含まれています。

-   サービスのプロバイダー名

-   1 つまたは複数のサービスのカテゴリ

-   モバイル ブロード バンドに固有の情報

-   モバイル ブロード バンド アプリ

-   モバイル ブロード バンド プロファイル

-   XML をプロビジョニングするための信頼された証明書

-   [DeviceNotificationHandler](devicenotificationhandler.md)要素

-   [PrivilegedApplications](privilegedapplications.md)要素

Windows 8、Windows 8.1、および Windows 10 のユーザー エクスペリエンスの側面をカスタマイズし、通信事業者アプリとして以前のモバイル ブロード バンドのアプリとの統合を提供する、メタデータ内の情報が使用されます。

サービス メタデータ パッケージは、.devicemetadata ms ファイル内で格納されている複数の XML ドキュメントで構成されます。 各ドキュメントには、サービスの属性のさまざまなコンポーネントを指定します。 これらの XML ドキュメントでは、ユーザーとネットワークの構成情報を表示のカスタマイズ内容を持つ Windows 接続マネージャーを提供します。

サービス メタデータ パッケージの XML ドキュメントのリファレンスについては、次を参照してください。[サービス メタデータ パッケージ スキーマ リファレンス](service-metadata-package-schema-reference.md)します。

## <a name="span-idservmdconspanspan-idservmdconspanservice-metadata-contents"></a><span id="servmdcon"></span><span id="SERVMDCON"></span>サービス メタデータの内容


次の概要に含まれているされ、サービス メタデータ パッケージ内で定義されている最も関心のあるフィールドの一部について説明します。

- **ハードウェア Id**  
  GSM ネットワークについては、一致するように、サービス メタデータ パッケージを対象の IMSI または ICCID の範囲を記述するメタデータ パッケージを送信できます。 MVNO 場合は、IMSIs または、MNO からリースが SIM ICC の Id の 1 つまたは複数の範囲を指定できます。 CDMA ネットワークについては、プロバイダーの ID (SID/NID) またはプロバイダー名を使用してパッケージを送信できます。 ハードウェア Id に対応しています、 [HardwareID](hardwareid.md)サービス メタデータ パッケージのスキーマ内の要素。 MNO や MVNO シナリオ、ハードウェアの Id (HWID) 範囲を計画する方法の詳細については、次を参照してください[MVNOs のエクスペリエンスを提供します。](delivering-experiences-for-mvnos.md)

- **サービス番号**  
  モバイル ブロード バンド サービス プロバイダーの一意の ID。 この GUID は、アカウントのプロビジョニングのメタデータを使用する場合、演算子を識別するためにも使用されます。 デバイス メタデータ パッケージを更新する場合、この GUID は、同じままする必要があります。 サービスの数を対応する、 [ServiceNumber](servicenumber.md)サービス メタデータ パッケージのスキーマ内の要素。

- **演算子のロゴ**   
  カスタム ロゴをネットワーク エントリの横にあるは、Windows 接続マネージャーが表示されます。 (ロゴはローミング ネットワーク上のユーザーが表示されません)。演算子のロゴに対応する、 [ServiceIconFile](serviceiconfile.md)サービス メタデータ パッケージのスキーマ内の要素。 ロゴの要件の詳細については、次を参照してください。[サービス アイコン要件](https://msdn.microsoft.com/library/windows/hardware/dn236416)します。  
  > [!IMPORTANT]
  > Windows 10 バージョン 1709 以降では、このフィールドは COSA を通じてブランドで置き換えられました。 ブランド化の COSA 内のフィールドが説明されている[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。 Windows 10 バージョン 1709 では、前に Windows のバージョンを対象としている場合、このセクションで説明したようにメタデータ パッケージを作成も。 COSA の詳細については、次を参照してください。 [COSA 概要](cosa-overview.md)します。 

- **モバイル ブロード バンド アプリ**  
  自動的にダウンロードされ、コンピューターに適用する UWP デバイス アプリ。 このアプリは、プランを購入、データの使用状況、およびヘルプとサポートなどのキーのエクスペリエンスを提供し、付加価値サービスを強調表示できます。

- **MB 購入プロファイル**  
  サブスクリプションをご購入の限定された接続を確立するために使用されるプロファイルを購入します。

  すべてのサブスクライバーに対して 1 つだけ購入 APN を持つ GSM 演算子の場合は、コンピューターをプロビジョニングするサービス メタデータを使用できます。 複数の購入 APNs がある場合は、アカウント プロビジョニングのメタデータを使用して、適切な購入 APN を設定する必要があります。 または、何も行うことができ、APN 接続情報を提供する、APN データベースに格納されているエントリを使用します。

- **MB インターネット プロファイル**  
  すべてのモバイル ブロード バンド サブスクリプションでは、ホーム ネットワーク オペレーターへの接続に使用される 1 つの既定のプロファイルを持つことができます。 Windows 接続マネージャーは、ネットワークに自動接続するため、このプロファイルを使用します。

  すべてのサブスクライバーに対して 1 つだけのインターネット APN を持つ GSM 演算子の場合は、コンピューターをプロビジョニングするサービス メタデータを使用できます。 複数のインターネット APNs の場合は、アカウント プロビジョニングのメタデータを使用して、適切なインターネット APN を設定する必要があります。 または、何も行うことができ、APN 接続情報を提供する、APN データベースに格納されているエントリを使用します。

- **証明書データ**  
  証明書のプロビジョニングに使用される情報。 これには、証明書の発行者名とサブジェクト名が含まれます。 この情報は、信頼されたオペレーターによって、web サイトによって開始されるアカウントのプロビジョニング操作が発行されることを確認するに使用されます。

- **カスタム演算子名**  
  通常、モバイル ブロード バンド デバイスは、Windows では、Windows 接続マネージャーを表示するオペレーター名を提供します。 この名前は、メタデータにカスタム名を指定することによってオーバーライドできます。 この名前は、ユーザーがホーム ネットワーク上にあり、ローミングのネットワーク上にない場合にのみ表示されます。 表示されているローミング ネットワーク名は、デバイスから受信する情報に基づきます。 これに対応して、 [ServiceProvider](serviceprovider.md)サービス パッケージのメタデータ スキーマ内の要素。  
  > [!IMPORTANT]
  > Windows 10 バージョン 1709 以降では、このフィールドは COSA を通じてブランドで置き換えられました。 ブランド化の COSA 内のフィールドが説明されている[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。 Windows 10、バージョン 1709 より前に、の Windows のバージョンを対象としている場合でも、このセクションで説明したメタデータ パッケージを作成します。 COSA の詳細については、次を参照してください。 [COSA 概要](cosa-overview.md)します。 

- **デバイスの通知ハンドラー**  
  一般に、アプリが、ユーザーが作業項目をシステム イベント ブローカーに登録できる前に少なくとも 1 回実行してください。 ただし、モバイル ブロード バンド アプリは、ユーザーがアプリを実行する前に、重要なイベントを受信する必要があります。 指定することができます、 [DeviceNotificationHandler](devicenotificationhandler.md)いくつかの重要なイベントを登録する Windows を使用してサービス メタデータ内の要素。 SMS 通知の詳細については、次を参照してください。 [MVNOs のエクスペリエンスを提供する](delivering-experiences-for-mvnos.md)します。

- **モバイル ブロード バンドの制限されたインターフェイスへのアクセス権限を持つアプリの一覧**  
  モバイル ブロード バンド Api とインターフェイス (アカウントのプロビジョニングと SMS を含む) は、モバイル ブロード バンド アプリのみに制限と使用可能なです。 内のサービス メタデータ パッケージでこれらの特権を持つ Api へのアクセス権を持つ特権のあるアプリの一覧を指定できます、 [PrivilegedApplications](privilegedapplications.md)要素。 特権のあるアプリをデバッグまたはアプリをテストすることができます。Microsoft Store 経由で配布するのには必須ではありません。

## <a name="span-idservicemetadatapackagestructurespanspan-idservicemetadatapackagestructurespanspan-idservicemetadatapackagestructurespanservice-metadata-package-structure"></a><span id="Service_Metadata_Package_Structure"></span><span id="service_metadata_package_structure"></span><span id="SERVICE_METADATA_PACKAGE_STRUCTURE"></span>サービス メタデータ パッケージの構造


サービス メタデータ パッケージのコンポーネントは、圧縮されたキャビネット ファイルに格納されのファイル拡張子が必要 **.devicemetadata ms**します。 サービス メタデータ パッケージは、デバイス メタデータ パッケージと同じ基になるプラットフォームを使用するために、このファイルの拡張機能を使用します。 作成する前に、 **.devicemetadata ms**ファイル メタデータ パッケージのグローバル一意識別子 (GUID) 最初に作成する必要があります。 次に、.devicemetadata ms ファイルを作成するときは、次の名前付け規則を使用する必要があります。**&lt;GUID&gt;.devicemetadata ms**します。

**注**  が、通常のファイル キャビネット ファイルの拡張子は **.cab**、サービス メタデータ パッケージ ファイルのファイル拡張子である必要があります **.devicemetadata ms**します。 これは、エンドユーザーの圧縮解除またはこれらのパッケージを変更する必要がありますいないという事実を強調するものです。

 

サービス メタデータ パッケージの 2 種類があります。 1 つのロケールのサービス メタデータ パッケージと複数のロケール サービス メタデータ パッケージ。

### <a name="span-idsinglelocaleservicemetadatapackagespanspan-idsinglelocaleservicemetadatapackagespanspan-idsinglelocaleservicemetadatapackagespansingle-locale-service-metadata-package"></a><span id="Single_Locale_Service_Metadata_Package"></span><span id="single_locale_service_metadata_package"></span><span id="SINGLE_LOCALE_SERVICE_METADATA_PACKAGE"></span>サービス メタデータ パッケージの 1 つのロケール

サービス メタデータ パッケージのローカライズ可能なリソースは、Windows 接続マネージャーとその横に表示されるサービスのアイコンに表示される演算子名です。 自分の名前をローカライズまたは PC からロケール情報に基づいて、アイコンを変更する必要がない場合は、1 つのロケールのサービス メタデータ パッケージを作成します。 ユーザーが自分の PC でを使用してどのようなロケールに関係なくオペレーター名を入手してサービスの 1 つのロケールのサービス メタデータ パッケージで定義されているアイコンは。

1 つのロケールのサービス メタデータ パッケージは、次のファイル構造が必要です。

![1 つのロケールのサービス メタデータ パッケージの構造](images/mb-xmlref-singlelocalesmp.jpg)

1 つのロケールのメタデータ パッケージに関する考慮事項がいくつか:

-   アイコン ファイルには、任意のファイル名を持つことができます。 ただし、個々 の XML ドキュメントを名前必要があります**PackageInfo.xml**、 **ServiceInfo.xml**、 **WindowsInfo.xml**、および**SoftwareInfo.xml**.

-   名前、 **MobileBroadbandInfo.xml**でファイルが定義されている、 **ServiceInfo.xml**します。 そのファイルは、このドキュメントに表示される名前を使用する必要があります。

-   **.Devicemetadata ms**ファイルを含めることはできません"{"または"}"の名前。 各メタデータ パッケージのファイル名の GUID は一意である必要があります。 新規または改訂後のサービス メタデータ パッケージを作成するときに、変更はマイナー場合でもは新しい GUID を作成する必要があります。

-   Windows のファイル拡張子を持つサービス メタデータ パッケージを認識する **.devicemetadata ms**します。

### <a name="span-idmultiplelocaleservicemetadatapackagestructurespanspan-idmultiplelocaleservicemetadatapackagestructurespanspan-idmultiplelocaleservicemetadatapackagestructurespanmultiple-locale-service-metadata-package-structure"></a><span id="Multiple_Locale_Service_Metadata_Package_Structure"></span><span id="multiple_locale_service_metadata_package_structure"></span><span id="MULTIPLE_LOCALE_SERVICE_METADATA_PACKAGE_STRUCTURE"></span>複数のロケール サービス メタデータ パッケージの構造

サービス メタデータ パッケージは、1 つのパッケージで複数のロケール ファイルをサポートします。 サービスの 1 つ以上のロケールをサポートする場合は、1 つのサービス メタデータ パッケージに複数のロケール ファイルを配置できます。

名を表示するローカライズされたサービスの Windows 接続マネージャーでネットワークの一覧またはネットワークの Windows 接続マネージャーで別のロゴを表示したい場合は、複数のローカル サービス メタデータ パッケージを使用できます。 Windows、ローカライズされたネットワーク名と Windows セットアップ中に構成が通常推奨システムの言語に基づいてロゴが表示されます。 現在のユーザーの言語が、推奨システムの言語と異なる場合でも、アイコンとネットワーク名常に表示されます、推奨システムの言語で。 サービス メタデータ パッケージに、ロケールが含まれていない場合は、サービス メタデータ パッケージのルートから言語中立的な説明が表示されます。 ほとんどのユーザー、言語は、推奨システムの言語を一致します。

複数のロケール サービス メタデータ パッケージは、次のファイル構造が必要です。

![複数のロケールのサービス メタデータ パッケージ構造](images/mb-xmlref-multiplelocalesmp.jpg)

複数のロケール メタデータ パッケージに関する考慮事項がいくつか:

-   各フォルダーでロケール名のフォルダーを作成し、ロケール名のフォルダーに XML ファイルまたは関連するファイルを配置します。

-   まだが必要、最上位の XML ファイルと関連するファイルは、各フォルダーの最上位レベルで、アイコン ファイルなどです。 これにより、サービス メタデータ パッケージのロケールが含まれていない場合、フォールバック メカニズムを提供します。

-   必要なすべてのファイルとそれらのファイル内のフィールドが完全に入力された各ロケール固有フォルダーで作成することを確認します。 これは各フォルダーの最上位レベルのコンテンツです。 たとえば、 [ServiceNumber](servicenumber.md) ServiceInfo.xml 内の要素を記入し、最上位のフォルダーとを作成するすべてのロケール固有のフォルダーを複製する必要があります。 これに失敗すると、エラーが発生します。

-   SoftwareInformation XML ドキュメントは、ロケールごとに異なる SoftwareInfo.xml ファイルを指定することはできませんので、複数のロケールをサポートしません。

## <a name="span-idmsdsubspanspan-idmsdsubspanservice-metadata-submission-and-maintenance"></a><span id="msdsub"></span><span id="MSDSUB"></span>サービス メタデータの送信とメンテナンス


詳細については、Windows デベロッパー センター ダッシュ ボードに – ハードウェア、サービス メタデータ パッケージを送信する方法についてを参照してください。[サービス メタデータを作成するための開発者ガイド](developer-guide-for-creating-service-metadata.md)します。

パッケージの記述方法の観点から最新の状態とする IMSI と ICCID または CDMA プロバイダーの名前または SID の値に一致するメタデータを保持する重要です。 これは、Sim と MNO または MVNO これらいる Iccid または IMSIs を提供されている先の新しい注文を追跡するために、SIM またはデバイスの取得の一部である新しいワークフローを実装するには、MNO または MVNO に必要です。

頻繁に作成を回避するベスト プラクティスおよび変更点、サービス メタデータ ICCID または IMSI 範囲 (または CDMA SIM/プロバイダー名) を予約して、MNO MVNO、事前にようにする場合は新しい Sim (または CDMA デバイス) は、調達、既にを占めている、サービス メタデータ パッケージ。

参照してください、Windows デベロッパー センター ハードウェア ダッシュ ボードに登録されているサービス id を更新する必要がある場合[サービス識別子所有権更新](service-identifier-ownership-updates.md)します。

メタデータの更新は自動的に適用されるに基づいて内部 Windows のロジック (8 日に一般) 更新プログラムのメタデータを更新するいずれかがあるかどうかに、Windows が WMIS をクエリした場合。

アプリを設計すると、メタデータが参照する、システムに最新のメタデータが適用されるまでの以前のバージョンで対処する必要があります。

[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)など、デバイスが見つからないか、認識されない場合のアドレス一般的なエラー ケースに発生するユーザーを設計する方法についてのガイドラインを提供します。

 

 






---
title: Web サイトを使用した Windows のプロビジョニング
description: Web サイトを使用した Windows のプロビジョニング
ms.assetid: ba60fddd-a248-4afb-9390-f9277ef1f094
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43e96b241107438e23351ae83d379711efd49f30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383652"
---
# <a name="provisioning-windows-using-a-website"></a>Web サイトを使用した Windows のプロビジョニング


このトピックでは、web サイトを使用して、顧客が購入し、Windows 8、Windows 8.1、または Windows 10 を実行しているコンピューター上のモバイル ブロード バンド プランを設定できるようにする方法について説明します。

Windows 8、Windows 8.1、および Windows 10 におけるモバイル ブロード バンドの詳細については、次を参照してください。[モバイル ブロード バンドの概要](overview-of-mobile-broadband.md)します。

開発し、モバイル ブロード バンドのアプリを使用して、最大限の柔軟性を提供し、最も統合エクスペリエンスを作成することをお勧めします。 ただし、いくつかのプランで購入し、セットアップ シナリオでは、モバイル ブロード バンド アプリが必ずしもインストールして使用するために使用できます。 これらのシナリオでは、Windows 8、Windows 8.1、および Windows 10 には、自分でホストされ、これらのシナリオを完了するために必要なエクスペリエンスを提供します。 モバイル ブロード バンド web サイトを自動的に開くサポートが含まれます。

## <a name="span-idkeyscenspanspan-idkeyscenspankey-scenarios-that-require-a-mobile-broadband-web-site"></a><span id="keyscen"></span><span id="KEYSCEN"></span>モバイル ブロード バンドの web サイトを必要とする主なシナリオ


次のシナリオでは、モバイル ブロード バンドの web サイトが必要です。

-   [USB モデムの最初の使用](#firstusb)

-   [埋め込みのモデムと共に SIM の最初の使用](#firstsimusb)

-   [アプリがアンインストールされたときに、更新を計画します。](#renewunin)

### <a name="span-idfirstusbspanspan-idfirstusbspanfirst-use-of-a-usb-modem"></a><span id="firstusb"></span><span id="FIRSTUSB"></span>USB モデムの最初の使用

ユーザーは、Windows 8、Windows 8.1、または Windows 10 の認定を受けたモバイル ブロード バンド USB モデム、関連付けられているデータをアクティブなプランがないから始まります。 ユーザーは、最初に、Windows 8、Windows 8.1、または Windows 10 コンピューターに USB モデムを接続し、デバイスのモバイル ブロード バンド クラス ドライバーが自動的にインストールします。 ユーザーは、Windows 接続マネージャーを開き、モバイル ブロード バンド ネットワークに接続することを選択します。

接続プロセスの一環として、Windows は、モバイル ブロード バンド ネットワークが提供しないことのインターネット アクセス、デバイスに関連付けられたアクティブなデータ プランがないためにを決定します。 通常、Windows のアプリがデータ プランを購入するか、それ以外の場合インターネットへのアクセスを有効にするオプションを提供できるようにモバイル ブロード バンド アプリが開きます。 ただし、USB モデムをインストールしたため、モバイル ブロード バンド アプリがまだインストールされていないコンピューターにします。

この場合は、Windows では、自分で指定した web サイトが開きます。 この web サイトでは、データ プランを購入するか、それ以外の場合インターネットへのアクセスを有効にする機能を提供します。 操作が完了したら、データ プランは、USB モデムに関連付けと、コンピューター、モバイル ブロード バンド ネットワーク上のインターネット アクセスが許可します。

### <a name="span-idfirstsimusbspanspan-idfirstsimusbspanfirst-use-of-a-sim-with-an-embedded-modem"></a><span id="firstsimusb"></span><span id="FIRSTSIMUSB"></span>埋め込みのモデムと SIM の最初の使用

ユーザーは、関連付けられているデータをアクティブなプランがない SIM から始まります。 ユーザーは、埋め込みのモバイル ブロード バンド モデムがある Windows 8、Windows 8.1、または Windows 10 コンピューターに、SIM を挿入します。 ユーザーは、Windows 接続マネージャーを開き、モバイル ブロード バンド ネットワークに接続することを選択します。

接続プロセスの一環として、Windows は、モバイル ブロード バンド ネットワークが提供しないことのインターネット アクセスを SIM で関連付けられているアクティブなデータ プランがないためにを決定します。 通常、Windows のアプリがデータ プランを購入するか、それ以外の場合インターネットへのアクセスを有効にするオプションを提供できるようにモバイル ブロード バンド アプリが開きます。 ただし、SIM が挿入したため、モバイル ブロード バンド アプリがまだインストールされていないコンピューターにします。

この場合は、Windows では、自分で指定した web サイトが開きます。 この web サイトでは、データ プランを購入するか、それ以外の場合インターネットへのアクセスを有効にする機能を提供します。 操作が完了したら、データ プランは、SIM に関連付けし、コンピューター、モバイル ブロード バンド ネットワーク上のインターネット アクセスが許可します。

### <a name="span-idrenewuninspanspan-idrenewuninspanplan-renewal-when-the-app-has-been-uninstalled"></a><span id="renewunin"></span><span id="RENEWUNIN"></span>アプリがアンインストールされたときに、更新を計画します。

ユーザーが定期的に使用されたモバイル ブロード バンド Windows 8、Windows 8.1、または Windows 10 コンピューターにします。 いくつかの時点では、ユーザーがモバイル ブロード バンドのアプリをアンインストールおよびため、有効期限の日付またはデータの使用状況データ プランの有効期限が切れました。 ユーザーは、Windows 接続マネージャーを開き、モバイル ブロード バンド ネットワークに接続することを選択します。

接続プロセスの一環として、Windows は、モバイル ブロード バンド ネットワークが提供しないことのインターネット アクセス、プランをアクティブなデータがデバイスに関連付けられているではなくなったためにを決定します。

Windows がインストールされていないアプリを開始できないため、Windows は、自分で提供される web サイトを開きます。 この web サイトには、ユーザーのデータ プランを更新またはインターネットへのアクセスを有効にするそれ以外の場合、エクスペリエンスを提供します。 操作が完了したら、データ プランは、ユーザーのデバイスに関連付けられてもう一度と、コンピューター、モバイル ブロード バンド ネットワーク上のインターネット アクセスが許可します。

## <a name="span-idhowtoenablekeyscenariosspanspan-idhowtoenablekeyscenariosspanspan-idhowtoenablekeyscenariosspanhow-to-enable-key-scenarios"></a><span id="How_to_enable_key_scenarios"></span><span id="how_to_enable_key_scenarios"></span><span id="HOW_TO_ENABLE_KEY_SCENARIOS"></span>主なシナリオを有効にする方法


次のガイドラインを使用して、これらの主要なシナリオを有効にできます。

### <a name="span-idenablesimpspanspan-idenablesimpspanenable-a-simple-connect-experience"></a><span id="enablesimp"></span><span id="ENABLESIMP"></span>単純な接続エクスペリエンスを有効にします。

最小限の Windows 8、Windows 8.1、または Windows 10 の APN データベースに含めるデータを提供する必要があります。 Windows APN データベースに関する詳細については、次を参照してください。 [APN データベースの概要](apn-database-overview.md)します。

APN データベースに含めるには、次の情報を提供する必要があります。

-   Windows APN またはアクセスの文字列を入力するように求めることがなく、モバイル ブロード バンド ネットワークに接続する、する必要があります、APNs の提供や文字列にアクセスします。

-   インターネット接続が検出されないときに、モバイル ブロード バンドの web サイトを自動的に開く Windows、web サイトの URL を指定する必要があります。

### <a name="span-iddetectspanspan-iddetectspandetect-internet-access"></a><span id="detect"></span><span id="DETECT"></span>インターネットへのアクセスを検出します。

Windows は、まずインターネット接続の決定にネットワークに接続するときに、さまざまなネットワーク テストを実行します。 これらのテストの接続先サイトでは、接続をテストするためだけに使用される予約済みのドメインである、msftncsi.com が。

偽陽性や偽陰性を避けるため、ユーザーが通常のインターネット アクセスがある場合のみ、ネットワークが www.msftncsi.com へのアクセスを許可する必要があります。 しなくても、プランをアクティブなデータをネットワークに接続しているユーザーは www.msftncsi.com へのアクセスに必要ありません。

### <a name="span-idwebaccessspanspan-idwebaccessspanweb-site-access"></a><span id="webaccess"></span><span id="WEBACCESS"></span>Web サイトへのアクセス

通常、通信事業者には、アクティブなデータが 2 つのメソッドのいずれかを使用して計画を持たないユーザーのネットワーク アクセスが制限されます。

-   プランを購入してアクティブ化に必要なサーバーの最小限のセットを除くすべてのネットワーク送信先へのアクセスをブロックが、同じ APN にユーザーを保持します。 この実装は「高いガーデン」とも呼ばれます

-   インターネットにアクセスすることはありません APN の購入にユーザーの移行には、プランを購入してアクティブ化に必要なサーバーのセットへのアクセスが提供します。

アクティブなデータ プランを持っていないユーザーは、これらのメソッドのいずれかを使用して、モバイル ブロード バンドの web サイトにアクセスできる必要があります。 さらに、ユーザーは、インターネット経由の HTTPS 接続を使用して web サイトにアクセスできる必要があります。

### <a name="span-iddevinfspanspan-iddevinfspandevice-information"></a><span id="devinf"></span><span id="DEVINF"></span>デバイス情報

Windows が携帯電話会社の URL を使用する場合 (AccountExperienceURL 属性、[演算子](operator.md)要素) Windows APN データベースからモバイル ブロード バンドをライセンス認証を完了するために必要なデバイス情報を提供しますweb サイトです。 このデバイス情報は、web サイトに HTTPS 要求のパラメーターとして渡されます。

URL の形式が **https://Operator URL\[でしょうか。 propN = valN\[& propN = valN\]\*\]** ここで。

-   **演算子 URL** URL によって提供され、APN データベースに格納されています。

-   **propN**プロパティ名。

-   **valN**プロパティ名に対応する値。

次の表には、含めることができるプロパティが一覧表示します。 プロパティの値を指定しない場合は、モバイル ブロード バンド デバイスによって、そのプロパティは含まれません。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>プロパティ名</th>
<th>［プロパティ値］</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SubId</p></td>
<td><p>サブスクライバー ID</p>
<ul>
<li><p>GSM デバイス。IMSI (最大 15 桁)</p></li>
<li><p>CDMA デバイス。最小値または MIN(IRM) (10 桁)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DevId</p></td>
<td><p>デバイス ID</p>
<ul>
<li><p>GSM デバイス。IMEI (最大 15 桁)</p></li>
<li><p>CDMA デバイス。ESN (11 桁の数字) または MEID (17 桁)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IccId</p></td>
<td><p>SIM ICCID (19 ~ 20 桁)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idconfigurethecomputerspanspan-idconfigurethecomputerspanspan-idconfigurethecomputerspanconfigure-the-computer"></a><span id="Configure_the_computer"></span><span id="configure_the_computer"></span><span id="CONFIGURE_THE_COMPUTER"></span>コンピューターを構成します。

ユーザーがデータ プランを購入したか、それ以外の場合、web サイトを使用して、モバイル ブロード バンド デバイスをアクティブ化が後、は、コンピューターに次の構成の変更を加えると便利な場合があります。

-   モバイル ブロード バンド接続プロファイルを定義します。

-   アカウント データを提供します。

-   Wi-fi ホット スポットの接続プロファイルを定義します。

-   モバイル ブロード バンド デバイスを再接続するコンピューターに指示します。

モバイル ブロード バンドのアプリを使用してコンピューターに適用できるメタデータをプロビジョニングするのと同じアカウントは、モバイル ブロード バンドの web サイトにも適用できます。 Web ページの JavaScript での可用性の確認、 [ **window.external.msProvisionNetworks** ](https://msdn.microsoft.com/library/dn529170)メソッド。 存在する場合、ブラウザーは、アカウントをプロビジョニングする Windows メタデータを転送できます。

アカウント プロビジョニングのメタデータに関する詳細については、次を参照してください。[アカウント プロビジョニング](account-provisioning.md)します。

**注**  アカウント プロビジョニングのメタデータは、web サイトによって提供されるときに、拡張された検証 (EV) 証明書で署名する必要があります。

 

 

 






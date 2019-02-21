---
title: モバイル ブロード バンドの Windows ランタイム Api の一覧
description: モバイル ブロード バンドの Windows ランタイム Api の一覧
ms.assetid: 45ec97c4-1a58-48a8-ad50-1cd8fcc4763f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 561d6c1eabda02ac372a62d083f855c7100ccdab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560096"
---
# <a name="list-of-mobile-broadband-windows-runtime-apis"></a>モバイル ブロード バンドの Windows ランタイム Api の一覧


次の表では、モバイル ブロード バンドのアプリを作成するための Api を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>API</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="connection-profile-api.md" data-raw-source="[Connection Profile API](connection-profile-api.md)">接続プロファイル API</a></p></td>
<td><p>(たとえば、インターネット) に接続状態に関する情報を提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="device-services-extension-api.md" data-raw-source="[Device Services Extension API](device-services-extension-api.md)">デバイス サービス拡張機能 API</a></p></td>
<td><p>SIM Toolkit と優先ローミング リスト (PRL) のダウンロードなどのデバイスに固有の拡張機能を有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="provisioning-api.md" data-raw-source="[Provisioning API](provisioning-api.md)">プロビジョニング API</a></p></td>
<td><p>プロビジョニング Windows アカウントのプロビジョニング データとデータの使用状況情報を使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="sim-pin-api.md" data-raw-source="[SIM PIN API](sim-pin-api.md)">SIM の暗証番号 (PIN) API</a></p></td>
<td><p>使用すると、有効化、無効にする、または SIM PIN を変更できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="sms-api.md" data-raw-source="[SMS API](sms-api.md)">SMS API</a></p></td>
<td><p>SMS クライアントを実装するために必要な機能を提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="subscriber-and-device-information-api.md" data-raw-source="[Subscriber and Device Information API](subscriber-and-device-information-api.md)">サブスクライバーとデバイスの情報の API</a></p></td>
<td><p>モバイル ブロード バンド デバイスに SIM とデバイスについては、サブスクライバー情報を提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="ussd-api.md" data-raw-source="[USSD API](ussd-api.md)">USSD API</a></p></td>
<td><p>(クライアントとネットワークが開始した) のネットワークと非構造化補助サービス データ (USSD) セッションを確立できます。</p></td>
</tr>
</tbody>
</table>

 

次のセクションでは、このトピックで使用できるとおりです。

-   [モバイル ブロード バンド アカウント API](#mbacctapi)

-   [アカウントのネットワーク Id](#netid)

## <a name="span-idmbacctapispanspan-idmbacctapispanmobile-broadband-account-api"></a><span id="mbacctapi"></span><span id="MBACCTAPI"></span>モバイル ブロード バンド アカウント API


お客様の個人を特定できる情報を取得し、モバイル ブロード バンド デバイス上のネットワーク設定の変更に使用できるメソッドがあるため、モバイル ブロード バンド アカウントの API は特権を持つ API になります。 つまり、ほとんどの UWP アプリが「アクセス拒否」エラーが発生せず、メソッドを呼び出すことはできません。 この API を呼び出すには、UWP アプリは、次の条件を満たす必要があります。

-   アプリがそれに関連付けられているデバイスのメタデータまたはサービス メタデータ パッケージを必要し、に指定する必要があります、 [PrivilegedApplications](privilegedapplications.md) SoftwareInfo.xml ファイル、パッケージ内の XML 要素。 パッケージをアプリケーションに限定する必要はありません。いくつかのパッケージの PrivilegedApplications 要素で一覧表示する、特定の UWP アプリのことができます。 インストールされているように、そのパッケージがアクティブになったを少なくとも 1 回、コンピューター、モバイル ブロード バンド デバイスのサービス プロバイダーを関連付ける必要があります。

-   アプリケーションの appxmanifest ファイルが必要な**&lt;DeviceCapability&gt;** モバイル ブロード バンド アカウント API のエントリ。 子として次の XML 要素を追加することでこれを行う、 **&lt;機能&gt;** アプリケーションの appxmanifest ファイル内の要素。

    ``` syntax
    <DeviceCapability Name="BFCD56F7-3943-457F-A312-2E19BB6DC648" />
    ```

    詳細については、 **&lt;機能&gt;** 要素を参照してください[Windows 8 用のマニフェスト ファイルをアプリ](https://msdn.microsoft.com/library/windows/apps/ff769509.aspx)します。

**注**  モバイル ブロード バンド アカウント API に無制限のアクセスに (たとえば、Microsoft Win32 サービスまたはデスクトップ アプリ) の UWP アプリではないアプリケーションをします。 これらのアプリケーションはモバイル ブロード バンド ネットワークへのフル アクセスを取得する既存の Win32 およびコンポーネント オブジェクト モデル (COM) Api を使用できるためです。 UWP アプリからこれらの Api を使用することはできません。

 

## <a name="span-idnetidspanspan-idnetidspannetwork-account-ids"></a><span id="netid"></span><span id="NETID"></span>アカウントのネットワーク Id


ネットワークのアカウント ID は、モバイル ブロード バンド アカウントの一意の識別子です。 ID に由来 GSM、CDMA、または WiMAX ネットワークかどうかを把握することがなく使用できる統合された ID を提供します。 Windows では、前にこれが発生していないハードウェアで提供されるネットワークのサブスクリプション識別子を検出するたびに、ネットワーク アカウント Id が生成されます。 次の一覧は、サポートされているネットワークの種類ごとのネットワーク アカウント ID を識別します。

-   GSM ネットワーク:SIM の ICCID は、サブスクリプション間で区別するために使用されます。

-   CDMA ネットワーク:モバイルの識別番号 (分) が使用されます。

Windows は、最初に上記のネットワークの種類のいずれかのように検出すると、新しいネットワーク アカウント ID を作成し、ハードウェアで提供されるサブスクリプションの識別子の sha-256 ハッシュにマップし、これらの両方がレジストリに格納します。 逆に、Windows には、レジストリ内のハードウェアで提供されるサブスクリプション id のハッシュが検出されると、そのハッシュに関連付けられているネットワーク アカウント ID を使用します。 ネットワーク アカウント Id は、グローバルに一意でなければなりません (それらに基づく Guid)、ハードウェアで提供される識別子のハッシュには格納されているものであるため ICCID または最小値が生成されたことに、ネットワーク アカウント ID をマップしようとするときに存在するネットワーク ハードウェアをある必要がありますが、差出人。

**重要な**  ネットワーク アカウントの ID から、ICCID を取得するには、コンピューターとそれらをまとめてマップに使用されるネットワーク デバイスへのアクセスが必要とする場合でもネットワーク アカウント Id は個々 のユーザーを一意に識別します。 そのため、それらに作業する場合は、個人を特定できる情報に対処するため、組織のポリシーに従うことをお勧めします。

 

エンドユーザーは、プロバイダー 1 と Provider2 の両方のモバイル ブロード バンド デバイスが対応するモバイル ブロード バンド アプリがインストールされている場合は、プロバイダー 1 アプリことはできません、Provider2 を使用するように、モバイル ネットワーク オペレーター (MNO) によってネットワーク アカウント Id が分離されました。ネットワーク アカウント Id、またはその逆です。 すべてのネットワーク アカウント Id は、ネットワーク アカウントの Id のみを返します、MNO アプリケーションを返す関数では、関数を呼び出します。 異なる MNO に属するネットワーク アカウント ID を使用した場合は、「アクセスが拒否されました」エラーになります。

**注**   (たとえば、Win32 サービスまたはデスクトップ アプリ) の UWP アプリではないアプリがネットワーク サービス プロバイダーに関係なくすべてのネットワーク アカウントへのアクセスがあります。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンド WinRT API の概要](mobile-broadband-winrt-api-overview.md)

 

 







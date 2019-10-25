---
title: デバイス オブジェクトを表す SDDL
description: デバイス オブジェクトを表す SDDL
ms.assetid: c0e4432a-4429-4ecd-a2e5-f93a9e3caf48
keywords:
- デバイスオブジェクト WDK カーネル、セキュリティ
- セキュリティ WDK デバイスオブジェクト
- セキュリティ記述子定義言語 WDK デバイスオブジェクト
- SDDL WDK デバイスオブジェクト
- Iocreateデバイス
- セキュリティ記述子 WDK デバイスオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4a77cf0fb17fbbc5a8171ea050b034ba757fe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836391"
---
# <a name="sddl-for-device-objects"></a>デバイス オブジェクトを表す SDDL





セキュリティ記述子定義言語 (SDDL) は、セキュリティ記述子を表すために使用されます。 デバイスオブジェクトのセキュリティは、 [INF ファイルに配置](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)されるか、または[**iocreateデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)に渡される SDDL 文字列によって指定できます。 [セキュリティ記述子定義言語](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

INF ファイルでは SDDL の全範囲がサポートされていますが、 **Iocreateデバイス**のルーチンでは、言語のサブセットのみがサポートされています。 このサブセットはここで定義されています。

デバイスオブジェクトの SDDL 文字列の形式は "d P" で、その後に1つ以上の形式の式が続きます。 "(A;;*アクセス*;;;*SID*) "。 *SID*値は、*アクセス*値を適用する対象 (ユーザーやグループなど) を決定するセキュリティ識別子を指定します。 *アクセス*値は、SID に許可されているアクセス権を指定します。 *アクセス*と*SID*の値は次のとおりです。

**注**  デバイスオブジェクトに対して SDDL を使用する場合、ドライバーは Wdmsec .lib にリンクする必要があります。

 

<a href="" id="access"></a>*Access*  
許可されるアクセスを決定する[**アクセス\_マスク**](access-mask.md)値を指定します。 この値は、"0x*hex*" 形式の16進値として、またはアクセス権を表す2文字のシンボリックコードのシーケンスとして書き込むことができます。

次のコードを使用して、汎用アクセス権を指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コード</th>
<th>汎用アクセス権</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GA</p></td>
<td><p>GENERIC_ALL</p></td>
</tr>
<tr class="even">
<td><p>GR</p></td>
<td><p>GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>GW</p></td>
<td><p>GENERIC_WRITE</p></td>
</tr>
<tr class="even">
<td><p>GX</p></td>
<td><p>GENERIC_EXECUTE</p></td>
</tr>
</tbody>
</table>

 

次のコードを使用して、特定のアクセス権を指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コード</th>
<th>特定のアクセス権</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リターン</p></td>
<td><p>READ_CONTROL</p></td>
</tr>
<tr class="even">
<td><p>SD</p></td>
<td><p>DELETE</p></td>
</tr>
<tr class="odd">
<td><p>WORD</p></td>
<td><p>WRITE_DAC</p></td>
</tr>
<tr class="even">
<td><p>フロー</p></td>
<td><p>WRITE_OWNER</p></td>
</tr>
</tbody>
</table>

 

汎用\_では、ACL を変更する機能など、上記の2つのテーブルに記載されているすべての権限が付与されることに注意してください。

<a href="" id="sid"></a>*SID*  
指定したアクセスを許可する SID を指定します。 Sid は、アカウント、エイリアス、グループ、ユーザー、またはコンピューターを表します。

次の Sid は、コンピューター上の*アカウント*を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SY</p></td>
<td><p>[システム]</p>
<p>ユーザーモードコンポーネントを含む、オペレーティングシステム自体を表します。</p></td>
</tr>
<tr class="even">
<td><p>AVL</p></td>
<td><p>Local Service</p>
<p>ローカルサービスの定義済みのアカウント (認証および世界にも属しています)。 この SID は、Windows XP 以降で使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>STATION</p></td>
<td><p>Network Service</p>
<p>ネットワークサービスの定義済みのアカウント (認証および世界にも属しています)。 この SID は、Windows XP 以降で使用できます。</p></td>
</tr>
</tbody>
</table>

 

次の Sid は、コンピューター上の*グループ*を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BA</p></td>
<td><p>管理者</p>
<p>コンピューター上の組み込みの Administrators グループ。</p></td>
</tr>
<tr class="even">
<td><p>BU</p></td>
<td><p>組み込みユーザーグループ</p>
<p>グループは、すべてのローカルユーザーアカウントとドメインのユーザーをカバーします。</p></td>
</tr>
<tr class="odd">
<td><p>BG</p></td>
<td><p>組み込みのゲストグループ</p>
<p>ローカルまたはドメインの guest アカウントを使用してログインするユーザーをグループ化します。</p></td>
</tr>
</tbody>
</table>

 

次の Sid は、ユーザーが認証された範囲を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AU</p></td>
<td><p>認証されたユーザー</p>
<p>ローカルコンピューターまたはドメインによって認識されたすべてのユーザー。 Builtin Guest アカウントを使用してログインしたユーザーは認証されないことに注意してください。 ただし、ゲストグループのメンバーは、コンピューターまたはドメインの個々のアカウントを使用して認証されます。</p></td>
</tr>
<tr class="even">
<td><p>込み</p></td>
<td><p>匿名ログオンユーザー</p>
<p>匿名ネットワークセッションなど、id なしでログオンしたユーザー。 Builtin Guest アカウントを使用してログインしているユーザーは、認証も匿名でもありません。 この SID は、Windows XP 以降で使用できます。</p></td>
</tr>
</tbody>
</table>

 

次の Sid は、ユーザーがコンピューターにログインする方法を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IU</p></td>
<td><p>対話型ユーザー</p>
<p>ローカルログオンやリモートデスクトップログオンなど、コンピューターに最初にログオンしたユーザー。</p></td>
</tr>
<tr class="even">
<td><p>ニュー</p></td>
<td><p>ネットワークログオンユーザー</p>
<p>対話型デスクトップアクセスを使用せずにリモートでコンピューターにアクセスするユーザー (ファイル共有や RPC 呼び出しなど)。</p></td>
</tr>
<tr class="odd">
<td><p>WORD</p></td>
<td><p>World</p>
<p>Windows XP より前では、この SID は、認証されたユーザー、匿名ユーザー、または Builtin Guest アカウントにかかわらず、すべてのセッションに適用されていました。</p>
<p>Windows XP 以降では、この SID は匿名ログオンセッションに対応していません。認証されたユーザーと Builtin Guest アカウントのみが対象となります。</p>
<p>信頼されていないコードまたは "制限された" コードは、世界の SID の対象ではないことに注意してください。 詳細については、次の表の制限されたコード (RC) SID の説明を参照してください。</p></td>
</tr>
</tbody>
</table>

 

次の Sid には特別な言及があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>SID</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>リターン</p></td>
<td><p>制限付きコード</p>
<p>この SID は、信頼されていないコードによるアクセスを制御するために使用されます。 RC を使用したトークンに対する ACL の検証は、2つのチェックで構成されています。1つはトークンの通常の Sid の一覧 (インスタンスの場合は WD)、もう1つは (通常は RC と元のトークンのサブセットを含む) 2 つのチェックで構成されます。 トークンが両方のテストに合格した場合にのみアクセスが許可されます。 そのため、RC は実際に他の Sid と組み合わせて動作します。</p>
<p>RC を指定する ACL では、WD も指定する必要があります。 ACL で RC と WD を組み合わせると、信頼されていないコードを含むすべてのユーザーのスーパーセットが記述されます。</p>
<p>信頼されていないコードは、エクスプローラーの [実行] オプションを使用してコードを起動することがあります。 既定では、世界は信頼されていないコードに対応していません。</p></td>
</tr>
<tr class="even">
<td><p>UD</p></td>
<td><p>ユーザーモードドライバー</p>
<p>この SID は、ユーザーモードドライバーへのアクセスを許可します。 現時点では、この SID は、ユーザーモードドライバーフレームワーク (UMDF) 用に記述されたドライバーのみを対象としています。 この SID は、Windows 8 以降で使用できます。</p>
<p>"UD" の省略形を認識しない以前のバージョンの Windows では、UMDF ドライバーへのアクセスを許可するには、この SID の完全修飾形式 (S-1-5-84-0-0-0-0-0) を指定する必要があります。 詳細については、「ユーザーモードドライバーフレームワークのドキュメント」の「<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access" data-raw-source="[Controlling Device Access](https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access)">デバイスアクセスの制御</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

### <a name="sddl-examples-for-device-objects"></a>デバイスオブジェクトの SDDL の例

このセクションでは、Wdmsec. h で見つかった定義済みの SDDL 文字列について説明します。 また、これらをテンプレートとして使用して、デバイスオブジェクトの新しい SDDL 文字列を定義することもできます。

SDDL\_DEVOBJ\_カーネル\_のみ

**"D-P"**

SDDL\_DEVOBJ\_カーネル\_のみが "空" の ACL です。 ユーザーモードコード (システムとして実行されているプロセスを含む) は、デバイスを開くことができません。

PnP バスドライバーは、PDO を作成するときにこの記述子を使用できます。 INF ファイルでは、デバイスに対して緩やかなセキュリティ設定を指定できます。 この記述子を指定することにより、バスドライバーは、INF が処理される前にデバイスを開こうとしても成功しないようにします。

同様に、WDM 以外のドライバーはこの記述子を使用して、適切なユーザーモードプログラム (インストーラーなど) がレジストリ内の最終的なセキュリティ記述子を設定するまで、デバイスオブジェクトにアクセスできないようにすることができます。

これらのすべての場合、既定値は厳格なセキュリティであり、必要に応じて緩和です。

SDDL\_DEVOBJ\_SYS\_すべて

**"D: P (A;;GA、;、SY) "**

SDDL\_DEVOBJ\_SYS\_ALL は SDDL\_DEVOBJ\_カーネル\_に似ていますが、カーネルモードコードだけでなく、システムとして実行されているユーザーモードコードでも、デバイスを開いて任意のアクセスを許可することができます。

レガシドライバーでは、この ACL を使用して、セキュリティ設定が厳重に開始される場合があります。また、 **SetFileSecurity**ユーザーモード関数を使用して、ユーザーが実行時にデバイスを起動できるようにします。 この場合、サービスはシステムとして実行されている必要があります。

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_すべて

**"D: P (A;;GA、;、SY) (A;;GA、;、BA) "**

SDDL\_DEVOBJ\_SYS\_すべての\_ADM\_を使用して、カーネル、システム、および管理者がデバイスを完全に制御できるようになります。 他のユーザーがデバイスにアクセスすることはできません。

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_RWX\_WORLD\_R

**"D: P (A;;GA、;、SY) (A;;GRGWGX;;;BA) (A;;GR;;;WD) "**

SDDL\_DEVOBJ\_SYS\_すべての\_ADM\_RWX\_WORLD\_R では、カーネルとシステムがデバイスを完全に制御できます。 既定では、管理者はデバイス全体にアクセスできますが、ACL を変更することはできません (管理者がデバイスを最初に制御する必要があります)。

すべてのユーザー (世界の SID) に読み取りアクセス権が付与されます。 信頼されていないコードはデバイスにアクセスできません (エクスプローラーで [実行] オプションを使用して信頼されていないコードが起動される可能性があります。 既定では、世界では制限されたコードに対応していません)。

また、走査アクセスは通常のユーザーに付与されないことにも注意してください。 そのため、名前空間を持つデバイスに適した記述子ではない可能性があります。

SDDL\_DEVOBJ\_SYS\_すべての\_ADM\_RWX\_WORLD\_R\_RES\_R

**"D: P (A;;GA、;、SY) (A;;GRGWGX;;;BA) (A;;GR;;;WD) (A;;GR;;;RC) "**

SDDL\_DEVOBJ\_SYS\_すべての\_ADM\_RWX\_WORLD\_R\_RES\_R を使用すると、カーネルとシステムがデバイスを完全に制御できます。 既定では、管理者はデバイス全体にアクセスできますが、ACL を変更することはできません (管理者がデバイスを最初に制御する必要があります)。

すべてのユーザー (世界の SID) に読み取りアクセス権が付与されます。 また、信頼されていないコードは、コードへのアクセスも許可されます。 信頼されていないコードは、エクスプローラーの [実行] オプションを使用してコードを起動することがあります。 既定では、世界は制限付きコードに対応していません。

また、走査アクセスは通常のユーザーに付与されないことにも注意してください。 そのため、名前空間を持つデバイスに適した記述子ではない可能性があります。

 

上記の SDDL 文字列に継承修飾子は含まれていないことに注意してください。 そのため、デバイスオブジェクトに対してのみ適切であり、ファイルまたはレジストリキーには使用しないでください。 SDDL を使用した継承の指定の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





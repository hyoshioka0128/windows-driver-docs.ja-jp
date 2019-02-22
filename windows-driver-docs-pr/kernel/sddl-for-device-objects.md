---
title: デバイス オブジェクトの SDDL
description: デバイス オブジェクトの SDDL
ms.assetid: c0e4432a-4429-4ecd-a2e5-f93a9e3caf48
keywords:
- デバイス オブジェクトの WDK カーネル、セキュリティ
- WDK デバイス オブジェクトのセキュリティ
- セキュリティ記述子定義言語の WDK デバイス オブジェクト
- SDDL の WDK デバイス オブジェクト
- IoCreateDeviceSecure
- WDK のデバイス オブジェクトのセキュリティ記述子
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7a0a85012f66c444b1850f207d93a265cb32eee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529975"
---
# <a name="sddl-for-device-objects"></a>デバイス オブジェクトの SDDL





セキュリティ記述子定義言語 (SDDL) は、セキュリティ記述子を表すために使用されます。 デバイス オブジェクトのセキュリティは、ある SDDL 文字列によって指定できます[が INF ファイルに配置](https://msdn.microsoft.com/library/windows/hardware/ff540212)に渡されるまたは[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)します。 [セキュリティ記述子定義言語](https://msdn.microsoft.com/library/windows/desktop/aa379567)Microsoft Windows SDK ドキュメントが充実します。

によって、言語のサブセットのみがサポートされている完全な範囲の SDDL をサポートして INF ファイル、 **IoCreateDeviceSecure**ルーチン。 このサブセットは、ここで定義されます。

SDDL 文字列の形式の"D:P"後では、フォームの 1 つまたは複数の式のデバイス オブジェクトの"(A;*アクセス*;;*SID*)"。 *SID*先を決定するセキュリティ識別子を指定する値、*アクセス*値 (例、ユーザーまたはグループ) に適用されます。 *アクセス*値が SID に対して許可されるアクセス権限を指定します。 *アクセス*と*SID*値は次のとおりです。

**注**  SDDL デバイス オブジェクトを使用する場合、ドライバーが Wdmsec.lib に対してリンクする必要があります。

 

<a href="" id="access"></a>*アクセス*  
指定します、 [**アクセス\_マスク**](access-mask.md)許可されたアクセスを決定する値。 この値で記述できる 16 進数の値として、フォーム"0 x*16 進*"、またはアクセス権を表すシンボリック コードの 2 文字のシーケンスとして。

汎用的なアクセス権を指定する、次のコードを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>コード</th>
<th>汎用的なアクセス権</th>
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

 

次のコードは、特定のアクセス権を指定できます。

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
<td><p>RC</p></td>
<td><p>READ_CONTROL</p></td>
</tr>
<tr class="even">
<td><p>SD</p></td>
<td><p>DELETE</p></td>
</tr>
<tr class="odd">
<td><p>WD</p></td>
<td><p>WRITE_DAC</p></td>
</tr>
<tr class="even">
<td><p>WO</p></td>
<td><p>WRITE_OWNER</p></td>
</tr>
</tbody>
</table>

 

注そのジェネリック\_すべて許可 ACL を変更する機能を含む 2 つのテーブル、上記のすべての権限が一覧表示します。

<a href="" id="sid"></a>*SID*  
指定したアクセスが許可された SID を指定します。 Sid は、アカウント、エイリアス、グループ、ユーザー、またはコンピューターを表します。

次の Sid 表す*アカウント*コンピューターにします。

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
<td><p>System</p>
<p>ユーザー モード コンポーネントを含む、オペレーティング システム自体を表します。</p></td>
</tr>
<tr class="even">
<td><p>%.*LS</p></td>
<td><p>Local Service</p>
<p>(これは認証され、世界に属するも) ローカル サービスの定義済みのアカウント。 この SID は、Windows XP 以降から使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>NS</p></td>
<td><p>Network Service</p>
<p>(これは認証され、世界に属している) ネットワーク サービスの定義済みのアカウント。 この SID は、Windows XP 以降から使用できます。</p></td>
</tr>
</tbody>
</table>

 

次の Sid 表す*グループ*コンピューターにします。

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
<p>コンピューターの組み込みの管理者グループ。</p></td>
</tr>
<tr class="even">
<td><p>BU</p></td>
<td><p>組み込みユーザー グループ</p>
<p>グループのすべてのローカル ユーザー アカウント、およびドメインのユーザーをカバーします。</p></td>
</tr>
<tr class="odd">
<td><p>BG</p></td>
<td><p>組み込みのゲストのグループ</p>
<p>グループはローカルまたはドメインのゲスト アカウントを使用してログインするユーザーをカバーします。</p></td>
</tr>
</tbody>
</table>

 

次の Sid には、ユーザーが認証されているエクステントがについて説明します。

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
<p>すべてのユーザーは、ローカル コンピューターまたはドメインを認識します。 組み込みのゲスト アカウントを使用してログオンしているユーザーが認証されていないことに注意してください。 ただし、コンピューターまたはドメインに個々 のアカウントと Guests グループのメンバーが認証されます。</p></td>
</tr>
<tr class="even">
<td><p>を</p></td>
<td><p>匿名ログオン ユーザー</p>
<p>すべてのユーザーは、匿名ネットワーク セッションなど、identity なしログに記録します。 組み込みのゲスト アカウントを使用してログオンしているユーザーは認証もでも匿名ことに注意してください。 この SID は、Windows XP 以降から使用できます。</p></td>
</tr>
</tbody>
</table>

 

次の Sid は、ユーザーが、コンピューターにログインする方法について説明します。

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
<p>最初に、マシンにログオンしているユーザー&quot;対話形式で&quot;、ローカルのログオンおよびリモート デスクトップ ログオンなど。</p></td>
</tr>
<tr class="even">
<td><p>NU</p></td>
<td><p>ネットワーク ログオン ユーザー</p>
<p>対話型デスクトップ アクセス (たとえば、ファイル共有または RPC 呼び出し) せず、コンピューターをリモートでアクセスするユーザー。</p></td>
</tr>
<tr class="odd">
<td><p>WD</p></td>
<td><p>World</p>
<p>この SID が認証されたかどうか、すべてのセッションをカバー Windows XP では、前にユーザー、匿名ユーザー、または組み込みのゲスト アカウント。</p>
<p>Windows XP 以降、この SID は匿名ログオン セッションについて説明しません。認証されたユーザーと、組み込みのゲスト アカウントのみを説明します。</p>
<p>信頼されていないので注意または&quot;制限&quot;コードも含まれていない世界の SID。 詳細については、次の表の説明、制限付きのコード (RC) の SID を参照してください。</p></td>
</tr>
</tbody>
</table>

 

次の Sid では、特別な言及が必要です。

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
<td><p>RC</p></td>
<td><p>制限付きのコード</p>
<p>この SID は、信頼できないコードによってアクセスを制御するために使用されます。 RC でのトークンに対する ACL 検証トークンに対して 1 つ、2 つのチェックから成る&#39;Sid が (たとえば WD を含む)、および (RC および元のトークンの Sid のサブセットを含む通常) 2 番目のリストに対して 1 つの s 通常のリスト。 アクセスは、トークンが両方のテストに合格かどうかのみ許可されます。 そのため、実際に RC が他の Sid と組み合わせて動作します。</p>
<p>RC を指定する任意の ACL では、WD も指定する必要があります。 RC は、ACL で WD とペアになり、信頼できないコードを含むすべてのユーザーのスーパー セットが記載されています。</p>
<p>信頼できないコードには、コード エクスプ ローラーで実行 のオプションを使用して起動される可能性があります。 既定では、世界では信頼できないコードは含まれません。</p></td>
</tr>
<tr class="even">
<td><p>UD</p></td>
<td><p>ユーザー モード ドライバー</p>
<p>この SID は、ユーザー モード ドライバーへのアクセスを付与します。 現時点では、この SID は、ユーザー モード ドライバー フレームワーク (UMDF) 用に記述されているドライバーのみを説明します。 この SID は、Windows 8 以降で使用できます。</p>
<p>認識されるしない Windows の以前のバージョンで、 &quot;UD&quot;の省略形のこの SID (S-1-5-84-0-0-0-0-0) UMDF ドライバーへのアクセスを許可する完全修飾形式を指定する必要があります。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh439567" data-raw-source="[Controlling Device Access](https://msdn.microsoft.com/library/windows/hardware/hh439567)">デバイスへのアクセスを制御する</a>ユーザー モード ドライバー フレームワークのドキュメント。</p></td>
</tr>
</tbody>
</table>

 

### <a name="sddl-examples-for-device-objects"></a>デバイス オブジェクトの SDDL の例

このセクションでは、Wdmsec.h 内で見つかった定義済みの SDDL 文字列について説明します。 デバイス オブジェクトの新しい SDDL 文字列を定義するのにテンプレートとしてこれらを使用できます。

SDDL\_DEVOBJ\_カーネル\_のみ

**"D:P"**

SDDL\_DEVOBJ\_カーネル\_「空」の ACL をのみです。 ユーザー モードのコード (システムとして実行されているプロセスを含む) は、デバイスを開くことができません。

PnP バス ドライバーは、PDO を作成するときに、この記述子を使用できます。 INF ファイルは、デバイスのセキュリティ設定をより緩やかなを指定し、できます。 この記述子を指定すると、バス ドライバーは、INF が処理される前に、デバイスを開こうとするとは成功しないことを確認します。

同様に、非 WDM ドライバーは、そのデバイス オブジェクトが、適切なまでアクセスできなくなるのこの記述子を使用できます (インストーラー) などのユーザー モードのプログラムは、レジストリの最終的なセキュリティ記述子を設定します。

このような場合のすべてでは、既定値は、厳重なセキュリティが緩和されると、必要に応じては。

SDDL\_DEVOBJ\_SYS\_すべて

**"D:P(A;;GA;;;SY)"**

SDDL\_DEVOBJ\_SYS\_SDDL に似ていますがすべて\_DEVOBJ\_カーネル\_のみ、カーネル モード コードだけでなく点を除き、システムとして実行されているユーザー モード コードも開くことが、アクセスのデバイスです。

従来、ドライバー強固なセキュリティの設定で開始するこの ACL を使用し、そのサービスを使用して、実行時に個々 のユーザー デバイスを開く、 **SetFileSecurity**ユーザー モード関数。 この場合、サービスは、システムとして実行されている必要があります。

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_すべて

**"D:P(A;;GA;;;SY)(A;;GA;;;BA)"**

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_すべてにより、デバイスのカーネル、システム、および管理者の完全な制御。 他のユーザーがデバイスにアクセスできません。

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_RWX\_WORLD\_R

**"D:P(A;;GA;;;SY)(A;;GRGWGX;;;BA)(A;;GR;;;WD)"**

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_RWX\_WORLD\_R により、デバイスのカーネルとシステムの完全な制御。 既定では、管理者は、デバイス全体にアクセスできますが、(管理者必要がありますかかるデバイスの制御最初)。 ACL を変更することはできません。

すべてのユーザー (世界の SID) には、読み取りアクセス権が与えられます。 コードは、デバイスにアクセスできない信頼されていない (信頼されていないコードのコード エクスプ ローラーで実行 のオプションを使用して起動される可能性があります。 既定では、世界は扱いません制限付きのコード。)

トラバーサルのアクセスが通常のユーザーに付与されていないことにも注意してください。 そのため、名前空間を使用したデバイスの適切な記述子できないこの可能性があります。

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_RWX\_WORLD\_R\_RES\_R

**"D:P(A;;GA;;;SY)(A;;GRGWGX;;;BA)(A;;GR;;;WD)(A;;GR;;;RC)"**

SDDL\_DEVOBJ\_SYS\_すべて\_ADM\_RWX\_WORLD\_R\_RES\_R により、デバイスのカーネルとシステムの完全な制御。 既定では、管理者は、デバイス全体にアクセスできますが、(管理者必要がありますかかるデバイスの制御最初)。 ACL を変更することはできません。

すべてのユーザー (世界の SID) には、読み取りアクセス権が与えられます。 さらに、信頼できないコードは、アクセス コードにも使用できます。 信頼できないコードには、コード エクスプ ローラーで実行 のオプションを使用して起動される可能性があります。 既定では、世界では制限付きのコードは含まれません。

トラバーサルのアクセスが通常のユーザーに付与されていないことにも注意してください。 そのため、名前空間を使用したデバイスの適切な記述子できないこの可能性があります。

 

上記の SDDL 文字列には、任意の継承修飾子が含まれていないことに注意してください。 そのため、デバイス オブジェクトの適切なのみと、ファイルまたはレジストリ キーのない使用する必要があります。 SDDL を使用して継承を指定する方法については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





---
title: INF AddService ディレクティブ
description: INF DDInstall.Services セクションまたは INF DefaultInstall.Services セクション内では、AddService ディレクティブが使用されます。
ms.assetid: 3314da8b-3fde-462a-a64d-a0514710663a
keywords:
- INF AddService ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddService Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db323bce9bb2f6ab32fd34b607363eb3077719b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379462"
---
# <a name="inf-addservice-directive"></a>INF AddService ディレクティブ


**注**  モニターを表示またはモデムなどのすべてのドライバーを必要としないデバイスをインストールする INF ファイルでこのディレクティブは使用されません。

 

**AddService**内ディレクティブの使用、 [ **INF *DDInstall*します。サービス セクション**](inf-ddinstall-services-section.md)または[ **INF DefaultInstall.Services セクション**](inf-defaultinstall-services-section.md)します。 これには、ドライバー、方法などを使用して、サービスが読み込まれると、およびその他の従来の基になるドライバーまたはサービスへの依存関係に関連付けられているサービスの特性を指定します。 必要に応じて、このディレクティブは、デバイスのイベント ログ サービスも設定します。

```ini
[DDInstall.Services] 
 
AddService=ServiceName,[flags],service-install-section
                     [,event-log-install-section[,[EventLogType][,EventName]]]
...
```

## <a name="entries"></a>エントリ


<a href="" id="servicename"></a>*サービス名*  
インストールするサービスの名前を指定します。 この値はデバイスの場合は"sermouse、"など、そのドライバーの汎用的な名前またはそのようないくつかの名前は、通常です。 この名前はローカライズされていない必要があります。 システムのローカル言語に関係なく同じ必要があります。

<a href="" id="flags"></a>*フラグ*  
いずれかが指定されるか、次のシステム定義フラグで定義されている複数 (Or) *Setupapi.h*、16 進数の値として表されます。

<a href="" id="0x00000001--spsvcinst-tagtofront-"></a>**0x00000001** (SPSVCINST_TAGTOFRONT)  
名前付きサービスのタグを積み重ねないに読み込まれる最初にそのグループ内 (この INF 仕様を使用した後でインストールされているデバイスでは、その変位させます) しない限り、そのグループの順序リストの先頭に移動します。 WDM ドライバーの PnP デバイスとデバイスのみをインストールする INF ファイルでは、このフラグは設定しないでください。

<a href="" id="0x00000002--spsvcinst-assocservice-"></a>**0x00000002** (SPSVCINST_ASSOCSERVICE)  
この INF ファイルによってインストールされているデバイスのドライバーの PnP 関数 (またはレガシ ドライバー) として、名前付きサービスを割り当てます。

サービスがデバイスの機能のドライバーであることを示す、サービスを指定する必要があります、 **SPSVCINST_ASSOCSERVICE**フラグ、 **AddService**ディレクティブ。  フィルター ドライバーやその他のドライバー コンポーネントなどのサービス、フラグが使用しない必要があります。

すべてのデバイス ドライバーの INF に関連付けられているサービスの 1 つだけ必要があります。  INF では拡張機能は、または、インクルードを使用して/、ディレクティブが関連付けられているサービスを別の INF に継承する必要がある場合、関連付けられているサービスは必要ありません。  関数のドライバーを必要としないデバイスの場合は、NULL ドライバーとしては、次のように指定できます。

```
AddService = ,2.
```

<a href="" id="0x00000008--spsvcinst-noclobber-displayname-"></a>**0x00000008** (SPSVCINST_NOCLOBBER_DISPLAYNAME)  
システムでこのサービスが既に存在する場合に指定されたサービスの (省略可能) のフレンドリ名を上書きしません。

<a href="" id="0x00000010--spsvcinst-noclobber-starttype-"></a>**0x00000010** (SPSVCINST_NOCLOBBER_STARTTYPE)  
このサービスを既に名前付きシステムが存在する場合、指定されたサービスのスタートアップの種類は上書きされません。

<a href="" id="0x00000020--spsvcinst-noclobber-errorcontrol-"></a>**0x00000020** (SPSVCINST_NOCLOBBER_ERRORCONTROL)  
名前付きサービスを既にこれがシステムに存在する場合、特定のサービスのエラー コントロールの値を上書きしません。

<a href="" id="0x00000040--spsvcinst-noclobber-loadordergroup-"></a>**0x00000040** (SPSVCINST_NOCLOBBER_LOADORDERGROUP)  
順序グループの読み込みの値を指定されたサービスの場合は、システムに存在する名前付きサービスが既にこのを上書きしません。 WDM ドライバーの PnP デバイスとデバイスのみをインストールする INF ファイルでは、このフラグは設定しないでください。

<a href="" id="0x00000080--spsvcinst-noclobber-dependencies--"></a>**0x00000080** (SPSVCINST_NOCLOBBER_DEPENDENCIES)   
このサービスを既に名前付きシステムが存在する場合、指定されたサービスの依存関係の一覧は上書きされません。 WDM ドライバーの PnP デバイスとデバイスのみをインストールする INF ファイルでは、このフラグは設定しないでください。

<a href="" id="0x00000100--spsvcinst-noclobber-description-"></a>**0x00000100** (SPSVCINST_NOCLOBBER_DESCRIPTION)  
システムでこのサービスが既に存在する場合、指定されたサービスの (省略可能) の説明は上書きされません。

<a href="" id="0x00000400--spsvcinst-clobber-security---windows-xp-and-later-versions-of-windows--"></a>**0x00000400** (SPSVCINST_CLOBBER_SECURITY) (Windows XP および Windows の以降のバージョン)   
システムでこのサービスが既に存在する場合は、サービスのセキュリティ設定を上書きします。

<a href="" id="0x00000800--spsvcsinst-startservice---windows-vista-and-later-versions-of-windows--"></a>**0x00000800** (SPSVCSINST_STARTSERVICE) (Windows Vista および Windows の以降のバージョン)   
サービスをインストールした後は、サービスを開始します。 このフラグは、function ドライバーのプラグ アンド プレイ (PnP) デバイスのフィルター ドライバーを実装するサービスを開始するのには使用できません。 それ以外の場合、このフラグを使用して、サービス コントロール マネージャー (SCM) によって管理されるユーザー モードまたはカーネル モードのサービスを開始できます。

<a href="" id="0x00001000--spsvcinst-noclobber-requiredprivileges---windows-7-and-later-versions-of-windows-"></a>**0x00001000** (SPSVCINST_NOCLOBBER_REQUIREDPRIVILEGES) (Windows 7 および Windows の以降のバージョン)  
このサービスは、システムに既に存在する場合、特定のサービスに対する権限は上書きされません。

<a href="" id="service-install-section"></a>*サービスのインストール-セクション*  
このデバイス (またはデバイス) の名前付きサービスをインストールするための情報を含む INF ライター定義のセクションを参照します。 詳細については、次を参照してください。**解説**セクション。

<a href="" id="event-log-install-section"></a>*event-log-install-section*  
必要に応じてをこのデバイス (またはデバイス) のイベント ログ サービスが設定されている INF ライター定義のセクションを参照します。

<a href="" id="eventlogtype"></a>*EventLogType*  
必要に応じてのいずれかを指定します。**システム**、**セキュリティ**、または**アプリケーション**します。 省略した場合、既定値は**システム**はほぼ常にデバイス ドライバーのインストールの適切な値。

たとえば、INF は指定**セキュリティ**場合にのみインストールするドライバーは、独自のセキュリティ サポートを提供します。

<a href="" id="eventname"></a>*eventName*  
必要に応じて、イベント ログに使用する名前を指定します。 省略した場合、既定値は、指定された*ServiceName*します。

<a name="remarks"></a>コメント
-------

システム定義の大文字と拡張機能を挿入できる、 <em>DDInstall</em>**します。サービス**を含むセクション、 **AddService**クロス オペレーティング システムやクロス プラットフォーム INF ファイルでプラットフォーム固有または OS 固有のインストールを指定するディレクティブ。

各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

**AddService**ディレクティブは名前付き参照する必要があります*サービス-インストール セクション*INF ファイルで別の場所。 このような各セクションでは、次の形式があります。

```ini
[service-install-section]
 
[DisplayName=name]
[Description=description-string]
ServiceType=type-code
StartType=start-code
ErrorControl=error-control-level
ServiceBinary=path-to-service
[StartName=driver-object-name]
[AddReg=add-registry-section[, add-registry-section] ...]
[DelReg=del-registry-section[, del-registry-section] ...]
[BitReg=bit-registry-section[,bit-registry-section] ...]
[LoadOrderGroup=load-order-group-name]
[Dependencies=depend-on-item-name[,depend-on-item-name]
[Security="security-descriptor-string"]...]
```

各*サービスのインストール-セクション*必要がありますが、少なくとも**ServiceType**、 **StartType**、 **ErrorControl**、および**ServiceBinary**エントリは、ここに示すようにします。 ただし、残りのエントリは省略可能です。

### <a name="service-install-section-entries-and-values"></a>サービス インストール セクション エントリと値

<a href="" id="displayname-name"></a>**DisplayName**=*name*  
容易にするため、% で表される、ローカライズの通常は、サービス/ドライバーのフレンドリ名を指定します*strkey*% のトークンで定義されている、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

<a href="" id="description-description-string"></a>**説明**=*説明文字列*  
必要に応じて、通常は、% で表される、サービスを説明する文字列を指定します*strkey*% のトークンで定義されている、**文字列**INF ファイルのセクション。

この文字列は、ユーザーよりもサービスの詳細について、 **DisplayName**します。 たとえば、 **DisplayName** 「DHCP クライアント」と説明は「登録および IP アドレスと DNS 名を更新してネットワーク構成を管理」のようなものである可能性がありますなどがあります。

*説明文字列*わかりやすいが厄介にしない限り長くしています。 場合、*説明文字列*任意 % を含む*strkey*% トークンは、各トークンは、最大 511 文字を表すことができます。 合計の文字列では、文字列トークン置換後にする必要がありますは 1024 文字以下。

<a href="" id="servicetype-type-code"></a>**ServiceType**=*型コード*  
カーネル モード デバイス ドライバーの型コードは、0x00000001 (SERVICE_KERNEL_DRIVER) に設定する必要があります。

*型コード*にデバイスを設定する必要がありますがインストールされている Microsoft Win32 サービス**0x00000010** (SERVICE_WIN32_OWN_PROCESS) または**0x00000020** (SERVICE_WIN32_SHARE_PROCESS)。 型コードの値を結合する場合は、Win32 サービス、デスクトップと対話できる、 **0x00000100** (SERVICE_INTERACTIVE_PROCESS)。

*型コード*最高レベルのネットワーク リダイレクター、または、ファイル システム ドライバーなどのドライバーに設定**0x00000002** (SERVICE_FILE_SYSTEM_DRIVER)。

SERVICE_xxxx 定数で定義されて*Wdm.h*と*Ntddk.h*します。

<a href="" id="starttype-start-code"></a>**StartType**=*スタート コード*  
10 進数のいずれかで表される、次の数値値の 1 つとして、16 進数表記で、次の一覧に示すように、ドライバーを開始するタイミングを指定します。

<a href="" id="0x0--service-boot-start-"></a>**0x0** (SERVICE_BOOT_START)  
オペレーティング システム ローダーによって開始されたドライバーを示します。

この値は、オペレーティング システムの読み込みに必要なデバイスのドライバーを使用する必要があります。

<a href="" id="0x1--service-system-start-"></a>**0x1** (SERVICE_SYSTEM_START)  
オペレーティング システムの初期化中に、ドライバーの開始を示します。

この値は、初期化中にデバイスの検出を行う、システムをロードする必要はありませんが、PnP ドライバーで使用する必要があります。

たとえば、レガシ デバイスも検出する PnP ドライバーがこの値の INF でこれを指定する必要があります、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)場合でも、そのデバイスにすることはできません、従来のデバイスを検索するルーチンが呼び出されますPnP マネージャーによって列挙されます。

<a href="" id="0x2--service-auto-start-"></a>**0x2** (SERVICE_AUTO_START)  
システムの起動時に、サービス コントロール マネージャーによって開始ドライバーを示します。

この値は使わないで INF ファイルで WDM または PnP デバイス ドライバー。

<a href="" id="0x3--service-demand-start-"></a>**0x3** (SERVICE_DEMAND_START)  
必要に応じて、いずれかまたは場合によって、対応するデバイスが列挙されたときに、PnP マネージャーによって、非 PnP デバイスの需要の明示的なユーザーに応答でサービス コントロール マネージャーによって開始ドライバーを示します。

この値は、システムを読み込むために不要なデバイスのすべての WDM ドライバーとは、システムの読み込みに必要なもデバイスの検出に関与するすべての PnP デバイス ドライバーの INF ファイルで使用する必要があります。

<a href="" id="0x4--service-disabled-"></a><strong>0x4 (</strong>SERVICE_DISABLED)  
ドライバーを起動できないことを示します。

この値は、デバイス ドライバー サービスを一時的に無効にできます。 ただし、その INF ファイルのサービスのインストールのセクションではこの値が指定されている場合は、デバイス ドライバーをインストールできません。

詳細については**StartType**を参照してください[ドライバーの読み込み順序を指定する](specifying-driver-load-order.md)します。

<a href="" id="errorcontrol-error-control-level"></a>**ErrorControl**=*コントロール レベルのエラー*  
10 進数のいずれかで表される、次の数値値の 1 つとして、16 進数表記で、次の一覧に示すように、エラー制御のレベルを指定します。

<a href="" id="0x0--service-error-ignore-"></a>**0x0** (SERVICE_ERROR_IGNORE)  
ドライバーがロードまたは初期化するには、失敗した場合システムの起動を続行し、ユーザーに警告を表示できません。

<a href="" id="0x1--service-error-normal-"></a>**0x1** (SERVICE_ERROR_NORMAL)  
ドライバーは、読み込みまたはそのデバイスの初期化に失敗した場合、システムの起動が続行する必要がありますが、ユーザーに警告を表示します。

<a href="" id="0x2--service-error-severe-"></a>**0x2** (SERVICE_ERROR_SEVERE)  
システムの起動が、レジストリを切り替える場合は、ドライバーの読み込みに失敗、**前回正常起動時**コントロール セットと、ドライバーがもう一度読み込みまたはデバイスとドライバーの初期化エラーを示す場合でも、システムの起動を続行します。

<a href="" id="0x3--service-error-critical-"></a>**0x3** (SERVICE_ERROR_CRITICAL)  
ドライバーの読み込みに失敗して、システムの起動時には、レジストリを使用していない場合**前回正常起動時**コントロール セットに切り替え、**前回正常起動時**もう一度やり直してください。

使用する場合、スタートアップがまだ失敗する場合**前回正常起動時**、バグ チェック ルーチンを実行します。 (*のみ*デバイス/ドライバーのシステムをブートするために必要な INF ファイルでこの値を指定します)。

<a href="" id="servicebinary-path-to-service"></a>**ServiceBinary**=*サービスへのパス*  
表される、サービスのバイナリのパスを指定します *%dirid\\filename*します。

*Dirid*数は、カスタム ディレクトリの識別子またはで説明されているディレクトリのシステム定義の識別子のいずれかのいずれか[を使用して Dirids](using-dirids.md)します。 特定*filename*ファイルが既に転送を指定します (を参照してください、 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md))、ターゲット ディレクトリに、ソース配布メディアからコンピューター。

<a href="" id="startname-driver-object-name"></a>**StartName**=*driver-object-name*  
この省略可能なエントリでは、このデバイスを表すドライバー オブジェクトの名前を指定します。 場合*型コード*指定**1** (SERVICE_KERNEL_DRIVER) または**2** (SERVICE_FILE_SYSTEM_DRIVER) この名前は I/O マネージャーが読み込みに使用するドライバー オブジェクト名、ドライバー。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg**=*add-registry-section*\[**,**<em>add-registry-section</em>\]...  
1 つを参照またはより INF ライター-定義*追加レジストリ セクション*で新しくインストールしたサービスに関連するすべてのレジストリ情報が設定されています。 **HKR**などの仕様、*追加レジストリ セクション*指定、 **HKLM\\システム\\CurrentControlSet\\サービス\\ServiceName**レジストリ キー。 詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)します。

サービス インストール セクションには、このディレクティブを使用ことはほとんどありません。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**DelReg**=*del-registry-section*\[**,**<em>del-registry-section</em>\]...  
1 つを参照またはより INF ライター-定義*del のセクション レジストリ*関連レジストリで、既にインストールされているサービスの情報が削除されます。 **HKR**などの仕様、 *del-section レジストリ*指定、 **HKLM\\システム\\CurrentControlSet\\サービス\\ServiceName**レジストリ キー。 詳細については、次を参照してください。 [ **INF してディレクティブ**](inf-delreg-directive.md)します。

このディレクティブは使用がほとんどない、*サービス-インストール セクション*が、同じデバイス ドライバー/サービスの以前のインストール用にレジストリを「更新」する INF で使用する場合があります。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**BitReg**=*bit-registry-section*\[**,**<em>bit-registry-section</em>\]...  
有効では、*サービス-インストール セクション*はほぼ使用しませんが、します。 **HKR**などの仕様、*ビットのレジストリ セクション*することも指定、 **HKLM\\システム\\CurrentControlSet\\サービス\\ServiceName**レジストリ キー。

<a href="" id="loadordergroup-load-order-group-name"></a>**LoadOrderGroup**=*load-order-group-name*  
この省略可能なエントリでは、このドライバーがメンバーであるロード順序グループを識別します。 "Standard"ロード順序グループのいずれかのようにできますが**SCSI**クラスまたは**NDIS**します。

一般に、このエントリは、このようなグループで従来の依存関係がある場合を除き WDM ドライバーとデバイスの場合、または排他的 PnP デバイスの場合に必要です。 ただし、このエントリは、一連の特定の順序でドライバーを読み込むことでデバイスの検出がサポートされている場合に役立ちます。

詳細については**LoadOrderGroup**を参照してください[ドライバーの読み込み順序を指定する](specifying-driver-load-order.md)します。

<a href="" id="dependencies-depend-on-item-name--depend-on-item-name----"></a>**依存関係**=*依存、上の項目の名前*\[**、**<em>依存、上の項目の名前</em>\].  
各*依存、上の項目の名前*依存関係一覧内の項目は、デバイス ドライバーが依存するサービスまたはロード順序グループの名前を指定します。

場合、*依存、上の項目の名前*サービスでは、このドライバーを開始する前に実行されている必要がありますサービスを指定します。 たとえば、システム提供の Win32 の TCP/IP 印刷サービスの INF は、基になる (カーネル モード) の TCP/IP トランスポート スタックのサポートに依存します。 その結果、としては、このエントリの指定 TCP/IP 印刷サービスの INF**依存関係 TCPIP =** します。

A*依存、上の項目の名前*このデバイス/ドライバーが依存しているロード順序グループを指定できます。 指定されたグループの少なくとも 1 つのメンバーが開始された場合にのみ、このようなドライバーが開始されます。 プラス記号 (+) でグループ名を前します。 たとえば、システム RAS サービス INF のようなエントリがある**依存関係 = + NetBIOSGroup, RpcSS**ロード順序グループとサービスの両方を一覧表示します。

<a href="" id="security--security-descriptor-string-"></a>**セキュリティ**="*セキュリティ記述子の文字列*"  
サービスに適用する、セキュリティ記述子を指定します。 このセキュリティ記述子には、開始、停止、およびサービスの構成などの操作を実行するために必要なアクセス許可を指定します。 *セキュリティ記述子の文字列*値を DACL を示すためにトークンを使用する文字列です (**d:**) セキュリティ コンポーネント。

セキュリティ記述子文字列については、次を参照してください。[セキュリティ記述子定義言語 (Windows)](https://msdn.microsoft.com/library/windows/desktop/aa379567)します。 セキュリティ記述子文字列の形式の詳細については、セキュリティ記述子定義言語 (Windows) を参照してください。

セキュリティ記述子を指定する方法の詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](creating-secure-device-installations.md)します。

### <a name="specifying-driver-load-order"></a>ドライバーの読み込み順序の指定

オペレーティング システムに従ってドライバーの読み込み、*サービス-インストール セクション*  **StartType**値、次のように。

-   システムのブート開始フェーズ中にオペレーティング システムを読み込むすべて**0x0** (SERVICE_BOOT_START) ドライバー。
-   システムの開始フェーズでは、オペレーティング システムが初めて読み込まれるすべての WDM と PnP ドライバーの PnP マネージャーがデバイス ノードを検索する (*devnode*)、レジストリで **.\\Enum**ツリー (INF ファイルを指定するかどうか**0x01** SERVICE_SYSTEM_START のまたは**0x03** SERVICE_DEMAND_START 用)。オペレーティング システムでは、すべての残り SERVICE_SYSTEM_START ドライバーを読み込みます。
-   システムの自動起動フェーズでは、オペレーティング システムは、すべての残り SERVICE_AUTO_START ドライバーを読み込みます。

詳細については**依存関係**を参照してください[ドライバーの読み込み順序を指定する](specifying-driver-load-order.md)します。

### <a name="promoting-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>ドライバーの StartType ブート シナリオによっては、ブート時の昇格

ブートのシナリオに応じて使用できます、 **BootFlags**オペレーティング システムでドライバーを昇格させるときを制御するレジストリ値**StartType** 0x0 (SERVICE_BOOT_START) する値。 いずれかを指定することができますか、値は次の数値、16 進数の値として表される複数 (Or)。

-   0x1 (CM_SERVICE_NETWORK_BOOT_LOAD) では、ネットワークから起動中の場合、ドライバーを昇格することを示します。

-   0x2 (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD) では、VHD から起動中の場合、ドライバーを昇格することを示します。

-   0x4 (CM_SERVICE_USB_DISK_BOOT_LOAD) では、ドライバーは、USB ディスクから起動する場合に昇格することを示します。

-   0x8 (CM_SERVICE_SD_DISK_BOOT_LOAD) では、SD ストレージから起動する場合、ドライバーを昇格することを示します。

-   0x10 (CM_SERVICE_USB3_DISK_BOOT_LOAD) では、USB 3.0 コント ローラー上のディスクから起動する場合、ドライバーを昇格することを示します。

-   0x20 (CM_SERVICE_MEASURED_BOOT_LOAD) では、起動してメジャー ブートが有効になっている場合、ドライバーを昇格することを示します。

-   0x40 (CM_SERVICE_VERIFIER_BOOT_LOAD) では、起動して verifier ブートが有効になっている場合、ドライバーを昇格することを示します。

-   0x80 (CM_SERVICE_WINPE_BOOT_LOAD) では、WinPE で起動する場合、ドライバーを昇格することを示します。

*サービス-インストール セクション*は次の一般的な形式があります。

```ini
[service-install-section]
AddReg=add-registry-section
...

[add-registry-section]
HKR,,BootFlags,0x00010003,0x14 ; CM_SERVICE_USB3_DISK_BOOT_LOAD|CM_SERVICE_USB_DISK_BOOT_LOAD
```

### <a name="registering-for-event-logging"></a>イベント ログに登録します。

**AddService**ディレクティブを参照できます、*イベント ログ-インストール セクション*INF ファイルで別の場所。 このような各セクションでは、次の形式があります。

```ini
[event-log-install-section]
 
AddReg=add-registry-section[, add-registry-section]... 
[DelReg=del-registry-section[, del-registry-section]...] 
[BitReg=bit-registry-section[,bit-registry-section]...]
 ...
```

一般的なデバイスとドライバー INF ファイルの場合、*イベント ログ-インストール セクション*のみを使用して、 **AddReg**ドライバーのイベント ログ メッセージ ファイルを設定するディレクティブ。 **HKR**内の指定、*追加レジストリ セクション*指定、 **HKLM\\システム\\CurrentControlSet\\サービス\\EventLog\\**<em>EventLogType</em>**\\**<em>EventName</em>レジストリ キー。 このイベント ログを記録*追加レジストリ セクション*は次の一般的な形式があります。

```ini
[drivername_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"path\IoLogMsg.dll;path\driver.sys"
HKR,,TypesSupported,0x00010001,7 
```

具体的にはのセクションでは、次のようにデバイス ドライバーの作成、レジストリ サブキーで値の 2 つのエントリを追加します。

-   という名前の値のエントリ**EventMessageFile**の種類は[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)FLG_ADDREG_TYPE_EXPAND_SZ 値によって指定された、 **0x00020000**します。 二重引用符 (") で囲まれた、その値は、システム提供を関連付けます*IoLogMsg.dll* (ただし、別のログ出力 DLL を関連付けることができます) ドライバーのバイナリ ファイルを使用します。 これらの各ファイルへのパスを指定すると、次のように、通常は。

    *%%SystemRoot%%\\System32\\IoLogMsg.dll*

    *%%SystemRoot%%\\System32\\drivers\\driver.sys*

-   という名前の値のエントリ**TypesSupported**の種類は[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)FLG_ADDREG_TYPE_DWORD 値によって指定された、 **0x00010001**します。

    この値は、ドライバー、 **7**します。 EVENTLOG_AUDIT_ を設定せずにこの値はビットごとの EVENTLOG_SUCCESS または、EVENTLOG_ERROR_TYPE、EVENTLOG_WARNING_TYPE、および EVENTLOG_INFORMATION_TYPE に相当*XXX*ビット。

*イベント ログ-インストール セクション*こともできます、 [**して**](inf-delreg-directive.md)既存を明示的に削除することによって、以前にインストールされているイベント ログ メッセージ ファイルを削除するディレクティブ**EventMessageFile**と**TypesSupported**エントリ以外の場合、ドライバーのバイナリを新しくインストールされたドライバによって置き換えられるは値します。 (「」も参照[ **INF DelService ディレクティブ**](inf-delservice-directive.md))。

中に、 [ **BitReg** ](inf-bitreg-directive.md)ディレクティブは、INF ライターの定義内で無効でも*インストール ログ イベントが*-*セクション*はほとんどないため、デバイス ドライバーのイベント ログの標準値のエントリがないビットマスクです。

<a name="examples"></a>使用例
--------

この例によって参照されるサービスのインストールとインストール ログ イベントがセクションを示しています、 **AddService**ディレクティブの例では、前半で既に示した[ * **DDInstall *。サービス**](inf-ddinstall-services-section.md)します。

```ini
[sermouse_Service_Inst]
DisplayName    = %sermouse.SvcDesc%
ServiceType    = 1                   ; = SERVICE_KERNEL_DRIVER
StartType      = 3                   ; = SERVICE_DEMAND_START
ErrorControl   = 1                   ; = SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\sermouse.sys
LoadOrderGroup = Pointer Port

[sermouse_EventLog_Inst]
AddReg = sermouse_EventLog_AddReg

[sermouse_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll;
       %%SystemRoot%%\System32\drivers\sermouse.sys"
;
; Preceding entry on single line in INF file. Enclosing quotation marks 
; prevent the semicolon from being interpreted as a comment.
;
HKR,,TypesSupported,0x00010001,7

[mouclass_Service_Inst]
DisplayName    = %mouclass.SvcDesc%
ServiceType    = 1                   ; = SERVICE_KERNEL_DRIVER
StartType      = 1                   ; = SERVICE_SYSTEM_START
ErrorControl   = 1                   ; = SERVICE_ERROR_NORMAL
ServiceBinary  = %12%\mouclass.sys
LoadOrderGroup = Pointer Class

[mouclass_EventLog_Inst]
AddReg = mouclass_EventLog_AddReg

[mouclass_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll;
       %%SystemRoot%%\System32\drivers\mouclass.sys"
HKR,,TypesSupported,0x00010001,7
; ...
[Strings]
; ...
sermouse.SvcDesc = "Serial Mouse Driver"
mouclass.SvcDesc = "Mouse Class Driver"
```

参照の例では、 [ * **DDInstall *。HW** ](inf-ddinstall-hw-section.md)前に説明したセクションでは、によって参照されるいくつかのサービスのインストール セクションも示しています、 **AddService** PnP 上フィルター ドライバーをセットアップするディレクティブ。

## <a name="see-also"></a>関連項目


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**DelService**](inf-delservice-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**文字列**](inf-strings-section.md)

 

 







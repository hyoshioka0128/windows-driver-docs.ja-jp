---
title: INF AddService ディレクティブ
description: AddService ディレクティブは、INF DDInstall. Services セクションまたは INF DefaultInstall セクション内で使用されます。
ms.assetid: 3314da8b-3fde-462a-a64d-a0514710663a
keywords:
- INF AddService ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddService Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d82e9ce6809ba0ac558e78f3cb6e9c724a7cade
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828799"
---
# <a name="inf-addservice-directive"></a>INF AddService ディレクティブ


**注**  このディレクティブは、モデムやディスプレイモニターなど、ドライバーを必要としないデバイスをインストールする INF ファイルでは使用されません。

 

**Addservice**ディレクティブは、 [**INF *ddinstall*内で使用されます。サービスセクション**](inf-ddinstall-services-section.md)または[**INF DefaultInstall セクション**](inf-defaultinstall-services-section.md)。 これは、サービスの読み込み方法やタイミングなど、ドライバーに関連付けられているサービスの特性、およびその他の基になるレガシドライバーまたはサービスへの依存関係を指定します。 必要に応じて、このディレクティブはデバイスのイベントログサービスも設定します。

```ini
[DDInstall.Services] 
 
AddService=ServiceName,[flags],service-install-section
                     [,event-log-install-section[,[EventLogType][,EventName]]]
...
```

## <a name="entries"></a>エントリ


<a href="" id="servicename"></a>*ServiceName*  
インストールするサービスの名前を指定します。 デバイスの場合、この値は通常、"sermouse" やそのような名前のように、ドライバーの汎用的な名前になります。 この名前はローカライズしないでください。 システムのローカル言語に関係なく、同じである必要があります。

<a href="" id="flags"></a>*示す*  
*Setupapi.log*で定義されている次のシステム定義フラグのうち、16進数の値で表されるものを1つ以上指定します。

<a href="" id="0x00000001--spsvcinst-tagtofront-"></a>**0x00000001** (SPSVCINST_TAGTOFRONT)  
名前付きサービスのタグをそのグループの順序の一覧の先頭に移動します。これにより、そのグループ内で最初に読み込まれます (この INF 仕様の後でインストールされたデバイスが移動する場合を除きます)。 このフラグを設定しないようにする必要があります。

<a href="" id="0x00000002--spsvcinst-assocservice-"></a>**0x00000002** (SPSVCINST_ASSOCSERVICE)  
この INF ファイルによってインストールされるデバイスの PnP 関数ドライバー (またはレガシドライバー) として、名前付きサービスを割り当てます。

サービスがデバイスの関数ドライバーであることを示すには、サービスで**Addservice**ディレクティブに**SPSVCINST_ASSOCSERVICE**フラグを指定する必要があります。  フィルタードライバーやその他のドライバーコンポーネントなどのサービスでは、フラグを使用しないでください。

すべてのデバイスドライバーの INF には、関連付けられたサービスが1つだけ必要です。  INF には、拡張機能の場合は関連付けられたサービスが必要ない場合や、関連付けられているサービスを別の INF から継承する場合は、インクルード/要求ディレクティブが使用されます。  関数ドライバーを必要としないデバイスの場合、NULL ドライバーは次のように指定できます。

```
AddService = ,2.
```

<a href="" id="0x00000008--spsvcinst-noclobber-displayname-"></a>**0x00000008** (SPSVCINST_NOCLOBBER_DISPLAYNAME)  
このサービスがシステムに既に存在する場合は、指定されたサービスのフレンドリ名を上書きしないでください。

<a href="" id="0x00000010--spsvcinst-noclobber-starttype-"></a>**0x00000010** (SPSVCINST_NOCLOBBER_STARTTYPE)  
この名前付きサービスがシステムに既に存在する場合は、指定されたサービスの開始の種類を上書きしないでください。

<a href="" id="0x00000020--spsvcinst-noclobber-errorcontrol-"></a>**0x00000020** (SPSVCINST_NOCLOBBER_ERRORCONTROL)  
この名前付きサービスがシステムに既に存在する場合は、指定されたサービスのエラー制御値を上書きしないでください。

<a href="" id="0x00000040--spsvcinst-noclobber-loadordergroup-"></a>**0x00000040** (SPSVCINST_NOCLOBBER_LOADORDERGROUP)  
この名前付きサービスがシステムに既に存在する場合は、指定されたサービスの読み込み順序グループの値を上書きしないでください。 このフラグを設定しないようにする必要があります。

<a href="" id="0x00000080--spsvcinst-noclobber-dependencies--"></a>**0x00000080** (SPSVCINST_NOCLOBBER_DEPENDENCIES)   
この名前付きサービスがシステムに既に存在する場合は、指定されたサービスの依存関係の一覧を上書きしないでください。 このフラグを設定しないようにする必要があります。

<a href="" id="0x00000100--spsvcinst-noclobber-description-"></a>**0x00000100** (SPSVCINST_NOCLOBBER_DESCRIPTION)  
このサービスがシステムに既に存在する場合は、指定されたサービスの (省略可能) の説明を上書きしないでください。

<a href="" id="0x00000400--spsvcinst-clobber-security---windows-xp-and-later-versions-of-windows--"></a>**0x00000400** (SPSVCINST_CLOBBER_SECURITY) (windows XP 以降のバージョンの windows)   
このサービスがシステムに既に存在する場合は、サービスのセキュリティ設定を上書きします。

<a href="" id="0x00000800--spsvcsinst-startservice---windows-vista-and-later-versions-of-windows--"></a>**0x00000800** (SPSVCSINST_STARTSERVICE) (windows Vista 以降のバージョンの windows)   
サービスをインストールした後で、サービスを開始します。 このフラグを使用して、デバイスのプラグアンドプレイ (PnP) 関数ドライバーまたはフィルタードライバーを実装するサービスを開始することはできません。 それ以外の場合は、このフラグを使用して、サービスコントロールマネージャー (SCM) によって管理されているユーザーモードまたはカーネルモードサービスを開始できます。

<a href="" id="0x00001000--spsvcinst-noclobber-requiredprivileges---windows-7-and-later-versions-of-windows-"></a>**0x00001000** (SPSVCINST_NOCLOBBER_REQUIREDPRIVILEGES) (windows 7 以降のバージョンの windows)  
このサービスがシステムに既に存在する場合は、指定されたサービスの特権を上書きしないでください。

<a href="" id="service-install-section"></a>*サービス-インストール-セクション*  
このデバイス (またはデバイス) の名前付きサービスをインストールするための情報を含む、INF ライターで定義されたセクションを参照します。 詳細については、次の「**解説**」を参照してください。

<a href="" id="event-log-install-section"></a>*イベントログ-インストール-セクション*  
必要に応じて、このデバイス (またはデバイス) のイベントログサービスが設定されている INF ライターで定義されたセクションを参照します。

<a href="" id="eventlogtype"></a>*EventLogType*  
オプションで、**システム**、**セキュリティ**、または**アプリケーション**のいずれかを指定します。 省略した場合、既定では**System**になります。これは、デバイスドライバーをインストールするのに最適な値です。

たとえば、INF は、インストールされているドライバーが独自のセキュリティサポートを提供する場合にのみ、**セキュリティ**を指定します。

<a href="" id="eventname"></a>*EventName*  
必要に応じて、イベントログに使用する名前を指定します。 省略した場合は、指定した*ServiceName*に既定値が設定されます。

<a name="remarks"></a>注釈
-------

システム定義および大文字と小文字を区別しない拡張機能は、 <em>Ddinstall</em>に挿入でき**ます。** プラットフォーム固有または OS 固有のインストールを指定するために、クロスオペレーティングシステムまたはクロスプラットフォームの INF ファイルに**addservice**ディレクティブを含む Services セクション。

各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**Addservice**ディレクティブは、INF ファイル内の他の場所にある、名前付き*サービスの install セクション*を参照する必要があります。 各セクションには、次の形式があります。

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

ここに示すように、各*サービスのインストールセクション*には、少なくとも**ServiceType**、 **starttype**、 **errorcontrol**、および**servicebinary**の各エントリが必要です。 ただし、残りのエントリは省略可能です。

### <a name="service-install-section-entries-and-values"></a>サービス-インストールセクションのエントリと値

<a href="" id="displayname-name"></a>**DisplayName**=*名*  
サービス/ドライバーのフレンドリ名を指定します。これは通常、ローカライズを容易にするために、INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義された%*strkey*% トークンとして表現されます。

<a href="" id="description-description-string"></a>**説明**=説明 *-文字列*  
必要に応じて、サービスを説明する文字列を指定します。この文字列は、通常、INF ファイルの**文字列**セクションで定義されている%*strkey*% token として表現されます。

この文字列は、サービスに関する詳細情報を**DisplayName**よりも多くのユーザーに提供します。 たとえば、 **DisplayName**は "DHCP クライアント" のようなものであり、"IP アドレスと DNS 名の登録と更新によってネットワーク構成を管理する" のような説明が表示されることがあります。

*説明文字列*は、わかりやすくするために十分な長さである必要がありますが、それほど厄介ではありません。 *説明文字列*に%*strkey*% トークンが含まれている場合、各トークンは最大511文字を表すことができます。 文字列トークンの置換後の合計文字列は、1024文字を超えないようにする必要があります。

<a href="" id="servicetype-type-code"></a>**ServiceType**=*タイプコード*  
カーネルモードデバイスドライバーの種類コードを 0x00000001 (SERVICE_KERNEL_DRIVER) に設定する必要があります。

デバイスにインストールされている Microsoft Win32 サービスの*種類コード*は、 **0x00000010** (SERVICE_WIN32_OWN_PROCESS) または**0x00000020** (SERVICE_WIN32_SHARE_PROCESS) に設定する必要があります。 Win32 サービスがデスクトップと対話できる場合は、型コードの値を**0x00000100** (SERVICE_INTERACTIVE_PROCESS) と組み合わせる必要があります。

リダイレクター、ファイルシステムドライバーなど、最高レベルのネットワークドライバーの*種類コード*は、 **0x00000002** (SERVICE_FILE_SYSTEM_DRIVER) に設定する必要があります。

SERVICE_xxxx 定数は、 *Wdm*および*Ntddk*で定義されています。

<a href="" id="starttype-start-code"></a>**Starttype**=*の開始コード*  
次の一覧に示されているように、10進表記またはのいずれかで表される、次の数値のいずれかとしてドライバーを開始するタイミングを指定します。

<a href="" id="0x0--service-boot-start-"></a>**0x0** (SERVICE_BOOT_START)  
オペレーティングシステムローダーによって開始されたドライバーを示します。

この値は、オペレーティングシステムの読み込みに必要なデバイスのドライバーに使用する必要があります。

<a href="" id="0x1--service-system-start-"></a>**0x1** (SERVICE_SYSTEM_START)  
オペレーティングシステムの初期化中にドライバーが開始されたことを示します。

この値は、初期化中にデバイスの検出を行う PnP ドライバーで使用する必要がありますが、システムの読み込みには必要ありません。

たとえば、レガシデバイスを検出できる PnP ドライバーでは、そのデバイスが PnP マネージャーによって列挙されていない場合でも、そのデバイスを検出するために[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが呼び出されるように、この値を INF に指定する必要があります。

<a href="" id="0x2--service-auto-start-"></a>**0x2** (SERVICE_AUTO_START)  
システムの起動時にサービスコントロールマネージャーによって開始されたドライバーを示します。

この値は、WDM または PnP デバイスドライバーの INF ファイルでは使用しないでください。

<a href="" id="0x3--service-demand-start-"></a>**0x3** (SERVICE_DEMAND_START)  
ドライバーがオンデマンドで開始されたことを示します。 pnp マネージャーは、対応するデバイスが列挙されるか、または、PnP 以外のデバイスに対する明示的なユーザーの要求に応じてサービスコントロールマネージャーによって検出されます。

この値は、システムの読み込みに必要ないデバイスのすべての WDM ドライバー、およびデバイスの検出に関与しないすべての PnP デバイスドライバーの INF ファイルで使用する必要があります。

<a href="" id="0x4--service-disabled-"></a><strong>0x4 (</strong>SERVICE_DISABLED)  
開始できないドライバーを示します。

この値を使用して、デバイスのドライバーサービスを一時的に無効にすることができます。 ただし、この値が INF ファイルの service-install セクションで指定されている場合、デバイス/ドライバーをインストールすることはできません。

**Starttype**の詳細については、「[ドライバーの読み込み順序の指定](specifying-driver-load-order.md)」を参照してください。

<a href="" id="errorcontrol-error-control-level"></a>**Errorcontrol**=*エラー制御レベル*  
次の一覧に示すように、10進形式またはで表される、次の数値のいずれかの数値としてのエラー制御レベルを指定します。

<a href="" id="0x0--service-error-ignore-"></a>**0x0** (SERVICE_ERROR_IGNORE)  
ドライバーの読み込みまたは初期化に失敗した場合は、システムの起動に進み、ユーザーに警告を表示しません。

<a href="" id="0x1--service-error-normal-"></a>**0x1** (SERVICE_ERROR_NORMAL)  
ドライバーがデバイスの読み込みまたは初期化に失敗した場合、システムの起動は続行しますが、ユーザーに警告が表示されます。

<a href="" id="0x2--service-error-severe-"></a>**0x2** (SERVICE_ERROR_SEVERE)  
ドライバーの読み込みに失敗した場合、システムのスタートアップは、ドライバーが読み込みまたはデバイス/ドライバーの初期化エラーを再度示す場合でも、レジストリの**正常**なコントロールセットに切り替え、システムの起動を続行する必要があります。

<a href="" id="0x3--service-error-critical-"></a>**0x3** (SERVICE_ERROR_CRITICAL)  
ドライバーの読み込みに失敗し、システムのスタートアップがレジストリの**正常**でないコントロールセットを使用していない場合は、[**前回**の実行時] に切り替えて、もう一度やり直してください。

**正常**に実行されているときにスタートアップが失敗する場合は、バグチェックルーチンを実行します。 (システムでブートするのに必要なデバイス/ドライバー*のみ*が INF ファイルにこの値を指定します)。

<a href="" id="servicebinary-path-to-service"></a>**Servicebinary**=*パスからサービスへのパス*  
サービスのバイナリのパスを指定します。このパスは *% dirid%\\filename*で表されます。

*Dirid*番号は、カスタムディレクトリ識別子、または「 [Dirid の使用](using-dirids.md)」で説明されているシステム定義のディレクトリ識別子のいずれかです。 指定されたファイル*名*によって、ソース配布メディアからターゲットコンピューター上のそのディレクトリに転送されたファイル ( [**INF の CopyFiles ディレクティブ**](inf-copyfiles-directive.md)を参照) が指定されます。

<a href="" id="startname-driver-object-name"></a>**StartName**=*driver-オブジェクト名*  
この省略可能なエントリは、このデバイス/ドライバーを表すドライバーオブジェクトの名前を指定します。 *型コード*で**1** (SERVICE_KERNEL_DRIVER) または**2** (SERVICE_FILE_SYSTEM_DRIVER) が指定されている場合、この名前は、i/o マネージャーがドライバーを読み込むために使用するドライバーオブジェクトの名前になります。

<a href="" id="addreg-add-registry-section--add-registry-section----"></a>**AddReg**= *\[* 、レジストリセクション\]**を**<em>追加</em>します...  
新しくインストールされたサービスに関連するレジストリ情報が設定されている、1つまたは複数の INF ライターで定義された*レジストリセクション*を参照します。 このような*add registry セクション*の**hkr**仕様では、 **HKLM\\System\\CurrentControlSet\\Services\\ServiceName**レジストリキーが指定されています。 詳細については、「 [**INF AddReg ディレクティブ**](inf-addreg-directive.md)」を参照してください。

このディレクティブは、サービスのインストールセクションではほとんど使用されません。

<a href="" id="delreg-del-registry-section--del-registry-section----"></a>**Delreg**=*del-registry-section*\[ **、** <em>del-section</em>\]...  
既にインストールされているサービスに関連するレジストリ情報が削除される、1つまたは複数の INF ライター定義の*del キーセクション*を参照します。 このような CurrentControlSet*セクション*の**hkr**仕様では、 **HKLM\\System\\\\Services\\ServiceName**レジストリキーが指定されています。 詳細については、「 [**INF DelReg ディレクティブ**](inf-delreg-directive.md)」を参照してください。

このディレクティブは、ほとんどの場合、*サービスのインストールセクション*では使用されませんが、同じデバイス/ドライバーサービスの以前のインストールのためにレジストリを "更新" する INF で使用されることがあります。

<a href="" id="bitreg-bit-registry-section--bit-registry-section----"></a>**Bitreg**=*ビットレジストリ-セクション*\[ **、** <em>ビットレジストリ-セクション</em>\]...  
は、サービスの*インストールセクション*では有効ですが、ほとんど使用されません。 また、このような*ビットレジストリセクション*の**hkr**仕様では、 **HKLM\\System\\CurrentControlSet\\Services\\ServiceName**レジストリキーも指定されています。

<a href="" id="loadordergroup-load-order-group-name"></a>**Loadordergroup**=の*読み込み順序-グループ名*  
この省略可能なエントリは、このドライバーがメンバーとなっている読み込み順序グループを識別します。 **SCSI**クラスや**NDIS**など、"標準" の読み込み順序グループのいずれかになります。

通常、このエントリは、WDM ドライバーを使用しているデバイスや、そのようなグループにレガシ依存関係がない限り、PnP デバイス専用のデバイスには必要ありません。 ただし、このエントリは、特定の順序でドライバーのグループを読み込むことによって、デバイスの検出がサポートされている場合に便利です。

**Loadordergroup**の詳細については、「[ドライバーの読み込み順序の指定](specifying-driver-load-order.md)」を参照してください。

<a href="" id="dependencies-depend-on-item-name--depend-on-item-name----"></a>依存**関係**=に依存しています-*名前*\[ **、** <em>依存している項目名</em>\]...  
依存関係の一覧にあるそれぞれの*項目に依存する名前*の項目は、デバイスまたはドライバーが依存するサービスまたは負荷順序グループの名前を指定します。

依存し*ている項目名*がサービスを指定している場合は、このドライバーを開始する前に実行する必要があるサービスを指定します。 たとえば、システムによって提供される Win32 TCP/IP 印刷サービスの INF は、基盤となる (カーネルモードの) TCP/IP トランスポートスタックのサポートに依存します。 その結果、TCP/IP 印刷サービスの INF は、このエントリを**依存関係 = TCPIP**として指定します。

依存する-*項目名*は、このデバイス/ドライバーが依存している読み込み順序グループを指定できます。 このようなドライバーは、指定したグループの少なくとも1つのメンバーが開始された場合にのみ開始されます。 グループ名の前にプラス記号 (+) を付けます。 たとえば、システム RAS サービス INF には、負荷順序グループとサービスの両方を一覧表示する**Dependencies = + NetBIOSGroup の**ようなエントリが含まれている場合があります。

<a href="" id="security--security-descriptor-string-"></a>**Security**= "*セキュリティ記述子-文字列*"  
サービスに適用されるセキュリティ記述子を指定します。 このセキュリティ記述子は、サービスの開始、停止、構成などの操作を実行するために必要なアクセス許可を指定します。 *セキュリティ記述子文字列*の値は、DACL (**D:** ) セキュリティコンポーネントを示すトークンを含む文字列です。

セキュリティ記述子の文字列の詳細については、「[セキュリティ記述子定義言語 (Windows)](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)」を参照してください。 セキュリティ記述子文字列の形式の詳細については、「セキュリティ記述子定義言語 (Windows)」を参照してください。

セキュリティ記述子を指定する方法の詳細については、「セキュリティ[で保護されたデバイスのインストールの作成](creating-secure-device-installations.md)」を参照してください。

### <a name="specifying-driver-load-order"></a>ドライバーの読み込み順序の指定

オペレーティングシステムは、次のように、*サービスのインストールセクション*の  **starttype**値に従ってドライバーを読み込みます。

-   システムブートの開始段階では、オペレーティングシステムはすべての**0x0** (SERVICE_BOOT_START) ドライバーを読み込みます。
-   システムの開始フェーズでは、オペレーティングシステムはまず、PnP マネージャーがレジストリ内のデバイスノード (*devnodes*) を検出するすべての WDM および pnp ドライバーを読み込み**ます。\\列挙**ツリー (INF ファイルで、SERVICE_DEMAND_START の SERVICE_SYSTEM_START または**0x03**に**0x01**が指定されているかどうか)。その後、オペレーティングシステムは、残りのすべての SERVICE_SYSTEM_START ドライバーを読み込みます。
-   システムの自動開始フェーズでは、オペレーティングシステムによって残りのすべての SERVICE_AUTO_START ドライバーが読み込まれます。

**依存関係**の詳細については、「[ドライバーの読み込み順序の指定](specifying-driver-load-order.md)」を参照してください。

### <a name="promoting-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>ブート時にドライバーの StartType を昇格する (ブートシナリオに応じて)

ブートシナリオに応じて、 **Bootflags**レジストリ値を使用して、オペレーティングシステムがドライバーの**starttype**値を 0x0 (SERVICE_BOOT_START) に昇格するタイミングを制御できます。 16進数値として表現される次の数値の1つ以上 (論理和) を指定できます。

-   0x1 (CM_SERVICE_NETWORK_BOOT_LOAD) ネットワークから起動する場合は、ドライバーを昇格させる必要があることを示します。

-   0x2 (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD) VHD から起動する場合は、ドライバーを昇格する必要があることを示します。

-   0x4 (CM_SERVICE_USB_DISK_BOOT_LOAD) USB ディスクから起動する場合は、ドライバーをに昇格させる必要があることを示します。

-   0x8 (CM_SERVICE_SD_DISK_BOOT_LOAD) SD ストレージから起動した場合、ドライバーを昇格させる必要があることを示します。

-   0x10 (CM_SERVICE_USB3_DISK_BOOT_LOAD) は、USB 3.0 コントローラー上のディスクから起動する場合に、ドライバーを昇格させる必要があることを示します。

-   0x20 (CM_SERVICE_MEASURED_BOOT_LOAD) は、測定されたブートが有効になっているときに起動時にドライバーを昇格させる必要があることを示します。

-   0x40 (CM_SERVICE_VERIFIER_BOOT_LOAD) は、検証ツールの起動が有効になっている場合にドライバーを昇格させる必要があることを示します。

-   0x80 (CM_SERVICE_WINPE_BOOT_LOAD) は、WinPE を起動した場合にドライバーを昇格させる必要があることを示します。

*Service-install セクション*には、次の一般的な形式があります。

```ini
[service-install-section]
AddReg=add-registry-section
...

[add-registry-section]
HKR,,BootFlags,0x00010003,0x14 ; CM_SERVICE_USB3_DISK_BOOT_LOAD|CM_SERVICE_USB_DISK_BOOT_LOAD
```

### <a name="registering-for-event-logging"></a>イベントログの登録

また、 **Addservice**ディレクティブは、INF ファイル内の他の場所で、*イベントログのインストールセクション*を参照することもできます。 各セクションには、次の形式があります。

```ini
[event-log-install-section]
 
AddReg=add-registry-section[, add-registry-section]... 
[DelReg=del-registry-section[, del-registry-section]...] 
[BitReg=bit-registry-section[,bit-registry-section]...]
 ...
```

一般的なデバイス/ドライバーの INF ファイルの場合、 **AddReg**ディレクティブのみを使用してドライバーのイベントログメッセージファイルを*設定します*。 **CurrentControlSet\\Services\\EventLog\\** <em>EventLogType</em> **\\** <em>EventName</em>レジストリキー*を指定する*と、によって、\\System の\\HKLM **r**仕様が指定されます。 このイベントログの*追加-セクション*には、次の一般的な形式があります。

```ini
[drivername_EventLog_AddReg]
HKR,,EventMessageFile,0x00020000,"path\IoLogMsg.dll;path\driver.sys"
HKR,,TypesSupported,0x00010001,7 
```

特に、次のように、デバイス/ドライバー用に作成されたレジストリサブキーに2つの値エントリを追加します。

-   **EventMessageFile**という名前の値のエントリは、FLG_ADDREG_TYPE_EXPAND_SZ 値の**0x00020000**によって指定された[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型です。 二重引用符 (") で囲まれた値は、システムによって提供される*Iologmsg .dll*を関連付けます (ただし、別のログ dll に関連付けることもできます)。 通常、これらの各ファイルへのパスは次のように指定されます。

    *%%SystemRoot%%\\System32\\IoLogMsg.dll*

    *%%SystemRoot%%\\System32\\drivers\\driver.sys*

-   **サポートさ**れている名前付きの値のエントリは、FLG_ADDREG_TYPE_DWORD 値**0x00010001**で指定されている[REG_DWORD](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型です。

    ドライバーの場合、この値は**7**にする必要があります。 この値は、EVENTLOG_SUCCESS、EVENTLOG_ERROR_TYPE、EVENTLOG_WARNING_TYPE、および EVENTLOG_INFORMATION_TYPE のビットごとの OR に相当します。これは、EVENTLOG_AUDIT_*XXX*ビットを設定する必要はありません。

また、ドライバーバイナリが新しくインストールされたドライバーによって置き換えられている場合は、既存の**EventMessageFile**と**タイプがサポートさ**れている値のエントリを明示的に削除することによって、以前にインストールされたイベントログメッセージファイルを削除するために、 [**delreg**](inf-delreg-directive.md)ディレクティブを使用すること*もできます*。 (「 [**INF DelService ディレクティブ**](inf-delservice-directive.md)」も参照してください)。

[**Bitreg**](inf-bitreg-directive.md)ディレクティブは、INF ライターで定義された*イベントログのインストール*-*セクション*内でも有効ですが、デバイスドライバーのイベントログの標準値のエントリはビットマスクではないため、ほとんど使用されません。

<a name="examples"></a>例
--------

この例では、 **Addservice**ディレクティブによって参照される、 [*ddinstall * の例で既に示したように、サービスインストールセクションとイベントログインストールセクションを示し**ます。サービス**](inf-ddinstall-services-section.md)。

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

[*Ddinstall * のリファレンスの例 **。** ](inf-ddinstall-hw-section.md)前に説明した HW セクションでは、PnP 上位フィルタードライバーを設定するために**addservice**ディレクティブによって参照されるサービスインストールセクションも表示されます。

## <a name="see-also"></a>関連項目


[**AddReg**](inf-addreg-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[* **DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[* **DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**DelReg**](inf-delreg-directive.md)

[**DelService**](inf-delservice-directive.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**Strings**](inf-strings-section.md)

 

 







---
title: INF AddEventProvider ディレクティブ
author: andylsn
description: AddEventProvider ディレクティブは、INF DDInstall. Events セクション内で使用されます。
ms.assetid: ''
keywords:
- INF AddEventProvider ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddEventProvider Directive
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2e3f64d893db57f32182aa9cd14bf015d3fd8547
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223188"
---
# <a name="inf-addeventprovider-directive"></a>INF AddEventProvider ディレクティブ

**AddEventProvider**ディレクティブは、 [**INF *ddinstall*内で使用されます。イベントセクション**](inf-ddinstall-services-section.md)。 ドライバーに関連付けられている[Windows イベントトレーシング](https://docs.microsoft.com/windows/desktop/ETW/about-event-tracing)(ETW) プロバイダーの特性を指定します。 このディレクティブは、Windows 10 バージョン1809以降でサポートされています。

```inf
[DDInstall.Events] 

AddEventProvider={ProviderGUID},event-provider-install-section
...
```

## <a name="entries"></a>エントリ


<a href="" id="ProviderGUID"></a>*ProviderGUID*  
プロバイダーを識別する GUID 値を指定します。 これは、形式`{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}`の明示的な GUID 値として、または INF ファイルの[**文字列**](inf-strings-section.md)セクションで`{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}`に定義された% strkey% token として表すことができます。

<a href="" id="event-provider-install-section"></a>*イベントプロバイダー-インストール-セクション*  
は、このデバイス (またはデバイス) のプロバイダーを登録するための情報を含む、INF ライターで定義されたセクションを参照します。 詳細については、次の「**解説**」を参照してください。

<a name="remarks"></a>解説
-------

システム定義および大文字と小文字を区別しない拡張機能は、 <em>Ddinstall</em>に挿入でき**ます。** クロスオペレーティングシステムまたはクロスプラットフォームの INF ファイルの**AddEventProvider**ディレクティブを含む Events セクション。プラットフォーム固有または OS 固有のインストールを指定します。

各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**AddEventProvider**ディレクティブは、INF ファイル内の別の場所にある、名前付きの*イベントプロバイダーのインストールセクション*を参照する必要があります。 各セクションには、次の形式があります。

```inf
[event-provider-install-section]
 
ProviderName=name
ResourceFile=path-to-file
[MessageFile=path-to-file]
[ParameterFile=path-to-file]
(ImportChannel=channel-name) |
(AddChannel=channel-name,channel-type[,channel-install-section])
...
```

各 ResourceFile*には*、 **ProviderName**と**ResourceFile**を指定する必要があります。 必要に応じて、 **importchannel**と**addchannel**の任意の組み合わせを使用して、プロバイダーのチャネルの一覧を個別の行に指定します。 INF ファイルのチャネルリストの詳細については、以下の「[**チャネルリストの指定**](#specifying-a-channel-list)」を参照してください。 [Windows イベントログ](https://docs.microsoft.com/windows/desktop/WES/windows-event-log)のチャネルの詳細については、「[チャネルの定義](https://docs.microsoft.com/windows/desktop/WES/defining-channels)」を参照してください。

### <a name="event-provider-install-section-entries-and-values"></a>イベントプロバイダー-インストールセクションのエントリと値

<a href="" id="providername-name"></a>**ProviderName**=*名*  
プロバイダーの名前を指定します。 名前は255文字以内にする必要があり、文字 ' > '、' < '、' & '、' "'、' | '、'\'、': '、' ' '、'? '、' * '、または ASCII 値が31未満の文字を含めることはできません。 また、ファイル名とレジストリキー名の一般的な制約に従う必要があります。 これらの制約については[、「ファイルの名前付け](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file)と[レジストリ要素のサイズの制限](https://docs.microsoft.com/windows/desktop/SysInfo/registry-element-size-limits)」を参照してください。

<a href="" id="resourcefile-path-to-file"></a>**ResourceFile**=*ファイルへのパス*  
%Dirid%\filename. として表現される、プロバイダーのメタデータリソースを含む exe または dll へのパスを指定します。

*Dirid*番号は、カスタムディレクトリ識別子、または「 [Dirid の使用](using-dirids.md)」で説明されているシステム定義のディレクトリ識別子のいずれかです。

<a href="" id="messagefile-path-to-file"></a>**MessageFile**=*ファイルへのパス*  
必要に応じて、プロバイダーのローカライズされたメッセージリソースを含む exe または dll へのパスを%dirid%\filename. として指定します。

<a href="" id="parameterfile-path-to-file"></a>**Parameterfile**=*パスからファイルへ*  
必要に応じて、プロバイダーのパラメーター文字列リソース (%dirid%\filename.) を含む exe または dll へのパスを指定します。

<a href="" id="importchannel-channel-name"></a>**Importchannel**=*channel-name*  
必要に応じて、別のプロバイダーによって定義されたチャネルを指定します。 詳細については、次を参照してください。**チャネルリスト**セクションを指定します。

<a href="" id="addchannel-channel-name-channel-type--channel-install-section-"></a>**Addchannel**=*channel-name*、*channel type*\[、*channel-install-section*\]  
オプションで、inf ファイル内の他の場所にある INF ライターで定義されたチャネルのインストールセクションを参照する、サブディレクティブを含むチャネルを指定します。 詳細については、次を参照してください。**チャネルリスト**セクションを指定します。

### <a name="specifying-a-channel-list"></a>チャネルリストの指定

プロバイダーのチャネルの一覧は、そのイベントプロバイダーの [*インストール] セクション*で指定できます。 チャネルをインポートしたり、一覧にチャネルを追加したりできます。これらのチャネルの順序は保持されます。 詳細については、「[チャネルの定義](https://docs.microsoft.com/windows/desktop/WES/defining-channels)」を参照してください。

*チャネル名*は、プロバイダーが使用するチャネルのリスト内で一意である必要があります。 *チャネル名*は255文字未満にする必要があり、次の文字を含めることはできません: ' > '、' < '、' & '、' "'\'、' | '、'、': '、' ' '、'? '、' * '、または ASCII 値が31未満の文字を含めることはできません。

*チャネルの種類*は、次の一覧に示すように、10進表記またはのいずれかの数値として指定できます。

<a href="" id="0x1--admin-"></a>**0x1** (管理者)  
管理タイプチャネルは、エンドユーザー、管理者、およびサポート担当者を対象とするイベントをサポートします。 管理チャネルに書き込まれるイベントには、管理者が操作できる適切に定義されたソリューションが必要です。

<a href="" id="0x2--operational-"></a>**0x2** (操作)  
動作の種類のチャネルは、問題や発生の分析と診断に使用されるイベントをサポートします。 問題や事象に応じたツールまたはタスクを起動する目的で使用できます。

<a href="" id="0x3--analytic-"></a>**0x3** (分析)  
分析タイプチャネルは、大量に発行されるイベントをサポートします。 これらは、プログラム操作を記述し、ユーザーの介入によって処理できない問題を示しています。

<a href="" id="0x4--debug-"></a>**0x4** (デバッグ)  
デバッグ型チャネルは、開発者がデバッグの問題を診断するためにのみ使用するイベントをサポートしています。

また、 **addchannel**サブディレクティブは、INF ファイル内の他の場所で*チャネルのインストールセクション*を参照することもできます。 各セクションには、次の形式があります。

```inf
[channel-install-section]

[Isolation=isolation-type]
[Access=access-string]
[Enabled=0|1]
[Value=value]
[LoggingMaxSize=max-size]
[LoggingRetention=retention-type]
[LoggingAutoBackup=0|1]
```

チャネル属性の詳細については、「 [Eventmanifest スキーマ](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-schema)内で定義されている[channeltype](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-channeltype-complextype) 」を参照してください。

### <a name="channel-install-section-entries-and-values"></a>Channel-Install セクションのエントリと値

<a href="" id="isolation-isolation-type"></a>**分離**=*分離-型*  
必要に応じて、次の一覧に示すように、10進表記またはのいずれかの数値として、チャネルの既定のアクセス許可を指定します。 省略した場合、既定値は**0x1** (アプリケーション) になります。

<a href="" id="0x1--application-"></a>**0x1** (アプリケーション)  

<a href="" id="0x2--system-"></a>**0x2** (システム)  

<a href="" id="0x3--Custom-"></a>**0x3** (カスタム)  

<a href="" id="access-access-string"></a>**アクセス**=*のアクセス-文字列*  
必要に応じて、チャネルをバックするログファイルへのアクセスを制御する[セキュリティ記述子定義言語](https://docs.microsoft.com/windows/desktop/SecAuthZ/security-descriptor-definition-language)(SDDL) アクセス記述子を指定します。

**分離**が**0x1** (アプリケーション) または**0x2** (システム) に設定されている場合、この文字列はファイルへの読み取りアクセスを制御します (書き込みアクセス許可は無視されます)。また、分離属性が**0x3** (カスタム) に設定されている場合は、チャネルへの書き込みアクセスと、ファイルへの読み取りアクセスを制御します。

<a href="" id="enabled-0-1"></a>**Enabled**=**0 | 1**  
必要に応じて、チャネルを有効にするかどうかを指定します。 省略した場合、既定値は 0 (無効) になります。

**0x3** (分析) と**0x4** (デバッグ) の*チャネルの種類*は大量のチャネルであるため、そのチャネルに書き込むコンポーネントの問題を調査する場合にのみ、 **Enabled**を1に設定する必要があります。 **0x3** (分析) および**0x4** (デバッグ) チャネルを有効にするたびに、サービスはチャネルからイベントをクリアします。

<a href="" id="value-value"></a>**値**=の*値*  
必要に応じて、プロバイダーが定義するチャネルのリスト内でチャネルを一意に識別する数値識別子を指定します。

<a href="" id="loggingmaxsize-max-size"></a>**ログイン maxsize**=*最大サイズ*  
必要に応じて、ログファイルの最大サイズをバイト単位で指定します。 既定値 (および最小値) は 1 MB です。

<a href="" id="loggingretention-retention-type"></a>**ログイン保有**=期間*の種類*  
必要に応じて、ログファイルが**0x1** (円形) と**0x2** (シーケンシャル) のどちらであるかを指定します。 既定値**は 0x1 (** 管理者) と**0x2** (操作)*チャネルタイプ*、および**0x3** **(分析**) および**0x4** (デバッグ)*チャネル型*の場合は、 **0x1** (円形) です。

<a href="" id="loggingautobackup-0-1"></a>**ログインの自動バックアップ**=**0 | 1**  
必要に応じて、現在のログファイルが最大サイズに達したときに新しいログファイルを作成するかどうかを指定します。 ログファイルが最大サイズに達したときにサービスによって新しいファイルが作成されるように要求するには、1に設定します。それ以外の場合は0です。 [ログインのリテンション期間] を**1 に設定**できるのは、[**ログインの保有期間**] が**0x2** (シーケンシャル) に設定されていて、かつ**0x1** (管理者) と**0x2** (操作) の*チャネルの種類*に対してのみです。

<a name="examples"></a>例
--------

この例では、「 **AddEventProvider** [ *ddinstall *」の例で既に説明したように、AddEventProvider ディレクティブによって参照されるイベントプロバイダーのインストールセクションを示します。イベント](inf-ddinstall-events-section.md)。

```inf
[foo_Event_Provider_Inst]
ProviderName  = FooCollector
ResourceFile  = %13%\FooResource.dll
MessageFile   = %13%\FooMessage.exe

[bar_Event_Provider_Inst]
ProviderName  = BarCollector
ResourceFile  = %13%\BarResource.exe
MessageFile   = %13%\BarMessage.dll
ParameterFile = %13%\BarParameter.dll
ImportChannel = Microsoft-Windows-BaseProvider/Admin
AddChannel    = Bar-Provider/Admin,0x1,bar_Channel2_Inst    ; Admin type
ImportChannel = Microsoft-Windows-BaseProvider/Operational
ImportChannel = Microsoft-Windows-SampleProvider/Admin
AddChannel    = Bar-Provider/Debug,0x4                      ; Debug type

[bar_Channel2_Inst]
Isolation         = 2                                       ; System isolation
Enabled           = 1
Value             = 17
LoggingMaxSize    = 20971520
LoggingRetention  = 2                                       ; Sequential
LoggingAutoBackup = 1
```

## <a name="see-also"></a>関連項目


[***DDInstall *。記録**](inf-ddinstall-events-section.md)

 

 






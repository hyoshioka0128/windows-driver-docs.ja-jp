---
title: INF AddEventProvider ディレクティブ
author: andylsn
description: AddEventProvider ディレクティブは、INF DDInstall.Events セクション内で使用されます。
ms.assetid: ''
keywords:
- INF AddEventProvider ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddEventProvider Directive
api_type:
- NA
ms.date: 06/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 797705e2c6ade14f4a9c6b641f5b6ccc164deb53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531627"
---
# <a name="inf-addeventprovider-directive"></a>INF AddEventProvider ディレクティブ

**AddEventProvider**内ディレクティブの使用、 [ **INF *DDInstall*します。[イベント] セクション**](inf-ddinstall-services-section.md)します。 特性を指定します、 [Windows のイベント トレース](https://msdn.microsoft.com/library/windows/desktop/aa363668)ドライバーに関連付けられている (ETW) プロバイダーです。 このディレクティブは 1809 およびそれ以降のバージョンの Windows 10 のサポートします。

```ini
[DDInstall.Events] 

AddEventProvider={ProviderGUID},event-provider-install-section
...
```

## <a name="entries"></a>エントリ


<a href="" id="ProviderGUID"></a>*ProviderGUID*  
プロバイダーを識別する GUID 値を指定します。 これは、フォームの明示的な GUID 値として表現できます`{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}`を %strkey% トークンが定義されているまたは`{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}`で、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

<a href="" id="event-provider-install-section"></a>*event-provider-install-section*  
このデバイス (またはデバイス) のプロバイダーを登録するための情報を含む INF ライター定義のセクションを参照します。 詳細については、次を参照してください。**解説**セクション。

<a name="remarks"></a>注釈
-------

システム定義の大文字と拡張機能を挿入できる、 <em>DDInstall</em>**します。イベント**を含むセクション、 **AddEventProvider**クロス オペレーティング システムやクロス プラットフォーム INF ファイルでプラットフォーム固有または OS 固有のインストールを指定するディレクティブ。

各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

**AddEventProvider**ディレクティブは名前付き参照する必要があります*イベント プロバイダーのインストール セクション*INF ファイルで別の場所。 このような各セクションでは、次の形式があります。

```ini
[event-provider-install-section]
 
ProviderName=name
ResourceFile=path-to-file
[MessageFile=path-to-file]
[ParameterFile=path-to-file]
(ImportChannel=channel-name) |
(AddChannel=channel-name,channel-type[,channel-install-section])
...
```

各*イベント プロバイダーのインストール セクション*提供する必要があります**ProviderName**と**ResourceFile**します。 必要に応じて、チャネルのリストを指定の任意の組み合わせを使用して、プロバイダーの**ImportChannel(s)** と**AddChannel(s)**、それぞれ別々 の行にします。 INF ファイルでチャネルのリストの詳細については、次を参照してください。 [**チャネルの一覧を指定する**](#specifying-a-channel-list)以下。 詳細については[Windows イベント ログ](https://msdn.microsoft.com/library/windows/desktop/aa385780)チャネルを参照してください[定義チャネル](https://msdn.microsoft.com/library/windows/desktop/dd996911)します。

### <a name="event-provider-install-section-entries-and-values"></a>イベント プロバイダーのインストール」セクションのエントリと値

<a href="" id="providername-name"></a>**ProviderName**=*name*  
プロバイダーの名前を指定します。 名前が 255 文字より長くすることはできず、文字を含めることはできません: ' >'、' <'、'&'、'"'、' | '、'\'、':'、' '、'?'、' *'、値より小さい 31 の ascii 文字またはします。 さらに、名前はファイルおよびレジストリのキー名の一般的な制約に従う必要があります。 これらの制約をご覧[Naming a File](https://msdn.microsoft.com/library/windows/desktop/aa365247)と[レジストリ要素のサイズ制限](https://msdn.microsoft.com/library/windows/desktop/ms724872)します。

<a href="" id="resourcefile-path-to-file"></a>**ResourceFile**=*ファイルへのパス*  
Exe または %dirid%\filename で表される、プロバイダーのメタデータ リソースが含まれている dll へのパスを指定します。

*Dirid*数は、カスタム ディレクトリの識別子またはで説明されているディレクトリのシステム定義の識別子のいずれかのいずれか[を使用して Dirids](using-dirids.md)します。

<a href="" id="messagefile-path-to-file"></a>**コード**=*ファイルへのパス*  
必要に応じて、ローカライズされたメッセージ リソース、%dirid%\filename で表したの exe または dll を含む、プロバイダーへのパスを指定します。

<a href="" id="parameterfile-path-to-file"></a>**ParameterFile**=*path-to-file*  
必要に応じて、exe または %dirid%\filename で表される、プロバイダーのパラメーターの文字列リソースを含む dll へのパスを指定します。

<a href="" id="importchannel-channel-name"></a>**ImportChannel**=*チャネル名*  
必要に応じて別のプロバイダーによって定義されているチャネルを指定します。 詳細については、次を参照してください。**チャネルの一覧を指定する**セクション。

<a href="" id="addchannel-channel-name-channel-type--channel-install-section-"></a>**AddChannel**=*channel-name*,*channel-type*\[,*channel-install-section*\]  
必要に応じて、INF ライター定義チャネルのインストール-セクション INF ファイルで別の場所を参照するサブ ディレクティブでチャネルを指定します。 詳細については、次を参照してください。**チャネルの一覧を指定する**セクション。

### <a name="specifying-a-channel-list"></a>チャネルの一覧を指定します。

チャネルの一覧を指定するには、プロバイダー内の*イベント プロバイダーのインストール セクション*します。 チャネルをインポートしたり、チャネルを一覧に追加され、これらのチャネルの順序が保持されます。 詳細については、[定義チャネル](https://msdn.microsoft.com/library/windows/desktop/dd996911)を参照してください。

*チャネル名*プロバイダーで使用されるチャネルのリスト内で一意である必要があります。 *チャネル名*255 文字未満にする必要があり、次の文字を含めることはできません: ' >'、' <'、'&'、'"'、' | '、'\'、':'、' '、'?'、' *'、値より小さい 31 の ascii 文字またはします。

*チャネル型*10 進数のいずれかで表される、次の数値値の 1 つとして、16 進数表記で、次の一覧に示すように指定することができます。

<a href="" id="0x1--admin-"></a>**0x1** (管理者)  
管理の種類のチャネルをターゲットのエンド ユーザー、管理者、イベントをサポートしている担当者をサポートします。 管理チャネルに書き込まれたイベントは、管理者が機能する明確な解決策が必要です。

<a href="" id="0x2--operational-"></a>**0x2** (操作)  
操作の型のチャネルでは、分析と問題や事象を診断に使用されるイベントをサポートします。 これらは、問題や事象に応じたツールまたはタスクをトリガーする使用できます。

<a href="" id="0x3--analytic-"></a>**0x3** (分析)  
分析の種類のチャネルでは、大量に公開されるイベントをサポートします。 プログラムの操作を記述され、ユーザーの介入によって処理できない問題を示します。

<a href="" id="0x4--debug-"></a>**0x4** (デバッグ)  
デバッグの問題を診断する開発者だけで使用される型のチャネル サポート イベントをデバッグします。

**AddChannel**サブ ディレクティブを参照できます、*チャネル-section インストール*INF ファイルで別の場所。 このような各セクションでは、次の形式があります。

```ini
[channel-install-section]

[Isolation=isolation-type]
[Access=access-string]
[Enabled=0|1]
[Value=value]
[LoggingMaxSize=max-size]
[LoggingRetention=retention-type]
[LoggingAutoBackup=0|1]
```

チャネルの属性の詳細については、[チャネル](https://msdn.microsoft.com/library/windows/desktop/aa382741)内で定義された[EventManifest スキーマ](https://msdn.microsoft.com/library/windows/desktop/aa384043)を参照してください。

### <a name="channel-install-section-entries-and-values"></a>チャネル インストール セクションのエントリと値

<a href="" id="isolation-isolation-type"></a>**分離**=*分離型*  
10 進数のいずれかで表される、次の数値値の 1 つとして、16 進数表記で、次の一覧に示すように必要に応じて、チャネルの既定のアクセス許可を指定します。 省略した場合、既定値は**0x1** (アプリケーション)。

<a href="" id="0x1--application-"></a>**0x1** (アプリケーション)  

<a href="" id="0x2--system-"></a>**0x2** (システム)  

<a href="" id="0x3--Custom-"></a>**0x3** (カスタム)  

<a href="" id="access-access-string"></a>**アクセス**=*アクセス文字列*  
オプションを指定します、[セキュリティ記述子定義言語](https://msdn.microsoft.com/library/windows/desktop/aa379567)(SDDL) へのアクセスの記述子がチャネルをサポートするログ ファイルへのアクセスを制御します。

場合、この文字列は (書き込みアクセス許可は無視されます)、ファイルへの読み取りアクセスを制御、**分離**に設定されている**0x1** (アプリケーション) または**0x2** (システム) 中、制御チャネルと分離属性に設定されている場合は、ファイルへの読み取りアクセスに対する書き込みアクセス**0x3** (カスタム)。

<a href="" id="enabled-0-1"></a>**有効になっている**=**0 | 1**  
必要に応じて、チャネルが有効になっているかどうかを指定します。 省略した場合、既定値は 0 (無効)。

**0x3** (分析) と**0x4** (デバッグ)*チャネル型*高ボリュームのチャネルを設定する必要があります、**有効**1 の場合にのみにそのチャネルへの書き込みをコンポーネントの問題を調査します。 有効にするたび、 **0x3** (分析) と**0x4** (デバッグ) チャネル、サービスがチャネルからイベントを消去します。

<a href="" id="value-value"></a>**値**=*値*  
必要に応じて、プロバイダーを定義するチャネルのリスト内でチャネルを一意に識別する数値識別子を指定します。

<a href="" id="loggingmaxsize-max-size"></a>**LoggingMaxSize**=*max-size*  
必要に応じて、ログ ファイルのバイト単位で最大のサイズを指定します。 既定 (および最小値) の値は、1 MB です。

<a href="" id="loggingretention-retention-type"></a>**LoggingRetention**=*保有期間の種類*  
必要に応じて、ログ ファイルにはあるかどうかを指定します**0x1** (円形) または**0x2** (連続)。 既定値は**0x1** (円形) を**0x1** (Admin) と**0x2** (操作)*チャネル型*と**0x2**(シーケンシャル) の**0x3** (分析) と**0x4** (デバッグ)*チャネル型*します。

<a href="" id="loggingautobackup-0-1"></a>**LoggingAutoBackup**=**0 | 1**  
必要に応じて現在のログ ファイルが最大サイズに達したときに、新しいログ ファイルを作成するかどうかを指定します。 1 に設定すると、ログ ファイルが最大サイズに達すると、サービスが新しいファイルを作成するよう依頼それ以外の場合、0 を返します。 設定することができます、 **LoggingAutoBackup** 1 の場合にのみに、 **LoggingRetention**に設定されている**0x2** (シーケンシャル) に対してのみ**0x1** (Admin) と**0x2** (操作)*チャネル型*します。

<a name="examples"></a>例
--------

この例で参照されているイベント プロバイダーのインストールのセクションでは、 **AddEventProvider**ディレクティブの例では、前半で既に示した[ * **DDInstall *。イベント**](inf-ddinstall-events-section.md)します。

```ini
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


[***DDInstall *。イベント**](inf-ddinstall-events-section.md)

 

 






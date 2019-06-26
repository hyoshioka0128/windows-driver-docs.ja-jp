---
title: チェックされているオペレーティング システムと HAL だけをインストールします。
description: チェック済みのオペレーティング システムと HAL のみのインストール (Windows Vista 以降)
ms.assetid: 1203b7cd-50b9-4174-8bec-112019444fac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a8f2c3e7d7735d63ab8747767c7009fbef4f423
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354796"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-vista-and-later"></a>チェック済みのオペレーティング システムと HAL のみのインストール (Windows Vista 以降)


完了チェック ビルドは、コンピューターにインストールではなく、システムの無料のビルドをインストールし、チェックされているバージョンのオペレーティング システム イメージとハードウェア アブストラクション レイヤー (HAL) をインストールできます。 この手順を使用する場合は、2 つのブート オプションを提供するためにブート ローダーを構成できます。 無料のビルドでは、1 つのブート オプションで十分です。 2 番目のブート オプションは、チェックされているオペレーティング システム イメージと HAL を使用してシステムを起動が、その他のすべてのシステム コンポーネントの無料版を使用します。

## <a name="step-1---identifying-the-files-to-install-for-windows-vista-and-later"></a>手順 1 - Windows Vista 以降のインストール ファイルを識別します。

部分的なチェック ビルドをインストールする前に、オペレーティング システム イメージと HAL ファイル システムに無料のビルドをインストールするために使用されたのバージョンを確認する必要があります。

**ヒント:**   の 64 ビット バージョンの Windows Vista 以降では、このプロセスは簡単です。 ある場合、 [Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/)、オペレーティング システム イメージと HAL ファイル デバッグからを使用する\\WDK のディレクトリ。 参照してください[チェック ビルドをインストールする](installing-the-checked-build.md)します。 各 amd64 または ia64 が対象の 1 つだけのバージョンがあります。 ファイルの名前は、ntkrnlmp.exe と Hal.dll です。 使用している Windows のバージョンの WDK があれば、進んでに[手順 2。チェックされたファイルをコピー](#step-2---copying-the-checked-files)します。

 

Windows の 32 ビット バージョンを実行するコンピューターでは、コピーするのにファイルの名前を識別するために、次の手順を使用します。

### <a name="determining-the-name-of-the-hal-that-is-installed"></a>インストールされている HAL の名前を決定します。

1.  開くファイルの %systemroot%\\Inf\\setupapi.dev.log して hal.dll を検索します。

    TargetFilename のような行を検索する必要があります 'hal.dll'

2.  対応するログ ファイルの同じセクションで探します*SourceFilename*します。 名前の右側に*SourceFilename*チェック ビルドからコピーする必要のある HAL ファイルの名前を指定します。

次の例は setupapi.dev.log ファイルです。 *SourceFilename*が表示されます。

```
{FILE_QUEUE_COPY}
   CopyStyle      - 0x09180000
   SourceRootPath - 'C:\Windows\System32\DriverStore\FileRepository\hal.inf_0c52392f'
   SourceFilename - 'halmacpi.dll'
   TargetDirectory- 'C:\Windows\system32'
   TargetFilename - 'hal.dll'
   SourceDesc     - 'windows cd'
{FILE_QUEUE_COPY exit(0x00000000)}
```

### <a name="determining-the-name-of-the-operating-system-image-file-installed"></a>インストールされているオペレーティング システム イメージ ファイルの名前を決定します。

64 ビット バージョンの Windows Vista 以降では、ファイルの名前は ntkrnlmp.exe します。

32 ビット バージョンの Windows Vista では、ユニプロセッサまたはマルチプロセッサのバージョンがインストールされているかどうかを確認するのに、次の手順を使用することができます。

1.  コンピューターの管理コンソール (compmgmt.msc) では、イベント ビューアーを開きます。

2.  システム ログでイベント ID 6009 を検索します。

    このイベントのプロパティでは、1 つのプロセッサまたはインストールされているオペレーティング システム イメージのマルチプロセッサのバージョンがあるかどうかを示します。

たとえばの次とは、フリー ビルド マルチプロセッサ対応のオペレーティング システムのことを示します。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Free.
```

プロセッサの種類と、コンピューターにインストールされている物理メモリの量を把握する場合は、次のいずれかから、イメージの名前を選択できます。 カーネル デバッガーがアタッチされている場合は、使用することも、 **lmv mnt**元のファイル名を識別するためにコマンド。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB の物理メモリをユニプロセッサ x86 アーキテクチャ システム。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa.exe  
PAE サポート ユニプロセッサ x86 アーキテクチャ システム。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp.exe  
4 GB の物理メモリをマルチプロセッサの x86 アーキテクチャ システム。

<span id="NTKRPAMP.EXE"></span>ntkrpamp.exe  
PAE のサポートしているマルチプロセッサの x86 アーキテクチャ システム。

## <a name="step-2---copying-the-checked-files"></a>手順 2 - チェックされているファイルのコピー

システムのインストール中に使用されていたファイルの名前がわかったら、システムにこれらのファイルの検証済みのバージョンをコピーできます。 WDK のデバッグ ディレクトリにまたは、チェックされている配布キットでは、指定したファイルを検索します。 %Systemroot% にこれらのファイルをコピー\\、一意の新しいファイル名を与えて、システムの system32 ディレクトリ。 一意のファイル名を確認する方法は .chk にその元のファイル タイプ (.dll または .exe) からファイルの種類の名前を変更するがコピーされるとき。 そのため、例を使用して、手順 1 で、ファイルをコピーするチェックされている配布キットから、次のように。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WDK のデバッグ ディレクトリでは、元のファイル名の場合。</th>
<th align="left">SystemRoot%\system32 で次のファイル名をコピーしてください。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ntkrnlmp.exe</p></td>
<td align="left"><p>ntkrnlmp.chk</p></td>
</tr>
<tr class="even">
<td align="left"><p>ntkrpamp.exe</p></td>
<td align="left"><p>ntkrpamp.chk</p></td>
</tr>
<tr class="odd">
<td align="left"><p>halmapic.dll</p></td>
<td align="left"><p>halmapic.chk</p></td>
</tr>
<tr class="even">
<td align="left"><p>hal.dll</p></td>
<td align="left"><p>hal.chk</p></td>
</tr>
</tbody>
</table>

 

## <a name="step-3---changing-the-boot-parameters-using-bcdedit"></a>手順 3 - BCDEdit を使用してブート パラメーターを変更します。

%Systemroot% にチェックされたファイルをコピーしたら\\system32 ディレクトリにより、これらのチェックされたファイルの使用を開始する、システム起動時のエントリを作成する必要があります。 BCDEdit を使用して、これを作成することができます。

**ヒント:**   チェックされているオペレーティング システム イメージと HAL を使用する変更可能な新しいブート エントリを作成する既存のブート エントリをコピーすることができます。 たとえば、現在のブート エントリのコピーを作成する次のコマンドを使用: **「Windows 8.1 部分チェック ビルド」bcdedit/copy {current}/d**します。
BCDEdit を使用して一般的な手順については、次を参照してください。[ドライバーのテストおよびデバッグの起動オプションを変更するためのツール](boot-options-for-driver-testing-and-debugging.md)と[ブート オプションの編集](editing-boot-options.md)します。

**注**  BCDEdit のオプションを無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要がありますを設定する前にします。

 
Windows Vista 以降では部分的なチェック ビルドを構成するには、使用、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドと**カーネル**と**hal**オプション。

たとえば、次のコマンドは、checked HAL およびカーネルのバージョンを使用するブート エントリを構成します。

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} kernel ntkrnlmp.chk
```

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} hal hal.chk
```

カーネル デバッグには、コンピューターを構成することも必要があります。 具体的には、ブートのデバッグ用のブート エントリを有効にする必要があります[ **BCDEdit/bootdebug**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--bootdebug)します。 ブート デバッグできないようにコンピューターに接続されているカーネル デバッガーがない場合は、この新しいブート エントリを選択した場合、Windows 回復環境に、コンピューターはブートします。

```
bcdedit /bootdebug {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} on
```

コマンドの結果を表示するには、次のように入力します。 **bcdedit/enum**します。 **/Enum**オプションには、すべてのブート エントリが一覧表示されます。 たとえば、次のブート エントリがチェックされているバージョンのカーネルと HAL を使用する変更されました。 また、ブートのブート エントリを有効にすることも必要があります。 (bcdedit/bootdebug {ID} 上) をデバッグします。

```
## Windows Boot Loader
-------------------
identifier              {44a942bf-d6ee-11e3-baf8-000ffee4f6cd}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             Windows 8.1 Partial Checked Build
locale                  en-US
inherit                 {bootloadersettings}
recoverysequence        {44a942bd-d6ee-11e3-baf8-000ffee4f6cd}
integrityservices       Disable
recoveryenabled         Yes
bootdebug               Yes
testsigning             Yes
allowedinmemorysettings 0x15000075
osdevice                partition=C:
systemroot              \Windows
kernel                  ntkrnlmp.chk
hal                     hal.chk
resumeobject            {44a942bb-d6ee-11e3-baf8-000ffee4f6cd}
nx                      OptIn
bootmenupolicy          Standard
debug                   Yes
```

## <a name="step-4---restart-the-computer"></a>手順 4 - コンピューターの再起動

構成し、変更を行った後カーネル デバッグは、コンピューターはブート デバッグを有効になっているし、カーネル デバッガーを接続します。 コンピューターを再起動します。 コンピューターを再起動すると、チェックされているオペレーティング システム イメージと HAL を選択できるように新しいオペレーティング システム ブート オプションが表示されます。

チェック ビルドを実行していることを確認するには次の手順に従います。

1.  コンピューターの管理コンソール (compmgmt.msc) では、イベント ビューアーを開きます。

2.  システム ログでイベント ID 6009 を検索します。

    このイベントのプロパティは、空きがあるかどうか、インストールされているオペレーティング システム イメージのチェック ビルドを指定します。

たとえば、次のイベントの説明では、マルチプロセッサ対応のオペレーティング システムのチェック ビルドを示します。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Checked.
```

## <a name="related-topics"></a>関連トピック


[デバッグ (カーネル モードとユーザー モード) の設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-set-up-for-debugging)

[Windows 用デバッグ ツール](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)

 

 







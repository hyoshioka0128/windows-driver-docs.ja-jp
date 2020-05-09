---
title: チェックしたオペレーティングシステムと HAL だけをインストールする
description: チェック済みのオペレーティング システムと HAL のみのインストール (Windows Vista 以降)
ms.assetid: 1203b7cd-50b9-4174-8bec-112019444fac
ms.date: 05/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 810a8ff6d1d3cd0672ea67d9d43bea1cbf27862b
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999060"
---
# <a name="installing-just-the-checked-operating-system-and-hal-for-windows-vista-and-later"></a>チェック済みのオペレーティング システムと HAL のみのインストール (Windows Vista 以降)

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。

コンピューターに完全なチェックを行ったビルドをインストールする代わりに、システムの無償ビルドをインストールし、オペレーティングシステムイメージとハードウェアアブストラクションレイヤー (HAL) のチェックされたバージョンをインストールすることができます。 この手順を使用する場合は、ブートローダーを構成して2つのブートオプションを提供できます。 ブートオプションの1つは、無料のビルド用です。 2番目のブートオプションは、チェックされたオペレーティングシステムイメージと HAL を使用してシステムを起動しますが、他のすべてのシステムコンポーネントの無料バージョンを使用します。

## <a name="step-1---identifying-the-files-to-install-for-windows-vista-and-later"></a>手順 1-Windows Vista 以降でインストールするファイルの識別

部分チェックされたビルドをインストールする前に、システムに無料のビルドをインストールするために使用したオペレーティングシステムイメージと HAL ファイルのバージョンを確認する必要があります。

**ヒント**   :64 ビット版の Windows Vista 以降では、このプロセスは簡単です。 [Windows Driver Kit (wdk)](https://docs.microsoft.com/windows-hardware/drivers/)を使用している場合は、オペレーティングシステムイメージと HAL ファイルを Wdk の Debug\\ディレクトリから使用できます。 「[チェックされたビルドのインストール](installing-the-checked-build.md)」を参照してください。 それぞれのバージョンは、amd64 または ia64 につき1つだけです。 ファイルの名前は ntkrnlmp と Hal.dll です。 使用している Windows のバージョンに対応する WDK がある場合は、「[手順 2: チェック](#step-2---copying-the-checked-files)されたファイルをコピーする」に進むことができます。

 

32ビット版の Windows を実行しているコンピューターでは、次の手順に従って、コピーするファイルの名前を指定します。

### <a name="determining-the-name-of-the-hal-that-is-installed"></a>インストールされている HAL の名前を確認する

1.  ファイル% SystemRoot%\\Inf\\setupapi.log を開き、hal.dll を検索します。

    TargetFilename-' hal.dll ' のような行が見つかります。

2.  ログファイルの同じセクションで、対応する*Sourcefilename*を探します。 *Sourcefilename*の右側の名前は、チェックされたビルドからコピーする必要がある HAL ファイルの名前です。

次の例は、setupapi.log ファイルからのものです。 *Sourcefilename*は halmacpi です。

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

### <a name="determining-the-name-of-the-operating-system-image-file-installed"></a>インストールされているオペレーティングシステムイメージファイルの名前を確認する

Windows Vista 以降の64ビットバージョンでは、ファイルの名前は ntkrnlmp です。

32ビットバージョンの Windows Vista では、次の手順を使用して、ユニプロセッサまたはマルチプロセッサのバージョンがインストールされているかどうかを確認できます。

1.  コンピューターの管理コンソール (compmgmt.msc) でイベントビューアーを開きます。

2.  システムログでイベント ID 6009 を検索します。

    このイベントのプロパティは、1つのプロセッサまたはマルチプロセッサバージョンのオペレーティングシステムイメージがインストールされているかどうかを示します。

たとえば、次の例は、マルチプロセッサをサポートするオペレーティングシステムの無償ビルドを示しています。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Free.
```

コンピューターに搭載されているプロセッサの種類と物理メモリの量がわかっている場合は、次のいずれかのイメージ名を選択できます。 カーネルデバッガーがアタッチされている場合は、 **lmv mnt**コマンドを使用して元のファイル名を識別することもできます。

<span id="NTOSKRNL.EXE"></span>ntoskrnl.exe  
4 GB 以下の物理メモリを搭載したユニプロセッサ x86 アーキテクチャシステム。

<span id="NTKRNLPA.EXE"></span>ntkrnlpa  
PAE がサポートされているユニプロセッサ x86 アーキテクチャシステム。

<span id="NTKRNLMP.EXE"></span>ntkrnlmp  
4 GB 以下の物理メモリを搭載したマルチプロセッサ x86 アーキテクチャシステム。

<span id="NTKRPAMP.EXE"></span>ntkrpq  
PAE がサポートされているマルチプロセッサ x86 アーキテクチャシステム。

## <a name="step-2---copying-the-checked-files"></a>手順 2-チェックされたファイルのコピー

システムのインストール中に使用されたファイルの名前がわかったので、これらのファイルのチェックされたバージョンをシステムにコピーできます。 WDK の debug ディレクトリまたは確認済みディストリビューションキットで特定したファイルを検索します。 次に、これらのファイルをシステムの\\% SystemRoot% system32 ディレクトリにコピーして、新しい一意のファイル名を指定します。 一意のファイル名を確保する方法の1つとして、ファイルの種類を元のファイルの種類 (.dll または .exe) から、コピー時に .chk に変更する方法があります。 したがって、手順 1. の例を使用して、次のように、チェックされた配布キットからファイルをコピーします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WDK の debug ディレクトリにある元のファイル名が次のようになっているとします。</th>
<th align="left">次のファイル名にコピーします。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ntkrnlmp</p></td>
<td align="left"><p>ntkrnlmp</p></td>
</tr>
<tr class="even">
<td align="left"><p>ntkrpq</p></td>
<td align="left"><p>ntkrpq amp</p></td>
</tr>
<tr class="odd">
<td align="left"><p>halmapic</p></td>
<td align="left"><p>halmapic</p></td>
</tr>
<tr class="even">
<td align="left"><p>hal.dll</p></td>
<td align="left"><p>hal.dll .chk</p></td>
</tr>
</tbody>
</table>

 

## <a name="step-3---changing-the-boot-parameters-using-bcdedit"></a>手順 3-BCDEdit を使用してブートパラメーターを変更する

チェックされたファイルを% SystemRoot%\\system32 ディレクトリにコピーした後、これらのチェックされたファイルの使用をシステムが開始できるようにするブート時エントリを作成する必要があります。 BCDEdit を使用してこれを作成できます。

**ヒント**   : 既存のブートエントリをコピーして、確認したオペレーティングシステムイメージと HAL を使用するように変更できる新しいブートエントリを作成することができます。 たとえば、現在のブートエントリのコピーを作成するには、次のコマンドを使用します。 **bcdedit/copy {current}/d "Windows 8.1 部分チェックビルド"**。
BCDEdit を使用するための一般的な手順については、「[ドライバーテストのブートオプションを変更するためのツール」と「デバッグ](boot-options-for-driver-testing-and-debugging.md)および[編集ブートオプション](editing-boot-options.md)」を参照してください。

**メモ**  BCDEdit オプションを設定する前に、コンピューターで BitLocker とセキュアブートを無効にしたり、中断したりすることが必要になる場合があります。

 
Windows Vista 以降で部分的にチェックされたビルドを構成するには、 [**BCDEdit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドおよび**カーネル**と**hal**のオプションを使用します。

たとえば、次のコマンドは、チェックされたバージョンのカーネルと HAL を使用するようにブートエントリを構成します。

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} kernel ntkrnlmp.chk
```

```
bcdedit /set {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} hal hal.chk
```

また、カーネルデバッグ用にコンピューターを構成する必要があります。 具体的には、ブートデバッグ[**BCDEdit/bootdebug**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--bootdebug)のブートエントリを有効にする必要があります。 ブートデバッグを有効にせず、コンピューターにカーネルデバッガーが接続されていない場合は、この新しいブートエントリを選択すると、コンピューターが Windows 回復環境で起動します。

```
bcdedit /bootdebug {44a942bf-d6ee-11e3-baf8-000ffee4f6cd} on
```

コマンドの結果を表示するには、「 **bcdedit/enum**」と入力します。 **/Enum**オプションを指定すると、すべてのブートエントリが一覧表示されます。 たとえば、次のブートエントリは、確認済みのカーネルのバージョンと HAL を使用するように変更されています。 ブートデバッグ (bcdedit/bootdebug {ID} on) に対してもブートエントリを有効にする必要があります。

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

## <a name="step-4---restart-the-computer"></a>手順 4-コンピューターを再起動する

変更を行った後、コンピューターがカーネルデバッグ用に構成され、ブートデバッグが有効になり、カーネルデバッガーが接続されていること。 コンピューターを再起動します。 コンピューターを再起動すると、選択したオペレーティングシステムイメージと HAL を選択できる新しいオペレーティングシステムブートオプションが表示されます。

次の手順を使用して、チェックビルドを実行していることを確認できます。

1.  コンピューターの管理コンソール (compmgmt.msc) でイベントビューアーを開きます。

2.  システムログでイベント ID 6009 を検索します。

    このイベントのプロパティは、オペレーティングシステムイメージがインストールされているかどうかを示します。

たとえば、イベントの次の説明は、マルチプロセッサをサポートするオペレーティングシステムのチェックされたビルドを示しています。

```
Microsoft (R) Windows (R) 6.00. 6001 Service Pack 1 Multiprocessor Checked.
```

## <a name="related-topics"></a>関連トピック


[デバッグの設定 (カーネルモードとユーザーモード)](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-set-up-for-debugging)

[Windows 用デバッグ ツール](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)

 

 







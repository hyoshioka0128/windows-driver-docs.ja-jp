---
title: インストールされている x64 Windows 7 システムを変換する方法
description: インストールされている x64 Windows 7 システムを変換する方法
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: d9fbb625f743fb2314a4cc734138833bc1a0c155
ms.sourcegitcommit: 969a98d4866be74e145df617a9f0963053898a0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153179"
---
# <a name="how-to-convert-an-installed-x64-windows-7-system"></a>インストールされている x64 Windows 7 システムを変換する方法

次の手順は、レガシ MBR + CSM から UEFI + GPT に変換する必要があるシナリオで、It プロフェッショナルで使用することを目的としています。 通常、このプロセスは、Windows 7 x64 がインストールされているシステムで開始されます。

X86 OS システムの場合は、「32ビットと64ビットの UEFI の依存関係とは」の「[ファームウェア WEG](frequently-asked-questions.md)に関する FAQ」の「」セクションを参照してください。

CSM が有効になっているレガシ MBR ブートディスクに BIOS モードでインストールされています。また、システムに次のものがあることを確認したか、OEM に確認してください。

1. CSM を有効または無効にする機能
1. UEFI ファームウェア 2.3.1 c 以降がある
1. 関心のあるセキュリティ機能 (セキュアブート、HVCI、Credential Guard) には、システム上で既に構成されているすべての適切なコンポーネントがあります。
    > [!NOTE]
    > 現在、Microsoft では、既存のファイルシステムをワイプまたはクリーニングし、クリーンディスクに新しいファイルシステムを作成することなく、レガシ MBR ブートディスクを GPT ディスクに変換するメカニズムを備えていません。

たとえば、Diskpart.exe を使用して、既存のパーティションを**クリーンアップ**してから、そのディスクで [ **GPT の変換**] コマンドを実行する必要があります。 [**クリーン**] コマンドを実行すると、ディスク全体がワイプされます。

1. すべてのデータがプライマリブートデバイスからバックアップされていること、およびユーザーまたは It プロフェッショナルがプライマリブートデバイスがディスク0であることを確認していることを確認します。
1. プライマリブートデバイスが完全にバックアップされている (ディスク上のすべてのデータがワイプされる)
1. BIOS に再起動します (BIOS ブートモードを UEFI ブートモードに切り替える手順については製造元に問い合わせてください)。また、UEFI + CSM に切り替えます。
1. X64 WinPE を含む USB フラッシュドライブを起動します。
1. WinPE を起動した後、コマンドプロンプトで次のコマンドを実行します。
    1. Diskpart.exe を開きます。
    1. select disk 0
    1. リスト par
    1. ボリュームを一覧表示する <= 既存の OS が割り当てられている場所を把握できるように、現在のドライブ文字を識別します (OS のドライブ文字を指定し、後で使用します)
    1. GPT の変換
    1. select partition 1
    1. par EFI size = 800 (mg) を作成する
    1. フォーマット fs = fat32 ラベル = システム
    1. 文字 S の割り当て
    1. par MSR の作成
    1. リスト par
    1. exit
1. コマンドプロンプトに戻り、次のように入力します。
    1. :
    1. BCDboot c: \\ windows/s s:/F UEFI
       > [!NOTE]
       > これは、上記の手順 c で特定されたドライブ文字です。
    1. dir/a
    1. 次のように表示します。 s: \\ EFI
    1. 再起動して OS を起動します

## <a name="verify-system-is-booted-in-uefi-mode"></a>システムが UEFI モードで起動されていることを確認する

次のいずれかの方法を使用して、システムが UEFI モードで起動されていることを確認します。

### <a name="msinfo32"></a>MSINFO32.EXE

Windows 10 システムの場合:

1. キーを押して [ \<Windows key\>  +  \<R\> **実行**] ダイアログを開きます。
1. 「Msinfo32」と入力し、[ **OK]** をクリックします。

既定では、[システムの概要] ページが開きます。

次の情報を探します。

![[システムの概要] ページ](images/system-summary-page.png)

管理者として実行するには、次の手順に従います。

1. キーを押して [ \<Windows key\>  +  \<R\> **実行**] ダイアログを開きます。
1. 「システム情報」の入力を開始します。

**システム情報**が強調表示されている場合は、を押したまま \<CTRL\>  +  \<SHIFT\> ヒットし \<ENTER\> ます。または、マウスを使用して右クリックし、[**管理者として実行**] を選択します。

ユーザー Access Control (UAC) によって、次のメッセージが表示されます。 [**このアプリをデスクトップに変更しますか?]**

### <a name="bcdedit"></a>BCDEDIT

Windows 7 以降のシステムの場合:

1. 管理者特権でのコマンドプロンプトを開始する
1. "BCDedit/enum {current}" を実行する
    > [!NOTE]
    > WinPE から起動した場合は、BCDedit の "/store" スイッチを使用します。
    > UEFI を使用している場合は、パスに「Winload. efi」と表示されます。
    > CSM がある場合、パスはサンプル出力に示されているように Winload .exe を表示します。

#### <a name="sample-output"></a>サンプル出力

```cmd
Windows Boot Loader
-------------------
identifier {current}
device partition=C:
path \WINDOWS\system32\winload.efi
```

### <a name="notepad-and-setupactlog"></a>メモ帳と SETUPACT。出力

1. 管理者特権でのコマンドプロンプトを開始する
1. "Notepad c: \\ windows \\ panther \\ setupact .log" を実行します。
1. Enter キーを押して検索 \<CTRL\>  +  \<F\> (または検索)
1. "Callback \_ boot環境検出" を検索します。

    - 結果は次のようになります。

        ```cmd
        Callback_BootEnvironmentDetect:FirmwareType 1

        Callback_BootEnvironmentDetect: Detected boot environment: BIOS
        ```

        または

        ```cmd
        Callback_BootEnvironmentDetect:FirmwareType 2

        Callback_BootEnvironmentDetect: Detected boot environment: UEFI
        ```

特定のシステムの構成の詳細については、OEM に問い合わせることが必要になる場合があります。

> [!WARNING]
> Diskpart.exe またはセットアップを使用してハードディスクドライブのパーティション情報をクリーニングまたはワイプすると、ディスク上のデータがすべて破棄されます。 これらの変更を行う前に、工場出荷時のイメージの回復方法またはデータバックアップオプションに関する PC の製造元に問い合わせてください。

## <a name="related-resources"></a>関連リソース

[推奨される UEFI ベースのディスクパーティション構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744301(v=ws.10))

[Win7 によるプログラム、システム設定、およびファイルのバックアップ](https://support.microsoft.com/help/17127/windows-back-up-restore#1TC=windows-7)

[Win7 Windows 7 バックアップを使用してファイルと PC を保護する](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/bg-p/FileCAB)

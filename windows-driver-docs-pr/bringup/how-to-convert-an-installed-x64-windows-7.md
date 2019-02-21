---
title: インストールされている x64 に変換する方法 システムの Windows 7
description: インストールされている x64 に変換する方法 システムの Windows 7
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: cffd5cfbf35961844f840f4b4b6e40c8e8e1107e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549956"
---
# <a name="how-to-convert-an-installed-x64-windows-7-system"></a>インストールされている x64 に変換する方法 システムの Windows 7

次の手順は、使用するためで、it プロフェッショナルのシナリオでレガシ MBR + CSM から UEFI と GPT に変換する必要があります。 通常、このプロセスは、Windows 7 がインストールされている x64 いるシステムから始まります。

X86 OS システムでは、セクションを参照して、[ファームウェア WEG FAQ](frequently-asked-questions.md)について"何が 32 ビットの vs への依存関係です。64 ビットの UEFI ですか?"。

CSM が有効な場合、レガシ MBR ブート ディスクに BIOS モードでインストールされていると、知っているかがチェックで、OEM が、システムでは、次のことを確認します。

1. 機能を有効にし、CSM を無効にします。
1. UEFI 2.3.1c のファームウェアまたはそれ以降
1. (セキュア ブート、Device Guard、や Credential Guard) に注目しているセキュリティ機能には、システムに既に構成されているすべての適切なコンポーネントがあります。
    > [!NOTE]
    > Microsoft には現在、最初のワイプまたは既存のファイル システムをクリーンアップしてクリーン ディスク上に新しいファイル システムを作成することがなく、レガシ MBR ブート ディスクを GPT ディスクに変換するためのメカニズムがありません。

Diskpart.exe を使用する必要がありますが、**クリーン**実行する前に、既存のパーティション、 **convert GPT**そのディスクにあるコマンド。 **クリーン**コマンドは、ディスク全体がワイプされます。

1. すべてのデータが、プライマリのブート デバイスからバックアップし、ユーザーまたは it プロフェッショナル向けの主なブート デバイスはディスク 0 が確認を確認します。
1. プライマリのブート デバイスが完全にサポートされる最大 (ディスク上の残りのすべてのデータは消去されます)
1. UEFI csm + BIOS (UEFI ブート モードを BIOS ブート モードの切り替えの手順については、製造元にお問い合わせください) の案内スイッチには、再起動します。
1. X64 を含む USB フラッシュ ドライブ ブート WinPE
1. コマンド プロンプトで、WinPE で起動: の後
    1. Diskpart.exe を開く
    1. ディスク 0 を選択します。
    1. リスト par
    1. ボリュームの一覧を表示 < = 既存の OS が割り当てられていることがわかるように、現在のドライブ文字を識別するために (後で使用されている OS のドライブ文字を識別する)
    1. convert GPT
    1. パーティション 1 を選択します。
    1. 作成 par EFI size = 800 (mg)
    1. フォーマット fs = fat32 ラベル システムを =
    1. S 文字を割り当てる
    1. par MSR を作成します。
    1. リスト par
    1. exit
1. コマンド プロンプトで次のように入力します。
    1. %s:
    1. BCDboot の c:\\windows/s s:/f UEFI
       > [!NOTE]
       > これは、特定のドライブ文字 c および d が上記の手順で
    1. dir/a
    1. %S: を表示する必要があります\\EFI
    1. 再起動し、オペレーティング システムをブートしようとしてください。

## <a name="verify-system-is-booted-in-uefi-mode"></a>システムが UEFI モードで起動したことを確認します。

システムの確認には、次のメソッドのいずれかが UEFI モードで起動に使用します。

### <a name="msinfo32"></a>MSINFO32

Windows 10 システム。

1. キーを押して\<Windows キー\> + \<R\>を開く、**実行**ダイアログ
1. Msinfo32 を入力し、クリックして**OK**

既定では、システムの概要ページが開きます。

次の情報になります。

![システムの概要 ページ](images/system-summary-page.png)

を管理者として実行するには、次の手順を使用します。

1. キーを押して\<Windows キー\> + \<R\>を開く、**実行**ダイアログ
1. 「システム情報」の入力を開始します。

場合**システム情報**が強調表示され、保持\<CTRL\> + \<shift キーを押し\>とヒット\<」と入力\>、またはマウスを使用して、右クリック選択と**管理者として実行**します。

求めユーザー アクセス制御 (UAC) によって、次のメッセージ。**デスクトップを変更するのには、このアプリを作成しますか。**

### <a name="bcdedit"></a>BCDEDIT

Windows 7 およびそれ以降のシステム。

1. 管理者特権のコマンド プロンプトを開始します。
1. "BCDedit/enum {現在}"の実行します。
    > [!NOTE]
    > WinPE から起動されている場合は、BCDedit.exe で"/store"スイッチを使用します。
    > UEFI がある場合は、パスは、Winload.efi を紹介します。
    > CSM がある場合は、パスは、出力の例に示すように、Winload.exe を表示します。

#### <a name="sample-output"></a>サンプル出力

```cmd
Windows Boot Loader
-------------------
identifier {current}
device partition=C:
path \WINDOWS\system32\winload.efi
```

### <a name="notepad-and-setupactlog"></a>メモ帳と SETUPACT します。ログ

1. 管理者特権のコマンド プロンプトを開始します。
1. 実行"メモ帳の c:\\windows\\panther\\setupact.log"
1. キーを押して\<CTRL\> + \<F\>検索 (または search)
1. 検索"コールバック\_BootEnvironmentDetect"

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

特定のシステムの構成の詳細について OEM に相談する必要があります。

> [!WARNING]
> Diskpart.exe またはセットアップを使用して、クリーニングまたはワイプのハード ディスク ドライブ パーティション情報をすべて破棄されますディスク上のデータ。 工場出荷時イメージの回復方法またはデータ バックアップ オプションに関するこれらの変更を行う前に、PC の製造元を参照してください。

## <a name="related-resources"></a>関連リソース

[UEFI ベースのディスク パーティションの構成をお勧めします。](https://technet.microsoft.com/library/dd744301)

[プログラム、システムの設定、およびファイルを戻す Win7](http://windows.microsoft.com/windows/back-up-programs-system-settings-files#1TC=windows-7)

[Win7 は、ファイルと Windows 7 のバックアップを PC を保護します。](https://blogs.technet.microsoft.com/filecab/2009/10/23/protect-your-files-and-pc-with-windows-7-backup/)

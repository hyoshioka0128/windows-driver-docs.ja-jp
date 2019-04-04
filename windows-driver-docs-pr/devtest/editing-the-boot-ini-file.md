---
title: Boot.ini ファイルの編集
description: Windows Vista では、前に、Windows を実行している BIOS ベースのコンピューターは、Boot.ini テキスト ファイルのブート オプションを格納します。
ms.assetid: 9edbbd5e-36b5-4a80-925d-a007a4469984
keywords:
- Bootcfg ツール
- Boot.ini ファイル、WDK の編集
- ブート オプションの編集
- メモ帳 WDK ブート オプション
- テキスト エディターの WDK ブート オプション
- 手動編集 WDK のブート オプション
- ブート エントリ パラメーター WDK
- WDK のブート パラメーター
- ブートの無期限のタイムアウト値 WDK
- WDK 起動のタイムアウトの値
- WDK ブート オプションのタイムアウト
- Boot.ini ファイル WDK、属性の削除
- Boot.ini の属性の削除
- ブート オプションを表示します。
- Boot.ini ファイル WDK, 表示
- エディターの WDK ブート オプション
- ブート オプション、WDK の編集
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8db413aeebdde2e1c135717876544e0147ef6d9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531293"
---
# <a name="editing-the-bootini-file"></a>Boot.ini ファイルの編集


> [!IMPORTANT] 
> このトピックでは、Windows XP および Windows Server 2003 でサポートされるブート オプションについて説明します。 Windows の最新バージョンのブート オプションを変更する場合は、[Windows Vista 以降のブート オプション](boot-options-in-windows-vista-and-later.md)を参照してください。

Windows Vista では、前に、Windows を実行している BIOS ベースのコンピューターは、Boot.ini テキスト ファイルのブート オプションを格納します。 Bootcfg を使用して Boot.ini を編集することができます (`bootcfg.exe`)、Windows XP および Windows Server 2003 に含まれるか、メモ帳などのテキスト エディターを使用して、ツール。 Bootcfg は、Windows ヘルプとサポートで記載されています。 表示またシステム コントロール パネルの ブート オプションを変更します。 システムのプロパティ ダイアログ ボックスの 詳細設定 タブで、の設定をクリックします。**起動と回復**します。 この機能が限られているために、このセクションでは説明しません。 については、**起動と回復** ダイアログ ボックスで、ヘルプとサポート センターを参照してください。

## <a name="bootcfg"></a>Bootcfg

Bootcfg は、ローカルおよびリモート コンピューター上のブート オプションを編集できるコマンド ライン ツールです。 Bootcfg と同じコマンドと手順を使用して、拡張ファームウェア インターフェイス非揮発性ランダム アクセス メモリ (NVRAM の EFI) ブート オプションと同様に、Boot.ini を編集できます。 含まれている Bootcfg、 `%Systemroot%\\System32` Windows XP および Windows Server 2003 のディレクトリ。 (Bootcfg 表示は、EFI の NVRAM にブート オプションを格納するシステムで若干異なりますが、コマンドは同じ)。

Bootcfg を使用するには追加、削除、およびすべてのブート エントリのパラメーターとブート オプションを変更するにはただし、ブートの無期限のタイムアウト値を設定するのには使用できません。 ブート オプションを設定または置換、またはオペレーティング システムをアップグレードした後、それらをリセットするは、スクリプトまたはバッチ ファイルで Bootcfg コマンドを使用することもできます。

手動で編集とは異なり Bootcfg 編集は、Boot.ini の保護の属性を変更することがなくオプションを起動します。 オペレーティング システムが起動を妨げる可能性のある入力ミスを回避することができます。

Bootcfg を使用するコンピューターの Administrators グループのメンバーがあります。 Bootcfg の使用に関する詳細な手順については、ヘルプとサポート センターを参照してください。

## <a name="editing-in-notepad"></a>メモ帳での編集

メモ帳などのテキスト エディターを使用して、Boot.ini を編集することができます。 ただし、このメソッドはエラーが発生しやすいため、その場合にのみ使用 Bootcfg は使用できません。

Boot.ini を編集する前に、不注意による変更からファイルを保護する Windows を使用するファイル属性を削除する必要があります。 NTFS ボリュームに Boot.ini がある場合は、その属性を変更するコンピューターの Administrators グループのメンバーがあります。

手動で編集 Boot.ini を準備するのにには、次の手順を使用します。 この手順では、システム、ファイルの非表示、および読み取り専用の属性を削除します。

**編集するための Boot.ini 属性を構成するには**

1.  開いている**Windows コマンド プロンプト**します。 

2.  システム ボリュームのルートに移動します。

3.  コマンドラインで次のテキストを入力します。

    ```
    attrib -s -h -r Boot.ini
    ```

    システムでは、非表示、および読み取り専用の属性は、ファイルから削除されます。
    
4.  編集するため、メモ帳でファイルを開きます。 Windows コマンド プロンプトでは、次のコマンドは、トリックを迅速に行う必要があります。

    ```
    notepad.exe Boot.ini
    ```

5.  編集が完了したら、Boot.ini を保護するファイル属性を戻すことができます。 ただし、Ntldr では、任意の属性セットで Boot.ini を使用できます。 属性を復元するには、Windows コマンド プロンプトで、次を入力します。

    ```
    attrib +s +h +r Boot.ini
    ```

    これは、Boot.ini ファイルを保護している属性を復元します。

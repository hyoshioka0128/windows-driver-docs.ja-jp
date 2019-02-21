---
title: Efi ブート オプションの編集
description: Efi ブート オプションの編集
ms.assetid: 0fdd01b3-7475-4959-87d8-5ec8ae65fea0
keywords:
- NVRAM ブート オプション、WDK の編集
- EFI NVRAM ブート オプション、WDK の編集
- ブート オプションの編集
- Bootcfg ツール
- Nvrboot ツール
- エディターの WDK ブート オプション
- ブート オプションを表示します。
- NVRAM ブート オプション WDK, 表示
- EFI NVRAM ブート オプション WDK, 表示
- ブート オプション、WDK の編集
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: d9dc5ea74b6d95452edce219253eef5a00aa45c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539263"
---
# <a name="editing-boot-options-in-efi"></a>Efi ブート オプションの編集


オプションを編集するブート コンピューターで EFI NVRAM と Windows Server 2003 または NT ベースの Windows の以前のバージョンを実行するには、Bootcfg (bootcfg.exe)、Windows、または Nvrboot (nvrboot.efi) EFI 環境で実行されているツールで実行されるツールを使用します。 Windows XP 64-bit Edition および Windows Server 2003 の 64 ビット バージョンでは、どちらのツールが含まれます。

表示またシステム コントロール パネルの ブート オプションを変更します。 システムのプロパティ ダイアログ ボックスの 詳細設定 タブで、の設定をクリックします。**起動と回復**します。 この機能が限られているために、このセクションでは説明しません。 については、**起動と回復** ダイアログ ボックスで、ヘルプとサポート センターを参照してください。

## <a name="bootcfg"></a>Bootcfg

Bootcfg (bootcfg.exe) はブート オプションを編集するコマンド ライン ツールで同じ Bootcfg コマンドと手順を使用して、ローカルまたはリモート コンピューター、Boot.ini ファイルまたは EFI NVRAM にブート オプションを編集することができます。 Bootcfg が、%systemroot% 内に含まれる\\Windows XP および Windows Server 2003 の System32 ディレクトリ。 (Bootcfg 表示は、EFI の NVRAM にブート オプションを格納するシステムで若干異なりますが、コマンドは同じ)。

Bootcfg を使用するには追加、削除、およびすべての有効なブート オプション; の値を変更するにはただし、無制限のタイムアウト値を設定することはできません。 ブート オプションを設定または置換、またはオペレーティング システムをアップグレードした後、それらをリセットするは、スクリプトまたはバッチ ファイルで Bootcfg コマンドを使用することもできます。

EFI NVRAM にブート オプションを格納するシステムで、Bootcfg もブート パーティション テーブルを表示、ミラー化されたドライブのブート エントリを追加および更新できますシステム パーティションの Guid。

Bootcfg を使用するコンピューターの Administrators グループのメンバーがあります。 Bootcfg の使用に関する詳細な手順については、ヘルプとサポート センターを参照してください。

## <a name="nvrboot"></a>Nvrboot

Nvrboot (nvrboot.efi) は、Windows XP 64-bit Edition および Windows Server 2003 の 64 ビット バージョンに含まれる EFI ベースのブート エントリ エディターです。 Nvrboot は EFI 環境で実行されます。 オペレーティング システムの実行中に、Nvrboot を実行することはできません。

Nvrboot 編集は、エントリのみをブートします。 使用できますが、表示または変更、ブート メニューのタイムアウト値を使用することはできません、**プッシュ**コマンド (**nvrboot p**) 既定のブート エントリを変更します。

Nvrboot には、ブート エントリのバックアップ コピーをエクスポートし、NVRAM にブート エントリのバックアップ コピーをインポートするコマンドも含まれています。 この手順については、 [efi ブート オプションをバックアップする](backing-up-boot-options-in-efi.md)セクション。

Nvrboot には、わかりやすい形式のブート オプションが表示されます。 たとえばが表示されますオペレーティング システム ファイルのパスと、ブート ローダーのファイル パスとしてパーティション GUID の後に Windows ディレクトリ パス。

次の手順では、Itanium ベース システムの多くに付属のツールでは EFI シェルから Nvrboot を開始する方法について説明します。 EFI シェルのツールは、製造元によって異なります、ため、このセクションで説明可能性がありますを正確に示さない EFI シェル インターフェイスで、特定のコンピューターにします。

**Nvrboot を実行するには**

1.  コンピューターを再起動します。

2.  **ブート**] メニューの [選択**EFI シェル**します。

3.  シェル プロンプトでは、c: などのシステム パーティションのドライブ文字またはファイル システムの番号を入力または**FS**n、n は、システム パーティションのファイル システムの数。

4.  型**cd msutil** nvrboot.efi がある Msutil ディレクトリに移動します。

5.  Nvrboot を開始するには、入力**nvrboot**します。

な Nvrboot の手順については、次のように入力します。 **h**します。

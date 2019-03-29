---
title: EMS リダイレクトを有効にするためのブート パラメーター
description: EMS リダイレクトを有効にするためのブート パラメーター
ms.assetid: b93fd580-0e1d-4b1e-8358-1c6ce7e2eb5e
keywords:
- WDK のブート パラメーター
- ブート エントリ パラメーター WDK
- 緊急管理サービスの WDK のブート パラメーター
- EMS のリダイレクト WDK のブート パラメーター
- リモート管理 WDK のブート パラメーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b045ee198245272a2c3eb1be8a09794e5ee2e21b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572639"
---
# <a name="boot-parameters-to-enable-ems-redirection"></a>EMS リダイレクトを有効にするためのブート パラメーター

緊急管理サービス (EMS) テクノロジは、ネットワークまたはその他の標準のリモート管理ツールにサーバーが接続されていない場合でも、サーバーの選択したコンポーネントをリモートで制御することができます。 EMS は、x86-、x64-、および Itanium ベースのコンピューターの Windows Server 2003 オペレーティング システムのすべてのバージョンでサポートされます。

> [!NOTE]
> このトピックでは、Windows Server 2003 を実行するコンピューターで EMS を有効にする方法について説明します。 このセクションで説明されているブート パラメーターは、Windows Vista または Windows の以降のバージョンではサポートされていません。
> ブート ローダーがかっこで囲まれた語句の場合を追加するコンピューターの BIOS ファームウェアで EMS のブート エントリが構成されると、 \[ems を有効になっている\]、ブート メニューに表示されるフレンドリ名にします。 ただし、ブート ローダーは、フレンドリ名と一緒のかっこで囲まれた語句は 70 文字を超えたときに、ブート メニューから、かっこで囲まれた語句を省略します。 かっこで囲まれた語句を復元するには、フレンドリ名を短きます。

コンピューターかどうかを判断するには、ACPI ファームウェア、デバイス マネージャー (devmgmt.msc) を使用してが。 デバイス マネージャーで、展開、**コンピューター**ノード。 ACPI ファームウェア、下のノードの名前を持つコンピューターで**コンピューター** 、単語を含む**ACPI**します。

## <a name="enabling-ems-on-a-computer-without-an-acpi-spcr-table-in-operating-systems-prior-to-windows-server-2008"></a>Windows Server 2008 より前のオペレーティング システムでは ACPI SPCR テーブルのないコンピューターで EMS を有効にします。

BIOS ファームウェアを ACPI シリアル ポート Console Redirection (SPCR) テーブルではありませんが、コンピューターでの EMS コンソール リダイレクトを有効にするには追加、**リダイレクト COM を = * * * x*と**redirectbaudrate =** パラメーターを\[ブート ローダー\] Boot.ini ファイルのセクション。 これらのパラメーターは、EMS のコンソールのリダイレクトのポートと送信レートを設定します。 BIOS で帯域外の通信が確立されている同じポートと送信レートを使用します。 次に、追加、 [**リダイレクト/** ](https://msdn.microsoft.com/library/windows/hardware/ff557180)ブート エントリのパラメーター。

次の Bootcfg コマンドは、一覧の最初のブート エントリの EMS コンソールのリダイレクトを使用できます。 COM2 のポートを設定し、115, 200 キロ ビット/秒 (Kbps) に転送速度を設定します。 これらは、同じポートとボー レートの設定、管理者が帯域外のポートの BIOS で設定します。

```command
bootcfg /ems ON /port COM2 /baud 115200 /id 1
```

次の Bootcfg 表示では、コマンドの結果を示します。 新しく追加したパラメーターは、太字で表示されます。

```command
## Boot Loader Settings
timeout:          3
default:          multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
redirect:         COM2
redirectbaudrate: 115200

Boot Entries
------------
Boot entry ID:   1
Friendly Name:   "Windows Server 2003, Standard with EMS"
Path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
OS Load Options: /fastdetect /redirect
```

次の例では、サンプルの Boot.ini ファイルで同じコマンドの結果を示します。

```command
[boot loader]
timeout=1
default=multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect=COM2
redirectbaudrate=115200
[operating systems]
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="EMS boot" /fastdetect /redirect
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="Windows Server 2003, Standard" /fastdetect
```

## <a name="enabling-ems-on-a-computer-without-an-acpi-spcr-table-in-windows-server-2008"></a>Windows Server 2008 で ACPI SPCR テーブルのないコンピューターでの EMS を有効にします。

BIOS ファームウェアを ACPI シリアル ポート Console Redirection (SPCR) テーブルではありませんが、コンピューターでの EMS コンソール リダイレクトを有効にするには使用、 [ **BCDEdit/emssettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542198) COM ポートを設定するコマンドボー レート。

これらのパラメーターは、EMS のコンソールのリダイレクトのグローバル ポートと送信レートを設定します。 BIOS で帯域外の通信が確立されている同じポートと送信レートを使用します。

次に、使用、 [ **BCDEdit/ems** ](https://msdn.microsoft.com/library/windows/hardware/ff542193)ブート エントリの EMS を有効にするコマンド。

次のコマンドは、COM2 と 115200 のボー レートを使用するグローバル EMS のリダイレクト設定を設定し、指定されたブート エントリの EMS を有効にします。

```command
bcdedit /emssettings EMSPORT:2 EMSBAUDRATE:115200
```

```command
bcdedit /ems {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

## <a name="enabling-ems-on-a-computer-with-an-spcr-table-in-operating-systems-prior-to-windows-server-2008"></a>Windows Server 2008 より前のオペレーティング システムで SPCR テーブルを使用しているコンピューターで EMS を有効にします。

ACPI BIOS ファームウェアと ACPI SPCR テーブルを使用しているコンピューターでは、EMS を有効にするを使用するか、**リダイレクト = USEBIOSSETTINGS**パラメーター、または **リダイレクト COM を = * * * x*と**redirectbaudrate =** パラメーター。 次に、追加、 [**リダイレクト/** ](https://msdn.microsoft.com/library/windows/hardware/ff557180)ブート エントリのパラメーター。

次の例での使用、**リダイレクト = USEBIOSSETTINGS**パラメーター。 次の Bootcfg コマンドは、一覧の最初のブート エントリの EMS コンソールのリダイレクトを使用できます。

```command
bootcfg /ems ON /port BIOSSET /id 1
```

次の Bootcfg 表示では、コマンドの結果を示します。 新しく追加したパラメーターは、太字で表示されます。

```command
## Boot Loader Settings
timeout: 1
default: multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect:USEBIOSSETTINGS

Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: EMS boot
Path:             multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
OS Load Options:  /fastdetect /redirect

Boot entry ID:    2
OS Friendly Name: Windows Server 2003, Standard
Path:             multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
OS Load Options:  /fastdetect
```

次の例では、サンプルの Boot.ini ファイルで同じコマンドの結果を示します。

```command
[boot loader]
timeout=1
default=multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
redirect=USEBIOSSETTINGS
[operating systems]
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="EMS boot" /fastdetect /redirect
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="Windows Server 2003, Standard" /fastdetect
```

## <a name="enabling-ems-on-a-computer-with-an-spcr-table-in-windows-server-2008"></a>Windows Server 2008 で SPCR テーブルを使用しているコンピューターでの EMS を有効にします。

ACPI BIOS ファームウェアと ACPI SPCR テーブルを使用しているコンピューターでは、EMS を有効にするを使用することができます、 [ **BCDEdit/emssettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542198)どちらかを指定し、 **BIOS**パラメーターまたは、 **emsport**と**emsbaudrate**パラメーター。 ブート エントリの EMS を有効にするを使用して、 [ **BCDEdit/ems** ](https://msdn.microsoft.com/library/windows/hardware/ff542193)コマンド。

次の例では、使用する方法、 **BIOS**パラメーター。 次の BCDEdit コマンドでは、現在のブート エントリの EMS コンソールのリダイレクトを使用できます。

```command
bcdedit /emssettings bios
bcdedit /ems on
```

## <a name="enabling-ems-on-a-computer-with-efi-firmware-in-operating-systems-prior-to-windows-server-2008"></a>Windows Server 2008 より前のオペレーティング システムで、EFI ファームウェアを使用しているコンピューターで EMS を有効にします。

EFI ファームウェアを使用しているコンピューターで EMS を有効にするのには、Bootcfg を使用して追加、 [**リダイレクト/** ](https://msdn.microsoft.com/library/windows/hardware/ff557180)ブート エントリのパラメーター。 Windows では、ファームウェアの SPCR テーブルを参照して、帯域外のポートとその設定を検索し、EMS のコンソールのリダイレクトを同じポートとレートを使用します。

次の Bootcfg コマンドは、Itanium ベースのコンピューターで EMS のリダイレクトを使用できます。 使用して、Bootcfg **/ems**スイッチの引数を追加すると、 **リダイレクト/** ブート エントリのパラメーター。 **/Id**スイッチ ブート エントリを識別します。

```command
bootcfg /ems ON /id 1
```

Bootcfg コマンドの結果が EFI NVRAM にブート オプションの次の Bootcfg 表示されます。 最初のブート エントリは、EMS のコンソールのリダイレクトを有効にされたオペレーティング システムを読み込むために構成されます。

```command
Boot Options
------------
Timeout:             30
Default:             \Device\HarddiskVolume3\WINDOWS
CurrentBootEntryID:  1

Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise with EMS
OsLoadOptions:     /fastdetect /redirect
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS
```

## <a name="enabling-ems-on-a-computer-with-efi-firmware-in-windows-server-2008"></a>Windows Server 2008 で EFI ファームウェアを使用しているコンピューターでの EMS を有効にします。

EFI ファームウェアを使用しているコンピューターでは、EMS を有効にする、使用、 [ **BCDEdit/ems** ](https://msdn.microsoft.com/library/windows/hardware/ff542193)コマンドし、ブート エントリを指定します。 Windows では、ファームウェアの SPCR テーブルを参照して、帯域外のポートとその設定を検索し、EMS のコンソールのリダイレクトを同じポートとレートを使用します。

次のコマンドは、{18b123cd-2bf6-11db-bfae-00e018e2b8db} の識別子を持つ指定されたブート エントリの EMS コンソールのリダイレクトを使用できます。

```command
bcdedit /ems {18b123cd-2bf6-11db-bfae-00e018e2b8db} on
```

## <a name="changing-ems-settings-on-a-computer-with-bios-firmware-in-operating-systems-prior-to-windows-server-2008"></a>Windows Server 2008 より前のオペレーティング システムの BIOS ファームウェアを使用しているコンピューターでの EMS 設定の変更

1 つのブート エントリの EMS を構成するときに、追加、**リダイレクト =** パラメーターを\[ブート ローダー\] Boot.ini ファイルのセクション。 ただし、さらにブート エントリの EMS を有効にするとする必要はありませんを追加する、**リダイレクト =** パラメーターをもう一度です。 などのすべてのエントリ、\[ブート ローダー\]セクション**リダイレクト =** (と**redirectbaudrate =)** コンピューター上のすべてのブート エントリに適用されます。

次の Bootcfg コマンドは、2 番目のブート エントリの EMS を使用できます。 ポートとボー レートが既に設定されているために、ありません **/port**または **/baud**コマンドにスイッチします。

```command
bootcfg /ems ON /id 2
```

ポートとボー レートの設定を変更するには、使用、Bootcfg **/ems**スイッチを引数を編集します。 次のコマンドは、com1、EMS のポートを変更し、ボー レートを 57,600 Kbps に変更します。

```command
bootcfg /ems EDIT /port COM1 /baud 57600
```

ブート エントリの EMS を無効にするを使用、Bootcfg **/ems** OFF 引数にスイッチします。 次のコマンドでは、最初のブート エントリの EMS を無効にします。

```command
bootcfg /ems OFF /id 1
```

Bootcfg もから EMS ポートとボー レートの設定が削除、他のブート エントリの EMS が無効である場合、\[ブート ローダー\] Boot.ini ファイルのセクション。

## <a name="changing-ems-settings-on-a-computer-running-windows-server-2008"></a>Windows Server 2008 を実行するコンピューターでの EMS 設定の変更

ACPI BIOS ファームウェアと ACPI SPCR テーブルを持つコンピューター上のブート エントリの EMS を構成するときに使用できます、 [ **BCDEdit/emssettings** ](https://msdn.microsoft.com/library/windows/hardware/ff542198)コマンドを指定するか、 **BIOS**オプションまたは**emsport**と**emsbaudrate**オプション。 使用する場合、 **BIOS**オプションを設定しないでください、 **emsport**または**emsbaudrate**オプション。

EFI ファームウェアをあるコンピューター上で EMS を構成することも ACPI BIOS ファームウェア、ACPI SPCR テーブルを使用せずには、使用するときに、 **BCDEdit/emssettings**コマンドを指定、 **emsport**と**emsbaudrate**オプション。

**Emsport**と**emsbaudrate**オプションは、EMS のコンソールのリダイレクトのシリアル ポートと送信レートを設定します。 これらの設定は、コンピューター上のすべてのブート エントリに適用されます。 使用する**emsbaudrate**も設定する必要があります、 **emsport**オプション。 既定では、転送速度は 9600 (9,600 Kbps) に設定されます。

たとえば、次のコマンドは、COM2 に EMS ポートを変更し、57,600 Kbps に、ボーを変更します。

```command
bcdedit /emssettings EMSPORT:2 EMSBAUDRATE:57600
```

有効またはブート エントリの EMS を無効にする、使用、 [ **BCDEdit/ems** ](https://msdn.microsoft.com/library/windows/hardware/ff542193)コマンド。

たとえば、次のコマンドは、{173075c9-2cb2-11dc-b426-001558c41f5c} の識別子を持つ特定のブート エントリの EMS を有効.

```command
bcdedit /ems {173075c9-2cb2-11dc-b426-001558c41f5c} on
```

を現在のブート エントリの EMS を無効にするには、次のコマンドを使用します。

```command
bcdedit /ems off
```

> [!NOTE]
> 各ブート エントリは、識別子として GUID を使用します。 識別子を指定しない場合、 **BCDEdit**コマンドは、現在のオペレーティング システムのブート エントリを変更します。 ブート エントリに関連付けられた GUID を中かっこで囲む必要がありますブート エントリが指定されている場合 **{}** します。 すべてのアクティブなブート エントリの GUID 識別子を表示する、 **bcdedit/enum**コマンド。
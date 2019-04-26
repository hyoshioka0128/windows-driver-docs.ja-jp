---
title: ブート エントリのフレンドリ名の変更
description: ブート エントリのフレンドリ名の変更
ms.assetid: 28f4f449-9027-453e-877a-d656539296c0
keywords:
- WDK のブート オプションの名前
- WDK のブート オプションのフレンドリ名
- WDK のブート エントリの名前を変更します。
- Boot.ini ファイル WDK、フレンドリ名
- ブート オプション WDK、フレンドリ名
ms.date: 01/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: f5c5b21ba678ae6d82d6f9de835bd4b805412a14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343986"
---
# <a name="changing-the-friendly-name-of-a-boot-entry"></a>ブート エントリのフレンドリ名の変更


、Windows では、Windows ブート マネージャーに表示される項目は、各ブート エントリの説明を示します。

通常、ブート エントリをコピーした後に元から区別するために、新しく作成されたエントリのフレンドリ名を変更します。

カスタマイズされたブート エントリを認識しやすくフレンドリ名を変更することもできます。 エントリを正確に説明する文字列には、膨大な時間と労力を保存できます。

たとえば、次のフレンドリ名の文字列は、ほとんどの値を追加します。

```
"Windows 10 Debug1"
"Windows 10 Debug2"
```

ただしより正確な文字列は、次のようなブート選択がはるかに簡単。

```
"Windows 10 kdnet"
"Windows 10 NullModem"
```

**注**  デバッグ用のブート エントリを構成するとき ([/debug/debugport](https://msdn.microsoft.com/library/windows/hardware/ff556253)) または緊急管理サービス (EMS) 用 ([リダイレクト/](https://msdn.microsoft.com/library/windows/hardware/ff557180)) x86-または x64 ベースのシステムでは、ブート ローダーがかっこで囲まれた語句を追加します (\[デバッガーを有効になっている\]または\[ems を有効になっている\]) ブート メニューに表示されるフレンドリ名にします。
ただし、ブート ローダーは、フレンドリ名と一緒のかっこで囲まれた語句は 70 文字を超えたときに、ブート メニューから、かっこで囲まれた語句を省略します。 かっこで囲まれた語句を復元するには、フレンドリ名を短きます。

Boot.ini ファイルでのブート エントリのフレンドリ名を変更するには、Bootcfg を使用するか、メモ帳で Boot.ini ファイルを編集することができます。 EFI NVRAM にブート オプションを格納するシステムで、Bootcfg を使用します。

Windows のブート エントリのフレンドリ名を変更するには、BCDEdit を使用します。 

> [!CAUTION]
> ブート構成の更新には、管理者特権が必要です。 いくつかのブート エントリのオプションを変更すると、コンピューターをしなくなる可能性があります。 


## <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>BCDEdit を使用してください。

ブート エントリの説明を変更するには、ブート メニューに表示するときに使用することができます、 **/set** *IDdescription*オプション。 コマンドは、次の構文を使用します。 ID は、ブート エントリ (またはのいずれかのよく知られている識別子 {0} 現在}) に関連付けられている GUID です。

> [!NOTE]
> 使用する場合[Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=108518)、たとえばブート エントリの識別子を囲む引用符を使用する必要があります: **"{49916baf-0e08-11db-9af4-000bdbd316a0}"** または **"{current}"**.


```console
bcdedit /set ID description "The new description"
```

例:

```console
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} description "Windows 10 NullModem"
```

現在実行中のオペレーティング システムに対応するブート エントリの説明を変更するには、次の例を使用します。

```console
bcdedit /set {current} description "Windows 10 NullModem"
```

既存ブート エントリを使用して、コピーするときに、説明を変更することも、 **/d**オプション。

```console
bcdedit /copy {current} /d "Windows 10 NullModem"
```



## <a name="span-idusingbootcfgspanspan-idusingbootcfgspanusing-bootcfg"></a><span id="using_bootcfg"></span><span id="USING_BOOTCFG"></span>Bootcfg を使用します。

Bootcfg でエントリをコピー中にのみ、ブート エントリのフレンドリ名を変更できます。 使用、Bootcfg **コピー/** エントリをコピーし、そのフレンドリ名を変更するスイッチ。

次の Bootcfg コマンドは、新しいエントリを作成する最初のブート エントリをコピーします。 **/ID**スイッチがコピーされるエントリの行番号を指定します。 **/D** (説明) スイッチを新しく作成されたエントリのフレンドリ名を指定します。

```console
bootcfg /copy /ID 1 /d "Windows 10 Debug"
```

Bootcfg を使用して完全な手順については、ヘルプとサポート サービスを参照してください。 例については、次を参照してください。[ブート パラメーターを使用して](using-boot-parameters.md)します。

## <a name="span-ideditingthebootinifilespanspan-ideditingthebootinifilespanediting-the-bootini-file"></a><span id="editing_the_boot_ini_file"></span><span id="EDITING_THE_BOOT_INI_FILE"></span>Boot.ini ファイルの編集

Boot.ini ファイルでは、ブート エントリのフレンドリ名は引用符でブート エントリに表示されます。

たとえば、Boot.ini ファイルから次の例では、Microsoft Windows 10 Professional の重複するブート エントリがあります。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```

ブート エントリのフレンドリ名を変更するには、ブート エントリの引用符で囲まれた文字列を入力します。 次の例では、最初のエントリはデバッグについては、カスタマイズ可能なため、名前が Windows 10 のデバッグに変更されます。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Windows 10 Debug" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```

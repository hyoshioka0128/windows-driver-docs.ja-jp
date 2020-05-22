---
title: ブート エントリのフレンドリ名の変更
description: ブート エントリのフレンドリ名の変更
ms.assetid: 28f4f449-9027-453e-877a-d656539296c0
keywords:
- 名前 WDK ブートオプション
- フレンドリ名 WDK ブートオプション
- ブートエントリの名前の変更 WDK
- Boot.ini ファイルの WDK、フレンドリ名
- ブートオプション WDK、フレンドリ名
ms.date: 01/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: d482ba1ffe09de6a900b0a939f08fb88e54cbf01
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769642"
---
# <a name="changing-the-friendly-name-of-a-boot-entry"></a>ブート エントリのフレンドリ名の変更


Windows では、Windows ブートマネージャーに表示される項目は、各ブートエントリの説明です。

通常、ブートエントリをコピーしたら、新しく作成されたエントリのフレンドリ名を変更して、元のエントリと区別します。

また、わかりやすい名前を変更して、カスタマイズされたブートエントリを簡単に認識できるようにすることもできます。 エントリを正確に記述する文字列を使用すると、かなりの時間と労力を節約できます。

たとえば、次のわかりやすい名前の文字列では、値がほとんど追加されません。

```
"Windows 10 Debug1"
"Windows 10 Debug2"
```

ただし、次に示すように、より正確な文字列を使用すると、ブートの選択がより簡単になります。

```
"Windows 10 kdnet"
"Windows 10 NullModem"
```

**メモ**   ブートエントリが x86 または x64 ベースのシステムでデバッグ用に構成されている場合 ([/debug/debugport](https://docs.microsoft.com/windows-hardware/drivers/devtest/-debug))、または緊急管理サービス ([ems) の](https://docs.microsoft.com/windows-hardware/drivers/devtest/-redirect)場合は、ブートローダーによって、 \[ \] \[ \] ブートメニューに表示されるフレンドリ名に角かっこで囲まれた語句 (debugger enabled または ems enabled) が追加されます。
ただし、ブートローダーは、表示名と角かっこで囲まれた語句が70文字を超える場合に、ブートメニューから角かっこで囲まれた語句を省略します。 かっこで囲まれた語句を復元するには、フレンドリ名を短くします。

Boot.ini ファイルのブートエントリのフレンドリ名を変更するには、Bootcfg を使用するか、またはメモ帳で boot.ini ファイルを編集します。 ブートオプションを EFI NVRAM に格納するシステムでは、Bootcfg を使用します。

Windows のブートエントリのフレンドリ名を変更するには、BCDEdit を使用します。 

> [!CAUTION]
> ブート構成を更新するには、管理者特権が必要です。 一部のブートエントリオプションを変更すると、コンピューターが動作しなくなる可能性があります。 


## <a name="span-idusing_bcdeditspanspan-idusing_bcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>BCDEdit の使用

ブートメニューに表示されるブートエントリの説明を変更するには、 **/Set** *iddescription*オプションを使用します。 このコマンドでは、次の構文を使用します。 ID は、ブートエントリに関連付けられている GUID (または既知の識別子の1つ ({current} など) です。

> [!NOTE]
> [Windows PowerShell](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/?view=powershell-6)を使用している場合は、ブートエントリ識別子を引用符で囲む必要があります。例: **"{49916baf08 e08-11db9af4000bdbd316a0}"** または **"{current}"**。


```console
bcdedit /set ID description "The new description"
```

次に例を示します。

```console
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} description "Windows 10 NullModem"
```

現在実行されているオペレーティングシステムに対応するブートエントリの説明を変更するには、次の例を使用します。

```console
bcdedit /set {current} description "Windows 10 NullModem"
```

また、 **/d**オプションを使用して既存のブートエントリをコピーするときに、説明を変更することもできます。

```console
bcdedit /copy {current} /d "Windows 10 NullModem"
```



## <a name="span-idusing_bootcfgspanspan-idusing_bootcfgspanusing-bootcfg"></a><span id="using_bootcfg"></span><span id="USING_BOOTCFG"></span>Bootcfg の使用

Bootcfg では、エントリをコピーするときにのみ、ブートエントリのフレンドリ名を変更できます。 Bootcfg **/copy**スイッチを使用してエントリをコピーし、そのフレンドリ名を変更します。

次の Bootcfg コマンドを実行すると、最初のブートエントリがコピーされ、新しいエントリが作成されます。 **/Id**スイッチは、コピーするエントリの行番号を指定します。 **/D** (説明) スイッチは、新しく作成されたエントリのフレンドリ名を指定します。

```console
bootcfg /copy /ID 1 /d "Windows 10 Debug"
```

Bootcfg を使用する手順の詳細については、「ヘルプとサポートサービス」を参照してください。 例については、「[ブートパラメーターの使用](using-boot-parameters.md)」を参照してください。

## <a name="span-idediting_the_boot_ini_filespanspan-idediting_the_boot_ini_filespanediting-the-bootini-file"></a><span id="editing_the_boot_ini_file"></span><span id="EDITING_THE_BOOT_INI_FILE"></span>Boot.ini ファイルの編集

Boot.ini ファイルでは、ブートエントリのフレンドリ名が引用符で囲まれたブートエントリに表示されます。

たとえば、boot.ini ファイルの次の例では、Microsoft Windows 10 Professional のブートエントリが重複しています。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```

ブートエントリのフレンドリ名を変更するには、ブートエントリに引用符で囲まれた文字列を入力します。 次の例では、最初のエントリがデバッグ用にカスタマイズされているため、名前は Windows 10 デバッグに変更されます。

```console
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Windows 10 Debug" /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows 10 Professional" /fastdetect
```

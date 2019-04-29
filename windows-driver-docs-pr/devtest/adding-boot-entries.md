---
title: ブート エントリの追加
description: Windows Vista 以降のブート エントリ、Windows Server 2008 以降、および Windows 回復環境の追加
ms.assetid: 5027d7ea-6f8b-435a-849f-06727068d18b
keywords:
- ブート オプション WDK、ブート エントリを追加します。
- WDK のブート エントリ
- ブート エントリを追加します。
- Boot.ini ファイル WDK、ブート エントリを追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 674a3afeb59ff74b5830d2350267d435fc507da3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332052"
---
# <a name="adding-boot-entries"></a>ブート エントリの追加


オペレーティング システムのブート オプションをカスタマイズするのには、最初の手順は、新しいを追加する*ブート エントリの*オペレーティング システム。 A*ブート エントリの*は、オペレーティング システムまたは起動可能なプログラムの読み込み構成を定義するためのオプションのセットです。

オペレーティング システムは、それぞれ異なる一連のブート パラメーターを持つ複数のブート エントリがあることができます。 Windows インストーラーは、オペレーティング システムをインストールして、ブート オプションを編集して、オペレーティング システムのカスタマイズされたブート エントリを作成するときに、標準のブート エントリを作成します。

追加、削除、および Windows インストーラーを作成したブート エントリのオプションを変更することができます。 ただし、標準のエントリを保持し、代わりに、カスタマイズに別個のエントリを追加することをお勧めです。

ブート エントリを追加するには、既存のブート エントリをコピーして、コピーを変更します。

このトピックでは、Windows Vista 以降、Windows Server 2008 以降と Windows 回復環境に当てはまります。

## 新しいブート エントリを追加します。 <a name="adding-a-new-boot-entry-in-windows-vista-and-later"></a>

Windows、BCDEdit を使用して、ブート オプションを変更します。 新しいブート エントリを追加するには、管理者特権でコマンド プロンプト ウィンドウを開きます (を右クリックして**コマンド プロンプト**クリック**管理者として実行**ショートカット メニューから)。

**注**  BCDEdit のオプションを無効にするか、またはコンピューターの BitLocker とセキュア ブートを中断する必要がありますを設定する前にします。

 

新しいブート エントリを作成する最も簡単な方法では、既存のエントリをコピーし、必要に応じて変更します。 これを行うに BCDEdit を使用して、 **コピー/** オプション。 たとえば、次のコマンドで BCDEdit 最後に使用した Microsoft Windows のブート エントリをコピーとして識別された boot Windows、 **{現在}**、新しいブート エントリを作成します。 **/D**オプションの説明は、新しいブート エントリの名前として DebugEntry を指定します。

```
bcdedit /copy {current} /d "DebugEntry"
```

コマンドが成功すると、BCDEdit には、次のようなメッセージが表示されます。

```
The entry was successfully copied to {49916baf-0e08-11db-9af4-000bdbd316a0}.
```

ブート メニューに表示されるブート ローダー エントリをコピーする場合、コピーがブート メニューの最後の項目として自動的に追加します。

上記のメッセージの GUID (中かっこの間に表示される ({})) は、新しいブート エントリの識別子です。 **コピー/** オプションのブート エントリの新しい GUID を作成します。 識別子を使用して、後続のすべての BCDEdit コマンドでエントリを表します。

コマンドが失敗した場合、必ず管理者特権でコマンド プロンプト ウィンドウで実行していることと、すべてのコマンド パラメーターのスペルが正しいことを囲む中かっこを含む **{現在}** します。

使用してブート エントリを追加することも、 **/create**オプション。 ブート エントリの種類に関する追加情報を提供する必要があるために、このメソッドは困難です。 指定する必要があります、 **/アプリケーション**、 **/inherit**、または **/device**オプション。 たとえば、"My Windows Vista"と呼ばれる新しいオペレーティング システムのブート エントリの作成は、次のように。

```
bcdedit /create /d "My Windows Vista" /application osloader
```

使用すると、 **/create**オプション、新しいブート ローダーのエントリは自動的にブート メニューに追加されません。 **/Create**オプションのブート エントリの新しい GUID を作成します。 使用して、ブート メニューに新しいブート エントリを追加する必要があります、 **/displayorder**オプション。 ブート ローダーのエントリは、任意の順序で配置できます。

については、 **/create**コマンドのパラメーター、型**bcdedit/でしょうか。/create**コマンド プロンプト ウィンドウでします。

## ブート メニューの編集 <a name="editing-the-boot-menu-in-windows-vista-and-later"></a>

、Windows で新しいブート ローダーのエントリはブート メニューに自動的に追加されません。 ブート ローダーのエントリは、任意の順序で配置できます。

使用することができます、 **/displayorder**をブート マネージャーが複数のブート メニューにブート エントリを表示する順序を設定するオプション。 コマンドでは、次の構文があります。

```
bcdedit /displayorder {ID} {ID} ...
```

ID がブート エントリまたは予約された識別子の GUID がなど **{現在}**)。 各識別子は、スペースで区切ります。 中かっこを含めるようにしてください ({})。

たとえば後のブート メニューに DebugEntry ブート エントリを追加する、 **{現在}** エントリ、次のコマンドを使用して (を使用してください`'{guid}'`Windows PowerShell で)。

```
bcdedit /displayorder {current} {49916baf-0e08-11db-9af4-000bdbd316a0}
```

オプションを使用することもできます。 **/addlast、/addfirst**、および **/remove**を注文し、メニューから項目を削除します。 たとえば、次のコマンドは、メニューの最後の項目として DebugEntry ブート エントリを追加します。

```
bcdedit /displayorder {49916baf-0e08-11db-9af4-000bdbd316a0} /addlast
```

## 削除して、ブート エントリを削除します。 <a name="removing-a-boot-entry-in-windows-vista-and-later"></a>

次のコマンドでは、ブート メニューから {49916baf-0e08-11db-9af4-000bdbd316a0} ブート エントリの項目を削除します。

```
bcdedit /displayorder {49916baf-0e08-11db-9af4-000bdbd316a0} /remove
```

使用して、指定されたブート エントリを削除するときに、 **/displayorder**と **/remove**オプション、ブート エントリは、ブート メニューから削除されますが、BCD ストアに存在します。 ブート メニューから、ストアから完全にブート ローダーのエントリを削除するには、使用、 **/delete**オプション。

```
bcdedit /delete {49916baf-0e08-11db-9af4-000bdbd316a0}
```

表示順序が正しいことを確認するには、次のコマンドを使用します。

```
bcdedit
```

入力すると**bcdedit**追加パラメーターを指定せず BCDEdit が表示されます、ブート マネージャ エントリとブート ローダーのエントリは、メニューに表示される順序で。

Windows ブート マネージャ エントリには、次の例のようにブート メニューの表示順序も含まれています。

```
## Windows Boot Manager
identifier              {bootmgr}
device                  partition=C:
description             Windows Boot Manager
locale                  en-US
inherit                 {globalsettings}
default                 {current}
displayorder            {current}
                        {18b123cd-2bf6-11db-bfae-00e018e2b8db}
toolsdisplayorder       {memdiag}
timeout                 30

## Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             Microsoft Windows Vista
locale                  en-US
inherit                 {bootloadersettings}
osdevice                partition=C:
systemroot              \Windows
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn

## Windows Boot Loader
-------------------
identifier              {18b123cd-2bf6-11db-bfae-00e018e2b8db}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             Debugger Boot
locale                  en-US
inherit                 {bootloadersettings}
osdevice                partition=C:
systemroot              \Windows
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn
debug                   Yes
```

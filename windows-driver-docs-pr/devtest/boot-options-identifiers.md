---
title: ブート オプションの識別子
description: ブート オプションの識別子をについて説明します。
ms.assetid: bd0caf3f-bb35-4242-a10a-4efa91a21797
keywords:
- ブート オプション Windows
- 識別子
- 既定値 (default)
- WDK のブート オプション
ms.date: 04/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 472167b0023469065200a42dac3d0fc0a26e1522
ms.sourcegitcommit: ff586f2b9ef79af53e3317973f087eee7babf083
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "64402108"
---
# <a name="boot-options-identifiers"></a>ブート オプションの識別子

Bcdedit のコマンドの多くには、識別子が必要です。 識別子は、ブート設定ストアに含まれているエントリを一意に識別します。 

Bcdedit/enum を使用すると、識別子を表示します。

```console
C:\>bcdedit /enum

Windows Boot Manager
--------------------
identifier              {bootmgr}

...

Windows Boot Loader
-------------------
identifier              {current}

```

既知の識別子では、いくつかのエントリを識別できます。 エントリに既知の識別子がある場合は、bcdedit に表示出力/v コマンド ライン スイッチを使用しない場合。 詳細については、次のように実行します。"bcdedit/でしょうか。 /v"。

一般的な既知の識別子はよく使用されます。

| 識別子           | 説明
|-----------------------|----------------------------------------------------------------------|
|    {default}          |     ブート マネージャの既定のアプリケーション エントリに対応する仮想識別子を指定します。 | 
|    {current}          |     現在実行中のオペレーティング システムのオペレーティング システムのブート アプリケーション エントリに対応する仮想識別子を指定します。 |
|    {bootmgr}          |     Windows ブート マネージャーのアプリケーション エントリを指定します。 |

これらの一般的なよく知られている識別子は、ブート アプリケーション エントリによって継承できます。

| 識別子           | 説明
|-----------------------|----------------------------------------------------------------------|
|    {globalsettings}    |    すべてのブート アプリケーション エントリに継承する必要がありますのグローバル設定のコレクションが含まれています。 |
|   {bootloadersettings} |   すべてのブート ローダー アプリケーション エントリに継承する必要がありますのグローバル設定のコレクションが含まれています。 |

これらのよく知られている識別子は、使用可能なも。

| 識別子           | 説明
|-----------------------|----------------------------------------------------------------------|
|    {dbgsettings}       |    ブート アプリケーション エントリを継承できるグローバルなデバッガ設定を格納します。 |
|    {hypervisorsettings} |   任意の OS ローダーのエントリが継承できるハイパーバイザー設定を格納します。 |
|    {emssettings}       |  ブート アプリケーション エントリを継承できるグローバルの緊急管理サービス設定が含まれています。 |
|    {resumeloadersettings} | により、すべて継承する必要があるグローバル設定のコレクションを含む Windows がアプリケーションのエントリは休止状態から再開します。 |
|    {badmemory}         |    ブート アプリケーション エントリに継承できるグローバル RAM 欠陥のリストが含まれています。 |
|   {memdiag}           |    メモリ診断アプリケーションのエントリを指定します。 |
|    {ramdiskoptions}    |   RAM ディスク デバイスのブート マネージャで必要な追加のオプションが含まれています。 |

これらのよく知られている識別子は、Windows の以前のバージョンと共に使用されます。

| 識別子           | 説明
|-----------------------|----------------------------------------------------------------------|
|    {ntldr}            |     Windows Vista より前のオペレーティング システムの起動に使用できる OS ローダー (Ntldr) を指定します。|
|    {fwbootmgr}        |     具体的には、拡張ファームウェア インターフェイス (EFI) 仕様を実装するシステム上のファームウェア ブート マネージャ エントリを指定します。|

## <a name="boot-option-inheritance"></a>ブート オプションの継承

一部のブート設定を継承できます。 これにより、グループの設定、休止状態から再開するときなど、さまざまなブートのシナリオで使用します。

コマンドを bcdedit/enum オプションを使用して、任意の識別子に関する情報を表示します。

次の例で情報を表示する {0} 現在} の識別子を示しています {bootloadersettings} を継承します。

```console
C:\>bcdedit /enum {current}

Windows Boot Loader
-------------------
identifier              {current}
device                  partition=C:
path                    \WINDOWS\system32\winload.exe
description             Windows 10
locale                  en-US
inherit                 {bootloadersettings}
...
```

Bcdedit/enum コマンドを使用して、どの設定が継承されます。

{Globalsettings} 以下の例で継承 {dbgsettings} での設定に従う {emssettings} と {badmemory}。

```console
C:\>bcdedit /enum {globalsettings}

Global Settings
---------------
identifier              {globalsettings}
inherit                 {dbgsettings}
                        {emssettings}
                        {badmemory}
```

Bcdedit/enum を継承 オプションを使用して、継承に関する情報を表示します。

次の例では、{bootloadersettings} が {globalsettings} を継承し、{hypervisorsettings} と {resumeloadersettings} {globalsettings} を継承します。

```console
C:\>bcdedit /enum inherit

...

Boot Loader Settings
--------------------
identifier              {bootloadersettings}
inherit                 {globalsettings}
                        {hypervisorsettings}


Resume Loader Settings
----------------------
identifier              {resumeloadersettings}
inherit                 {globalsettings}

...

```

Bcdedit を使用して、すべての設定を表示する/all コマンド。  

```console
C:\>bcdedit /enum all

Windows Boot Manager
--------------------
identifier              {bootmgr}
device                  partition=\Device\HarddiskVolume1
description             Windows Boot Manager

...

```

## <a name="guids-and-identifiers"></a>Guid と Id

識別子は、グローバルに一意の識別子または GUID を使用します。 GUID は、次の形式では、"x"が 16 進数を表します。 Guid の操作が間違いであるため、{current} など、識別子の英語名を使用して Windows 用に構成された現在のブート情報で操作することをお勧めします。

```guid
{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}
```

次に、例を示します。

```guid
{d2b69192-8f14-11da-a31f-ea816ab185e9}
```
ハイフン (-) と GUID の前後に中かっこの位置が必要です。

識別子に関連付けられている Guid を表示するのにには、bcdedit/enum/v を使用します。

```console
C:\>bcdedit /enum /v

Windows Boot Manager
--------------------
identifier              {9dea862c-5cdd-4e70-acc1-f32b344d4795}
device                  partition=\Device\HarddiskVolume1
description             Windows Boot Manager
locale                  en-US
inherit                 {7ea2e1ac-2e61-4728-aaa3-896d9d0a9f0e}
```

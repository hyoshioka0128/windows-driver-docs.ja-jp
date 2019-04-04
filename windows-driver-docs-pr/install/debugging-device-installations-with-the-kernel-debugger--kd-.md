---
title: カーネル デバッガー (KD) でのデバイスのインストールのデバッグ
description: カーネル デバッガー (KD) でのデバイスのインストールのデバッグ
ms.assetid: 0967d375-2602-44d2-b4ac-8d1e112afc3f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67a236e3391cae97bd201fe6f6d8790b2a4a4923
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577820"
---
# <a name="debugging-device-installations-with-the-kernel-debugger-kd"></a>カーネル デバッガー (KD) でのデバイスのインストールのデバッグ


以降、Windows Vista では、プラグ アンド プレイ (PnP) マネージャー、システムで新しいデバイスを検出した場合、オペレーティング システムの起動時、デバイスのインストールのホスト プロセス (*DrvInst.exe*) を検索し、デバイスのドライバーをインストールします。

デバイスのインストールは、このユーザー モード プロセス内で発生するためは、通常は」の説明に従って、ユーザー モード デバッガーを使用する最も簡単な[ユーザー モード デバッガーでのデバイス インストールのデバッグ](debugging-device-installations-with-a-user-mode-debugger.md)します。 場合によっては、ただし、役立つがあります、カーネル デバッガー (KD) を使用して、ユーザー モード デバイスのインストール プロセスを監視します。

などの KD を使用すると、ユーザー モード デバイスのインストールのデバッグ中に、次の操作にすることができます。

-   使用して、カーネル モードの問題を同時にデバッグ! devnode、! devobj、!、drvobj! irp、およびその他の KD 拡張機能。

-   KD 拡張機能を使用して複数のデバッガーを管理することがなく他のユーザー モード プロセスを監視します。 プロセスまたは .process/p です。

KD と他のデバッグ ツールの詳細については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。

**DebugInstall**レジストリ値がデバッグのサポート システムで有効になっているデバイスのインストールの種類を指定します。 このレジストリ値の詳細については、[デバイス インストールのデバッグのサポートを有効にする](enabling-support-for-debugging-device-installations.md)を参照してください。

ときに、 **DebugInstall**レジストリ値が 1 に設定*DrvInst.exe*最初は、カーネル デバッガーが有効になっているおよびデバッガーに中断されるまでに現在接続されているを確認します。 この中断が行われた後は、現在のプロセスのユーザー モードのモジュールでブレークポイントを設定できます。 例:

```cpp
kd> .reload /user
kd> bp /p @$proc setupapi!SetupDiCallClassInstaller
```

これは、SETUPAPI ルーチンにブレークポイントを設定します。現在のプロセスのみの SetupDiCallClassInstaller します。

開発者にとって、[ドライバー パッケージ](driver-packages.md)、通常、デバイスのインストール中に、クラスのインストーラー ファイルまたは DLL の共同インストーラーの動作をデバッグする最も好ましいことです。 ただし、 *DrvInst.exe*デバッガー、クラスのインストーラーや共同インストーラー Dll ドライバー パッケージからに区切りが読み込まれていません。 ユーザー モード デバッガーでプロセスにユーザー モードのモジュールが読み込まれるときに、デバッガーの例外を設定する機能をサポートしていますが、"sx e %ld"コマンド、カーネル デバッガーには、そのコマンドを使用してカーネル モードのモジュールのみがサポートされます。

次のコード例では、「デバッガー コマンド プログラム」が、現在のプロセスに、特定のクラスのインストーラー ファイルまたは共同インストーラーの読み込みを監視する方法を示します。 この例で、デバッガー コマンド プログラムにブレークポイントを設定 (CoInstallerProc) のメイン エントリ ポイントの*Mycoinst.dll*共同インストーラー。

```cpp
file: Z:\bpcoinst.txt

r $t1 = 0
!for_each_module .if ($spat("@#ModuleName", "mycoinst*") = 0) {r $t1 = 1}
.if (not @$t1 = 0) {.echo mycoinst is loaded, set bp on mycoinst!CoInstallerProc } .else {.echo mycoinst not loaded}
.if (not @$t1 = 0) {.reload mycoinst.dll}
.if (not @$t1 = 0) {bp[0x20] /p @$proc mycoinst!CoInstallerProc } .else {bc[0x20]}
```

現在のプロセスに読み込まれたモジュールのリストを実行すると、デバッガー コマンド プログラムがチェックされ*Mycoinst.dll*します。 DLL が読み込まれたこの共同インストーラーの後に、デバッガーは CoInstallerProc のエントリ ポイント関数に (よく知られているブレークポイントの ID) を持つブレークポイントを設定することにします。

によって開始されたデバッグ ブレークから始まる、 *DrvInst.exe*ホスト プロセスをする必要があります最初にブレークポイントを設定、呼び出しの戻り値のアドレスを*DrvInst.exe*カーネル デバッガーに割り込んだします。 このブレークポイントをすべてオフはブレークポイントが、デバイスのインストール中に設定され、実行を続行します。

```cpp
DRVINST.EXE: Entering debugger during PnP device installation.
Device instance = "X\Y\Z" ...

Break instruction exception - code 80000003 (first chance)
010117b7 cc               int     3

kd> bp[0x13] /p @$proc @$ra "bc *;g"
```

次に、デバイスのインストール中に適切なタイミングで実行するデバッガー コマンド プログラムで、コマンドを許可するようにプロセス内でブレークポイントをいくつかを設定する必要があります。

つまり、新しい DLL が現在のプロセスに読み込まれるときにいつでもクラス インストーラーまたは共同インストーラー DLL エントリ ポイントのブレークポイントが設定されているデバイスのインストールの関数が呼び出される前に、デバッガー コマンド プログラムを実行するか後に、LoadLibraryExW への呼び出しが返されます。

```cpp
kd> .reload
kd> bp[0x10] /p @$proc kernel32!LoadLibraryExW "gu;$$><Z:\\bpcoinst.txt;g"
```

プロセス内で LoadLibraryEx 呼び出しごとにプログラムを実行するのではなく (bp\[0x10\])、開発者には、class インストーラーのみと共同インストーラー Dll がプロセスに読み込まれるを実行するように制限できます。 [ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)ルーチンをクラスのインストーラーを呼び出すと、デバイスの登録されている共同インストーラーには、これらの Dll は、その呼び出し中に、プロセスに読み込まれます。

仮定は行われませんについてからこれらの Dll がアンロードされるときにあるため、 *DrvInst.exe*ホスト プロセスを行う必要がありますに加えられたすべての呼び出し中にDLLのエントリポイントを検索するブレークポイントを処理できることを確認して**SetupDiCallClassInstaller**から、 *DrvInst.exe*プロセスをホストします。

```cpp
kd> bd[0x10]
kd> bp[0x11] /p @$proc setupapi!SetupDiCallClassInstaller "be[0x10];bp[0x12] /p @$proc @$ra \"bd[0x10];bc[0x12];g\";g"
kd> g
```

デバッガー コマンド プログラムの実行をブレークポイント (bp\[0x10\]) は、最初に無効になります。 有効になってたびに[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)が呼び出されます (bp\[パターン\])、および実行が続行されます。 デバッガー コマンド プログラム (bp\[0x10\]) ときに無効になって再度**SetupDiCallClassInstaller**自体ルーチンの戻り値のアドレスにブレークポイントを設定して返します (bp\[0x12\]).

デバッガー コマンド プログラムを無効にするブレークポイントもが自動的に消去となるまで実行を継続[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)もう一度、またはインストールされるまで呼び出されますプログラムが完了して、すべてのブレークポイントをクリア (bp\[0x13\])。

上記のブレークポイントを設定した後の実行開始時に mycoinst に対する各呼び出しプロセスが中断されます。CoInstallerProc します。 これにより、中核となるデバイスのインストール中に、クラスのインストーラーまたは共同インストーラー DLL の実行をデバッグすることができます。

既定のインストール プロセスが完了するための期間は 5 分です。 特定の期間内で、プロセスが完了しない場合、プロセスが応答しなくなったことは終了と見なされます。

デバイスのインストール上に配置する既定のタイムアウト制限は、カーネル デバッガーを使用、プロセスをデバッグ中は有効なままでは。 インストール プロセスによって実行される時間が追跡されるため、デバッガーに分割中に、システム上のすべてのプログラムの実行が停止、デバッグ中でないシステムでの場合と同じです。

 

 






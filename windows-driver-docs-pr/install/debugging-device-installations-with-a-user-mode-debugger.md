---
title: ユーザー モード デバッガーによるデバッグ デバイスのインストール
description: ユーザー モード デバッガーによるデバッグ デバイスのインストール
ms.assetid: 34427afb-3303-44ec-a3a7-72f247c5506d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a86b65d148ce509e7e85619775ce7fadd8427728
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532577"
---
# <a name="debugging-device-installations-with-a-user-mode-debugger"></a>ユーザー モード デバッガーによるデバッグ デバイスのインストール


以降、Windows Vista では、プラグ アンド プレイ (PnP) マネージャー、システムで新しいデバイスを検出した場合、オペレーティング システムの起動時、デバイスのインストールのホスト プロセス (*DrvInst.exe*) を検索し、デバイスのドライバーをインストールします。

ユーザー モード デバイスのインストールのホスト プロセスをデバッグする最も効率的な方法は、WinDbg または Visual Studio など、ユーザー モード デバッガーです。 *DrvInst.exe*プロセスは通常ユーザーが介入せずに完了、マイクロソフトの開発者を許可するには、Windows Vista と以降のバージョンの Windows にサポートが追加されて、[ドライバー パッケージ](driver-packages.md)デバイス インストールの主要なステージが処理される前にデバッガーをアタッチします。

ユーザー モード デバッガーや他のデバッグ ツールの詳細については、次を参照してください。 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

**DebugInstall**レジストリ値がデバッグのサポート システムで有効になっているデバイスのインストールの種類を指定します。 このレジストリ値の詳細については、次を参照してください。[デバイス インストールのデバッグのサポートを有効にする](enabling-support-for-debugging-device-installations.md)します。

ときに、 **DebugInstall**レジストリ値が 2 に設定*DrvInst.exe*インストールを続行する前にそのプロセスに接続するユーザー モード デバッガーが待機します。 デバッガーが接続されると、デバッガー自体に、プロセスが中断されます。 デバッガーをアタッチおよび構成のデバッグ中にターゲット システムで、独自の最初のブレークポイントは開始されませんする必要があります。

デバッガーをアタッチしてになど*DrvInst.exe*名。

```cpp
C:\>C:\Debuggers\WinDbg.exe -g -pn DrvInst.exe
```

または、デバッガーがターゲット システムに接続されている場合、次のデバッグ情報が表示されます。

```cpp
DRVINST.EXE: Waiting for debugger on Process ID = 3556 ......
```

これにより、デバッガーに接続する、 *DrvInst.exe*その一意のプロセス ID を使用してプロセス。

```cpp
C:\>C:\Debuggers\WinDbg.exe -g -p 3556
```

ユーザー モード後デバッガーがアタッチされている、 *DrvInst.exe*プロセス、プロセスは、デバッガーが中断されます。

```cpp
Debugger detected!
DRVINST.EXE: Entering debugger during PnP device installation.
Device instance = "X\Y\Z" ...

(d48.5a0): Break instruction exception - code 80000003 (first chance)
eax=7ffde000 ebx=00000000 ecx=00000000 edx=77f745c0 esi=00000000 edi=00000000
eip=77f24584 esp=0105ff74 ebp=0105ffa0 iopl=0         nv up ei pl zr na po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000246
ntdll!DbgBreakPoint:
77f24584 cc               int     3

0:000> |
.  0id: d48attachname: E:\Windows\system32\DrvInst.exe
```

デバイスのインストールの主要な段階が処理されていないため、クラスのインストーラーや共同インストーラーは、デバイスに使用される Dll がまだ読み込まれていません。

ブレークポイントを設定するモジュールと関数の名前が事前にわかっている場合、"bu"のデバッガー コマンドを使用して、その名前を未解決のブレークポイントとして設定できます。 次のコード例は、のメイン エントリ ポイント (CoInstallerProc) の未解決のブレークポイントを設定する方法を示します、 *MyCoinst.dll*共同インストーラー。

```cpp
0:000> bu mycoinst!CoInstallerProc
0:000> bl
 0 eu             0001 (0001) (mycoinst!CoInstallerProc)
```

ときに*MyCoinst.dll*共同インストーラーが読み込まれ、ブレークポイントに到達します。

```cpp
Breakpoint 0 hit
eax=00000001 ebx=00000000 ecx=00000152 edx=00000151 esi=01a57298 edi=00000002
eip=5bcf54f1 esp=0007e204 ebp=0007e580 iopl=0         nv up ei pl nz na pe nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000202
mycoinst!CoInstallerProc:
5bcf54f1 8bff             mov edi,edi
0:000> bl
 0 e 5bcf54f1     0001 (0001)  0:**** mycoinst!CoInstallerProc
```

クラスのインストーラーまたは共同インストーラー DLL ときに、それぞれが読み込みまたはからアンロードを予測する必要がありますいない、 *DrvInst.exe*プロセス。 ただし、モジュールが読み込まれていない場合でも、"bu"を使用して設定されているブレークポイントは残ります。

または、 *DrvInst.exe*時点まで、特定のクラスのインストーラーを実行するプロセスを許可する場合がありますまたはその DLL の読み込みイベントのデバッガーの例外を設定して共同インストーラー DLL がプロセスに読み込まれます。

```cpp
0:000> sxe ld mycoinst.dll
```

0:000&gt; g

モジュールが読み込まれた後は、DLL 内でブレークポイントを設定できます。 次に、例を示します。

```cpp
ModLoad: 5bcf0000 5bd05000   C:\WINDOWS\system32\mycoinst.dll
eax=00000000 ebx=00000000 ecx=011b0000 edx=7c90eb94 esi=00000000 edi=00000000
eip=7c90eb94 esp=0007da54 ebp=0007db48 iopl=0         nv up ei ng nz ac po nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000296
ntdll!KiFastSystemCallRet:
7c90eb94 c3               ret
0:000> .reload mycoinst.dll
0:000> x mycoinst!*InstallerProc*
5bcf54f1 mycoinst!CoInstallerProc (unsigned int, void *, struct _SP_DEVINFO_DATA *)

0:000> bu mycoinst!CoInstallerProc
0:000> bl
 0 e 3b0649d5     0001 (0001)  0:**** mycoinst!CoInstallerProc
0:000> sxd ld mycoinst.dll
0:000> g
Breakpoint 0 hit
eax=00000001 ebx=00000000 ecx=000001d4 edx=000001d3 esi=000bbac0 edi=00000002
eip=5bcf54f1 esp=0007e204 ebp=0007e580 iopl=0         nv up ei pl nz na pe nc
cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000             efl=00000202
mycoinst!CoInstallerProc:
5bcf54f1 8bff             mov edi,edi
0:000> 
```

ブレークポイントが未解決のブレークポイント (bu) として設定されていたためは設定されたまま、モジュールが読み込まれていない場合でもです。

既定のインストール プロセスが完了するための期間は 5 分です。 特定の期間内で、プロセスが完了しない場合 (停止している応答)、プロセスがハングしていることと、インストール プロセスが終了と見なされます。

ユーザー モード デバッガーがデバイスのインストール プロセス中に、ターゲット システムに接続されている場合、システムには、このタイムアウトは強制されません。 これにより、[ドライバー パッケージ](driver-packages.md)インストール プロセスをデバッグするために必要な時間を費やすの開発者。

 

 






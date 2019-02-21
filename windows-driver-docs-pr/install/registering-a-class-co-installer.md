---
title: クラスの共同インストーラーを登録します。
description: クラスの共同インストーラーを登録します。
ms.assetid: a86a4302-ec37-4117-aa5c-4fa84fbb7902
keywords:
- 共同インストーラー WDK クラスします。
- クラスの co-installer を登録します。
- WDK デバイス インストールのセットアップ-クラス GUID
- CoDeviceInstallers
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db8f5fd54dfac5dd5b0f4f7e9d5fcded5d177a69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558277"
---
# <a name="registering-a-class-co-installer"></a>クラスの共同インストーラーを登録します。





特定のセットアップ クラスのすべてのデバイスの共同インストーラーを登録するには、下には、次のようなレジストリ エントリを作成、 **HKLM\\システム\\CurrentControlSet\\コントロール\\CoDeviceInstallers**サブキー。

```cpp
{setup-class-GUID}: REG_MULTI_SZ : "XyzCoInstall.dll,XyzCoInstallEntryPoint\0\0"
```

システムを作成、 **CoDeviceInstallers**キー。 *セットアップ クラスの GUID*の GUID を指定します、[デバイス セットアップ クラス](device-setup-classes.md)します。 共同インストーラーは、デバイスの 1 つ以上のクラスに適用する場合は、セットアップ クラスごとに個別の値のエントリを作成します。

以前に書き込まれたその他の共同インストーラーを上書きする必要があります、*セットアップ クラスの GUID*キー。 共同インストーラー、文字列の追加、キーの読み取り、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)ボックスの一覧し、キーをレジストリに書き込みます。

省略した場合、 *CoInstallEntryPoint*、既定値は CoDeviceInstall します。

共同インストーラー DLL は、システム ディレクトリにコピーする必要があります。

クラスの共同インストーラーは、ファイルがコピーされているし、レジストリ エントリが作成に関連するデバイスとサービスに対して呼び出されるようにします。

クラスの共同インストーラーを登録するレジストリ エントリを手動で作成するのではなく、次のような INF ファイルを使用して登録できます。

```cpp
[version]
signature = "$Windows NT$"
 
[DestinationDirs]
DefaultDestDir = 11    // DIRID_SYSTEM
 
[DefaultInstall]
CopyFiles = @classXcoinst.dll
AddReg = CoInstaller_AddReg
 
[CoInstaller_AddReg]
HKLM,System\CurrentControlSet\Control\CoDeviceInstallers, \
 {setup-class-GUID},0x00010008, "classXcoinst.dll,classXCoInstaller"
; above line uses the line continuation character ()
```

このサンプルの INF ファイルをコピーする*classXcoinst.dll*システムのディレクトリへエントリになり、*セットアップ クラスの GUID*クラスの下で、 **CoDeviceInstallers**キー。 内のエントリ、 *Xxx*_AddReg セクションが 2 つのフラグを指定します:「00010000」のフラグは、エントリがあるを指定します、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)、「00000008」のフラグは、新しい値がいずれかに追加することを指定します既存の値 (新しい値が文字列の設定がないと) 場合。

またはを呼び出すアプリケーションを右クリックしてインストールして、クラスの共同インストーラーを登録します。 このような、INF をアクティブにできる**SetupInstallFromInfSection**します。

 

 






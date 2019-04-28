---
title: デバイスに固有の共同インストーラーの登録
description: デバイスに固有の共同インストーラーの登録
ms.assetid: 7a80bc60-e2f0-4447-bd73-4ce12fcfc2e3
keywords:
- デバイスに固有の共同インストーラー WDK デバイスのインストール
- デバイスに固有の co-installer を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ab7e8a3ff040d26938a099d52b91ff6d58ad263
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373892"
---
# <a name="registering-a-device-specific-co-installer"></a>デバイスに固有の共同インストーラーの登録





デバイスに固有の共同インストーラーを登録するには、デバイスの INF ファイルに次のセクションを追加します。

```cpp
;  :
;  :
[DestinationDirs]
XxxCopyFilesSection = 11                \\DIRID_SYSTEM
                                        \\ Xxx = driver or dev. prefix
;  :
;  :
[XxxInstall.OS-platform.CoInstallers]   \\ OS-platform is optional
CopyFiles = XxxCopyFilesSection
AddReg = Xxx.OS-platform.CoInstallers_AddReg
 
[XxxCopyFilesSection]
XxxCoInstall.dll
 
[Xxx.OS-platform.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"XxxCoInstall.dll, \
 XxxCoInstallEntryPoint"
```

内のエントリ、 **DestinationDirs**セクションでは、ファイルで表示されていることを指定します、 *Xxx*CopyFilesSection はシステム ディレクトリにコピーされます。 *Xxx*プレフィックスは、ドライバー、デバイスまたはデバイス (たとえば、cdrom_CopyFilesSection) のグループを識別します。 *Xxx*プレフィックスは一意である必要があります。

*インストール セクション名*共同インストーラーのエントリは省略可能な OS/アーキテクチャの拡張機能 (たとえば、cdrom_install で修飾することができます。NTx86.CoInstallers)。 詳細については、次を参照してください。 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)します。

内のエントリ、 <em>Xxx</em>**_AddReg**セクションを作成し、 **CoInstallers32**デバイスのエントリの値*ドライバー キー*します。 エントリには、共同インストーラー DLL と、必要に応じて、特定のエントリ ポイントが含まれています。 エントリ ポイントを省略すると、既定では CoDeviceInstall です。 16 進数のフラグ パラメーター (0x00010000) は、これを指定します、 [REG_MULTI_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)エントリの値します。

デバイスの 1 つ以上のデバイスに固有の共同インストーラーを登録するには、各共同インストーラーのファイルをコピーし、レジストリ エントリでは、複数の文字列が含まれます。 たとえば、2 つの co-installer を登録するには、INF セクションでは、次のようなを作成します。

```cpp
;   :
;   :
[DestinationDirs]
XxxCopyFilesSection = 11                \\DIRID_SYSTEM
                                        \\ Xxx = driver or dev. prefix
;   :
;   :
[XxxInstall.OS-platform.CoInstallers]   \\ OS-platform is optional
CopyFiles = XxxCopyFilesSection
AddReg = Xxx.OS-platform.CoInstallers_AddReg
 
[XxxCopyFilesSection]
XxxCoInstall.dll                         \\ copy 1st coinst. file
YyyCoInstall.dll                         \\ copy 2nd coinst. file
 
[Xxx.OS-platform.CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,                 \
    "XxxCoInstall.dll, XxxCoInstallEntryPoint", \
    "YyyCoInstall.dll, YyyCoInstallEntryPoint"
                                         \\ add both to registry
```

デバイスに固有の共同インストーラーは、共同インストーラー INF セクションが処理されるときに、デバイスのインストールの処理中に登録されます。 SetupAPI は、インストール プロセスの以降の各ステップで、共同インストーラーを呼び出します。 デバイスの 1 つ以上の共同インストーラーが登録されると場合、SetupAPI はレジストリ内で表示される順序でこれらを呼び出します。

 

 






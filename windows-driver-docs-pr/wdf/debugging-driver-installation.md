---
title: KMDF および UMDF ドライバーのインストールのトラブルシューティング
description: KMDF および UMDF ドライバーのインストールのトラブルシューティング
ms.assetid: b0b71adc-cb6e-4b84-a5bf-bd1269bcf315
keywords:
- カーネルモードドライバーフレームワーク WDK、ドライバーのインストール
- フレームワークベースのドライバー WDK KMDF, インストール
- INF ファイル WDK KMDF、デバッグ
- ドライバーのデバッグ WDK KMDF、インストール
- WDK KMDF ドライバーのデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 411840c0587fc347baaddacc7fdcb5aba055b9d8
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261439"
---
# <a name="troubleshooting-kmdf-and-umdf-driver-installation"></a>KMDF および UMDF ドライバーのインストールのトラブルシューティング


フレームワークの共同インストーラーによって、デバッグメッセージが作成されます。 これらのメッセージは、デバッガーで確認できます。

また、共同インストーラーによって、デバッグメッセージが[セットアップアクションログ](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi-text-logs)( *% windir%\\setupact .log*) に書き込まれます。 セットアップアクションログには、ドライバーの INF ファイルで指定されているバージョンの共同インストーラーとドライバーが含まれています。 これらが想定どおりであることを確認する必要があります。

## <a name="examining-kmdf-installation"></a>KMDF のインストールを確認しています


セットアップアクションログの次の出力は、KMDF ドライバーが正常にインストールされた場合のものです。

```cpp
WdfCoInstaller: DIF_INSTALLDEVICE: Pre-Processing
WdfCoInstaller: ReadComponents:  WdfSection for Driver Service ECHO using KMDF lib version Major 0x1, minor 0x9 
WdfCoInstaller: DIF_INSTALLDEVICE: Coinstaller version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF in-memory version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF on-disk version: 1.9.7100
WdfCoInstaller: Service Wdf01000 is running
WdfCoInstaller: DIF_INSTALLDEVICE: Update is not required. The on-disk KMDF version is newer than or same as the version of the coinstaller
WdfCoInstaller: DIF_INSTALLDEVICE: Post-Processing
```

上記のシナリオでは、更新は必要ありませんでした。これは、ディスク上のバージョンとメモリ内のフレームワークのバージョンが KMDF 1.9 であり、これは同じバージョンの共同インストーラーです。

次の出力について考えてみます。これは、インストールが失敗したことを示します。

```cpp
WdfCoInstaller: ReadComponents:  WdfSection for Driver Service ECHO using KMDF lib version Major 0x1, minor 0x9  
WdfCoInstaller: DIF_INSTALLDEVICE: Coinstaller version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF in-memory version: 1.7.6000
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF on-disk version: 1.7.6000
WdfCoInstaller: Service Wdf01000 is running
WdfCoInstaller: DIF_INSTALLDEVICE: Reboot is required, because the in-memory KMDF version is older than the coinstaller's version.
WdfCoInstaller: DIF_INSTALLDEVICE: Update is required, because the on-disk KMDF version is older than the coinstaller
WdfCoInstaller: VerifyMSRoot: exit: error(0) The operation completed successfully.
WdfCoInstaller: Invoking "D:\Windows\system32\wusa.exe "D:\Windows\Temp\WdfTemp\Microsoft Kernel-Mode Driver Framework Install-v1.9-Vista.msu" /quiet /norestart".
WdfCoInstaller: The update process returned error code :error(265) <no error text>. 
WdfCoInstaller: For additional information please look at the log files %windir%\windowsupdate.log and %windir%\Logs\CBS\CBS.log
```

このシナリオでは、KMDF ランタイムのメモリ内バージョンとディスク上のバージョンが共同インストーラーのバージョンよりも古いため、更新と再起動の両方が必要でした。 ただし、更新は失敗しました。 共同インストーラーは、エラーに関する詳細情報が記載されている追加のログファイルを参照します。

また、システムイベントログで、KMDF ドライバーのランタイムライブラリへの動的バインドに関連するエラーを確認することもできます。 このようなエラーが発生すると、システムイベントログに**Wdf**&lt;*MajorVersionNumber*&gt;&lt;*minorversionnumber,* &gt; エントリが生成されることがあります。 この場合は、コンピューターを再起動します。 また、 *% windir%\\system32\\drivers*フォルダーから**Wdf**&lt;*MajorVersionNumber*&gt;&lt;*minorversionnumber,* **&gt;を削除**して、kmdf ランタイムを強制的に再インストールすることもできます。

## <a name="examining-umdf-installation"></a>UMDF インストールの検証


セットアップアクションログの次の出力は、UMDF ドライバーのインストールが成功したことを示しています。

```cpp
WudfUpdate: installing version (1,9,0,7100).
WudfUpdate: Checking for presence of previous UMDF installation.
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfrd.sys version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfpf.sys version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfhost.exe version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfsvc.dll version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfx.dll version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfplatform.dll version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfcoinstaller.dll version (1.9.0.7100)
WudfUpdate: UMDF installation is same as update. WudfUpdate: Loading configuration coinstaller from D:\Windows\system32\wudfcoinstaller.dll.
WudfCoInstaller: ReadWdfSection: Checking WdfSection [Echo_Install.NT.Wdf]
WudfCoInstaller: Configuring UMDF Service  WUDFEchoDriver.
WudfCoInstaller: Service WudfSvc is already running.
WudfCoInstaller: Final status: error(0) The operation completed successfully.
```

上記のシナリオでは、更新は必要ありません。これは、ランタイムのディスク上のバージョンが UMDF 1.9 であるためです。これは、共同インストーラーのバージョンと同じです。

次の出力について考えてみましょう。インストールの失敗について詳しく説明します。

```cpp
WudfUpdate: installing version (1,9,0,7100).
WudfUpdate: Checking for presence of previous UMDF installation.
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfrd.sys version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfpf.sys version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfhost.exe version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfsvc.dll version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfx.dll version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfplatform.dll version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfcoinstaller.dll version (1.5.0.6000)
WudfUpdate: UMDF installation is older than current.
WudfUpdate: Locating resource stream WUDF_UPDATE_VISTA-RTM.
WudfUpdate: unpacking update from resource to Microsoft User-Mode Driver Framework Install-v1.9-Vista.msu.
WudfUpdate: Temporary path is D:\Windows\Temp\WDF7625.tmp.
WudfUpdate: Invoking update "%SYSTEMROOT%\system32\wusa.exe" with command line "D:\Windows\Temp\WDF7625.tmp\Microsoft User-Mode Driver Framework Install-v1.9-Vista.msu /quiet /norestart".
WudfUpdate: Waiting for update to terminate.
WudfUpdate: Update process returned 22.
WudfUpdate: update returned error 0x16 - error(22) The device does not recognize the command.
WudfUpdate: For additional information please look at the log files %windir%\windowsupdate.log and %windir%\Logs\CBS\CBS.log
WudfUpdate: Cleaning up update.
WudfUpdate: Error updating UMDF - error(22) The device does not recognize the command. Aborting installation.
```

このシナリオでは、UMDF runtime のディスク上のバージョンが、共同インストーラーのバージョンより古いバージョンでした。 ただし、この場合、更新は失敗しました。 共同インストーラーは、エラーの原因に関する詳細情報が記載されている追加のログファイルを参照します。










---
title: KMDF および UMDF ドライバーのインストールのトラブルシューティング
description: KMDF および UMDF ドライバーのインストールのトラブルシューティング
ms.assetid: b0b71adc-cb6e-4b84-a5bf-bd1269bcf315
keywords:
- カーネル モード ドライバー フレームワーク WDK は、ドライバーをインストールします。
- フレームワーク ベースのドライバー WDK KMDF をインストールします。
- INF ファイル WDK KMDF、デバッグ
- ドライバー WDK KMDF、インストールのデバッグ
- ドライバー WDK KMDF のデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0912301a578b3fcc62af100dbd334aafa1c47546
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552712"
---
# <a name="troubleshooting-kmdf-and-umdf-driver-installation"></a>KMDF および UMDF ドライバーのインストールのトラブルシューティング


フレームワークの共同インストーラーは、デバッグ メッセージを作成します。 Windows のチェック ビルドを実行している場合、デバッガーでこれらのメッセージを確認できます。

さらに、共同インストーラーが、デバッグ メッセージを書き込みます、[セットアップ アクション ログ](https://msdn.microsoft.com/library/windows/hardware/ff550900)(*%windir%\\setupact.log*) ファイル。 セットアップの操作ログには、共同インストーラーと、ドライバーの INF ファイルで指定されたドライバーのバージョンが含まれています。 期待どおりにあることを確認する必要があります。

## <a name="examining-kmdf-installation"></a>KMDF インストールの確認


セットアップの操作ログに次の出力は、KMDF ドライバーのインストールの成功からです。

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

上記のシナリオでは、更新プログラムがないために必要なため、ディスク上のバージョンとメモリ内のフレームワーク バージョンは、KMDF 1.9 共同インストーラーの同じバージョンであります。

次の出力をインストールが失敗の詳細を示すを検討してください。

```cpp
WdfCoInstaller: ReadComponents:  WdfSection for Driver Service ECHO using KMDF lib version Major 0x1, minor 0x9  
WdfCoInstaller: DIF_INSTALLDEVICE: Coinstaller version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF in-memory version: 1.7.6000
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF on-disk version: 1.7.6000
WdfCoInstaller: Service Wdf01000 is running
WdfCoInstaller: DIF_INSTALLDEVICE: Reboot is required, because the in-memory KMDF version is older than the coinstaller&#39;s version.
WdfCoInstaller: DIF_INSTALLDEVICE: Update is required, because the on-disk KMDF version is older than the coinstaller
WdfCoInstaller: VerifyMSRoot: exit: error(0) The operation completed successfully.
WdfCoInstaller: Invoking "D:\Windows\system32\wusa.exe "D:\Windows\Temp\WdfTemp\Microsoft Kernel-Mode Driver Framework Install-v1.9-Vista.msu" /quiet /norestart".
WdfCoInstaller: The update process returned error code :error(265) <no error text>. 
WdfCoInstaller: For additional information please look at the log files %windir%\windowsupdate.log and %windir%\Logs\CBS\CBS.log
```

このシナリオで更新と再起動の両方が必要なメモリ内のバージョンおよび KMDF ランタイムのディスク上のバージョンが共同インストーラーのバージョンよりも古いため。 ただし、更新に失敗しました。 共同インストーラーは、障害の詳細が得られる追加のログ ファイルを指します。

ランタイム ライブラリを KMDF ドライバーの動的バインドに関連するエラーのシステム イベント ログを確認することもできます。 このようなエラーが発生する**Wdf**&lt;*MajorVersionNumber*&gt;&lt;*MinorVersionNumber* &gt;内のエントリシステム イベント ログ。 この場合、コンピューターを再起動します。 削除することによって、KMDF ランタイムの再インストールを強制することもできます**Wdf**&lt;*MajorVersionNumber*&gt;&lt;*MinorVersionNumber*&gt; **.sys**から、 *%windir%\\system32\\ドライバー*フォルダー。

## <a name="examining-umdf-installation"></a>UMDF インストールの確認


セットアップの操作ログに次の出力には、成功した UMDF ドライバーのインストールについて説明します。

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

上記のシナリオでは、更新プログラムは必要ありませんディスク上のバージョンのランタイムは、UMDF 1.9 共同インストーラーのバージョンと同じであるためです。

次の出力をインストールが失敗の詳細を示すを検討してください。

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

このシナリオでは、UMDF ランタイムのディスク上のバージョンを共同インストーラーのバージョンよりも古かった。 ただし、この場合、更新に失敗しました。 共同インストーラーは、失敗の原因に関する詳細情報が得られる追加のログ ファイルを指します。










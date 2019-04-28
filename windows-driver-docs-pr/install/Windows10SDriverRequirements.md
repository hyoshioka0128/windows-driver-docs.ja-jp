---
title: Windows 10 S モードでのドライバー要件
ms.date: 05/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9a2f9fce6b3146f0ad3c49f9a71fe8b02b541d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375752"
---
# <a name="windows-10-in-s-mode-driver-requirements"></a>Windows 10 S モードでのドライバー要件

このセクションは、Windows 10 s. でドライバーのインストール要件、およびブロックされているコンポーネントを説明します。  

## <a name="driver-requirements"></a>ドライバーの要件

Windows 10 S モードでインストールするには、ドライバー パッケージは次の要件を満たす必要があります。

-   ドライバー パッケージはデジタル署名で署名する必要があります、 **Windows、WHQL、ELAM、またはストア**から証明書、 [Windows ハードウェア デベロッパー センター ダッシュ ボード](https://aka.ms/DevCenterPortal)します。
-   付属するソフトウェアを署名する必要があります、[の証明書を Microsoft Store](https://docs.microsoft.com/windows/uwp/publish/the-app-certification-process)します。
-   含まれません、 \*.exe、 \*.zip、 \*.msi または\*符号なしのバイナリを抽出するドライバー パッケージ内の .cab です。
-   ドライバーは、INF ディレクティブのみを使用してをインストールします。
-   ドライバーは呼び出しません[受信トレイのコンポーネントをブロック](#blocked-inbox-components)します。
-   ドライバーは、任意のユーザー インターフェイス コンポーネント、アプリ、または設定には含まれません。  代わりに、ユニバーサル アプリケーションから Microsoft Store を使用します。
    *  [アプリのハードウェア サポート](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-access-for-universal-windows-platform-apps)
    *  [UWP デバイス アプリ](https://docs.microsoft.com/windows-hardware/drivers/devapps/meet-uwp-device-apps)
    *  [Centennial アプリ](https://developer.microsoft.com/windows/bridges/desktop)
-   ドライバーとファームウェアのサービスは、Windows Update とアップデーター アプリケーションではなくを使用します。

最後に、可能な場合は、ユニバーサル Windows ドライバーを使用してをお勧めします。  For more info, see:

-   [ユニバーサル ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)
-   [ユニバーサル ドライバーの検証](https://docs.microsoft.com/windows-hardware/drivers/develop/validating-universal-drivers)

## <a name="blocked-inbox-components"></a>ブロックされた受信トレイのコンポーネント

次のコンポーネントは、Windows 10 s: での実行からブロックされます。

-   bash.exe
-   cdb.exe
-   cmd.exe
-   cscript.exe
-   csi.exe
-   dnx.exe
-   fsi.exe
-   hh.exe
-   infdefaultinstall.exe (Windows 10 バージョン 1709 で新たに追加)
-   kd.exe
-   lxssmanager.exe
-   msbuild.exe
-   mshta.exe
-   ntsd.exe
-   powershell.exe
-   powershell_ise.exe
-   rcsi.exe
-   reg.exe
-   regedit.exe  
-   regedt32.exe
-   regini.exe
-   syskey.exe
-   wbemtest.exe
-   windbg.exe
-   wmic.exe
-   wscript.exe
-   wsl.exe

> [!次へ] S モードで Windows 10 を実行するデバイスで Windows アプリが正常に動作させるには、確認してください、[テスト ガイダンス](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-test-windows-s)アプリ。 

---
title: Windows 10 S モードでのドライバー要件
ms.date: 05/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2b25df5609f6d7dade0de6f2bf4f8b0859d55b
ms.sourcegitcommit: fc42f2042aad57cf19fac798ff838bb064b1a4e6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66223227"
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

## <a name="installation"></a>インストール

* ダッシュ ボード内のドライバーを提出するときに、S のコンプライアンス チェック ボックスをチェックする場合、ドライバーは、S モードと同じハードウェア ID を持つ、Windows 10 のデスクトップ バージョンでは、どちらも Windows 10 に配信されます。 これらのダッシュ ボードのオプションの詳細については、次を参照してください。[ドライバーを Windows Update に公開](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)します。
* 別のドライバー パッケージが Windows 10 用のモードと同じ HWID を対象とする Windows 10 のデスクトップ バージョンで必要な場合は、大きい設定**DriverVer**内のエントリ、 [INF バージョン セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)パッケージWindows 10 のデスクトップ バージョンを対象とするとします。  たとえば、設定することがあります、 **DriverVer**の`05/24/2019,10.0.1.0`S モードで Windows 10 をターゲットとするパッケージのと`05/24/2019,10.1.1.0`のデスクトップ バージョンの Windows 10 をターゲットとするパッケージ。

## <a name="troubleshooting-installation"></a>インストールのトラブルシューティング

両方の基本 INF と、拡張子 INF は INF が Windows 10 のデスクトップ バージョンにインストールする拡張機能のみのモードで Windows 10 をターゲットに場合、インストールされているドライバーが大きいランクのか、基本のドライバーが、適切なターゲットでは発行されていません。ing します。  (CHID 異なる場合があります)。    確認し、基本のドライバーとドライバーの拡張機能の出荷ラベルを比較します。

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

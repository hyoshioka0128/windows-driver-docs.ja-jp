---
title: UMDF Verifier を使用します。
description: UMDF Verifier を使用します。
ms.assetid: 95D85894-86AF-4312-B5BD-F1C9E8F8B2E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1825120f534ba82299792ae6971ee0775bdf2dd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559611"
---
# <a name="using-umdf-verifier"></a>UMDF Verifier を使用します。


フレームワークは、実行中のユーザー モード ドライバー フレームワーク (UMDF) ドライバーをテストに使用できる組み込みの検証機能を提供します。 ドライバーの状態と、ドライバーが framework オブジェクトのメソッドに渡される引数を幅広く UMDF 検証機能とも呼ばれます。 この機能は、検証します。 UMDF Verifier を使用するには、単独または汎用と共に[Application Verifier (AppVerif.exe)](../debugger/debugger-download-tools.md)ツール。

UMDF Verifier は、ロックの取得と階層を確認します、正確な I/O キャンセルとキューの使用率を検証し、ドライバー、フレームワークが文書化されているコントラクトを従うことにより。

UMDF 検証とは UMDF ドライバー コードにエラーが発生*バグ チェック*ホスト プロセス。 ただし、UMDF バグ チェックでは、エラーに関する情報を表示する青色のテキスト画面は発生しません。 代わりに、チェックのバグを UMDF:

-   メモリ ダンプ ファイルを作成し、コンピューターのログ ファイルのディレクトリにファイルを保存します (%windir% など\\System32\\LogFiles\\WUDF\\*Xxx*.dmp)。

    **注**  ログ ディレクトリは、UMDF 2.15 以降、 *%programdata%*\\Microsoft\\WDF します。

     

-   作成、[エラー レポート](how-umdf-reports-errors.md)(オプトイン) microsoft。

-   コンピューターに接続されている場合は、デバッガーを中断します。

-   ホスト プロセスを終了し、デバイスを無効にします。

UMDF 2.0 以降、UMDF Verifier は発行で場合によっては、ブレークポイントし、他のユーザーで UMDF バグ チェックが実行します。 この動作は、KMDF Verifier に似ています。

すべての開発を行うと、有効にした後、ドライバーのテストを強くお勧め[Application Verifier (AppVerif.exe)](../debugger/debugger-download-tools.md) WUDFHost.exe にします。 次のコマンドを使用して、デバッガーをアタッチして再起動します。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

実行する場合、UMDF のバージョン 2.0 以降[Application Verifier](../debugger/debugger-download-tools.md)ドライバー ホスト プロセス (Wudfhost) UMDF 検証ツールが自動的に有効になって UMDF 2.0 ドライバーはすべて、そのホストとホストの将来のドライバーのすべての UMDF 2.0 ドライバー処理します。

UMDF 1.11 以降では、フレームワークの検証は常にオンおよびオフにすることはできません。

## <a name="enabling-and-disabling-umdf-verifier"></a>有効にして、UMDF 検証を無効化


設定して UMDF 検証できるように手動で**VerifierOn** 0 以外の場合、ドライバーの値に**パラメーター\\Wdf**のサブキー、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス\\&lt;ドライバー名&gt;** レジストリ キー。

**注**  の存在を**VerifierOn**ゼロに設定しても、すべての値には、Application Verifier と共にリンケージがより優先されます。 その結果、強制しているされませんが、0 に設定するのではなく、値を削除するをお勧めします。

 

UMDF 検証機能が有効になっているかどうかを確認するには、ドライバーの呼び出しの後の場所にブレークポイントを設定します[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)を使用すると、 [ **! wdfdriverinfo**。](https://msdn.microsoft.com/library/windows/hardware/ff565724)デバッガー拡張機能コマンド。

**!wdfkd.wdfdriverinfo** *&lt;your drivername&gt;* **** **0x1**

デバッガーの拡張機能コマンドの詳細については、次を参照してください。 [Framework ベースのドライバーの拡張機能をデバッガー](debugger-extensions-for-kmdf-drivers.md)します。

## <a name="controlling-the-verifiers-behavior"></a>検証の動作を制御します。


レジストリの値を変更することによって、UMDF 検証ツールの動作を制御できます。 また、使用することができます、 [WDF Verifier コントロール アプリケーション](https://msdn.microsoft.com/library/windows/hardware/ff556129)をこれらの値を設定します。

次のレジストリ値は、UMDF 1 で使用できます。*x* UMDF 2.0 以降のドライバーとドライバー。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**VerifyDownLevel** (**REG\_DWORD**)  
場合**VerifyDownLevel** 0 以外の値に設定されているフレームワークの検証方法には、ドライバーが現在のバージョンより古いフレームワークのバージョンでビルドされている場合、ドライバーがビルドされた後に追加されたテストが含まれています。 この値が存在しないか、0 に設定されているの場合、フレームワークの検証には、ドライバーのビルド時に存在していたテストのみが含まれます。

たとえばには、ドライバーは、framework の version 1.7 で作成した場合、およびフレームワークのバージョン 1.9 がコンピューターにインストールされている場合は、設定**VerifyDownLevel**に 0 以外の場合と、検証機能に追加されたテストを含めるドライバーの実行時に検証ツールのバージョン 1.9 にします。

この値にある、**パラメーター\\Wdf**のサブキー、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\WindowsNT\\CurrentVersion\\WUDF\\サービス\\* DriverName*** レジストリ キー。

<a href="" id="trackobjects-----------------------------reg-dword-"></a>**TrackObjects** (**REG\_DWORD**)  
場合**TrackObjects**設定が 0 以外の値をフレームワークが入力、デバッガー、ドライバーが読み込まれるときに、フレームワークに基づくオブジェクトがある場合[リーク](determining-if-a-driver-leaks-framework-objects.md)(されていない削除) します。

通常のテスト中に有効にしてください**TrackObjects**なく**TrackRefCounts**します。 有効にするコントロール アプリケーションを使用、検証機能では、ドライバーで framework のオブジェクトがリークしていることを報告する場合、 **TrackRefCounts** verifier オプション。

この値にある、 *DefaultHostProcessGuid*のサブキー、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス**のレジストリ キー、 *DefaultHostProcessGuid*で検索できる値は、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**サブキー。

<a href="" id="trackrefcounts-----------------------------reg-dword-"></a>**TrackRefCounts** (**REG\_DWORD**)  
場合**TrackRefCounts**設定が 0 以外の値に、フレームワークは各フレームワーク ベースのオブジェクトへの参照の数のカウントを保持します。 使用することができます、 [! wudfrefhist](using-umdf-debugger-extensions.md)デバッガー拡張機能オブジェクトの参照カウントの変更を表示します。

設定**TrackRefCounts** 0 以外の値をドライバーのパフォーマンスが低下にため、オブジェクトの削除バグをデバッグしている場合を除き、ゼロから値を残しておく必要があります。

この値にある、 *DefaultHostProcessGuid*のサブキー、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス**のレジストリ キー、 *DefaultHostProcessGuid*で検索できる値は、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**サブキー。

レジストリだけでなく上記の値、UMDF 2.0 およびそれ以降のドライバーも使用できますのレジストリ値の多く[KMDF Verifier を使用して](using-kmdf-verifier.md)します。

 

 






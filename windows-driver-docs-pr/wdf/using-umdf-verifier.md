---
title: UMDF 検証ツールの使用
description: UMDF 検証ツールの使用
ms.assetid: 95D85894-86AF-4312-B5BD-F1C9E8F8B2E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06870c6c89dd3624c0e3e912eb7a06f53c394534
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842588"
---
# <a name="using-umdf-verifier"></a>UMDF 検証ツールの使用


フレームワークには、実行中のユーザーモードドライバーフレームワーク (UMDF) ドライバーのテストに使用できる、組み込みの検証機能が用意されています。 この機能は、UMDF Verifier とも呼ばれ、ドライバーの状態と、ドライバーがフレームワークオブジェクトメソッドに渡す引数を広範囲にわたって検証します。 UMDF 検証ツールは、単独で使用することも、汎用[アプリケーション検証ツール (appverif.chm)](../debugger/debugger-download-tools.md)ツールと共に使用することもできます。

UMDF 検証ツールは、取得と階層をロックし、正しい i/o のキャンセルとキューの使用状況を確認し、ドライバーとフレームワークがドキュメントに記載されたコントラクトに従っていることを確認します。

UMDF 検証ツールでは、UMDF ドライバーコードでエラーが発生し、ホストプロセスが*バグチェック*されます。 ただし、UMDF バグチェックによって、エラーに関する情報が青色のテキスト画面に表示されることはありません。 代わりに、UMDF バグチェックを行います。

-   メモリダンプファイルを作成し、コンピューターのログファイルディレクトリ (たとえば、% windir%\\System32\\ログファイル\\WUDF\\*Xxx*.dmp) に保存します。

    **  UMDF** 2.15 以降では、ログディレクトリは *% programdata%* \\Microsoft\\WDF になります。

     

-   Microsoft (オプトイン) の[エラーレポート](how-umdf-reports-errors.md)を作成します。

-   デバッガーがコンピューターに接続されている場合、デバッガーを中断します。

-   ホストプロセスを終了し、デバイスを無効にします。

UMDF 2.0 以降では、umdf 検証機能によってブレークポイントが問題になることがあり、他の場合は UMDF バグチェックが発生します。 この動作は、KMDF 検証機能と似ています。

WUDFHost で[アプリケーション検証ツール (appverif.chm)](../debugger/debugger-download-tools.md)を有効にした後、ドライバーのすべての開発とテストを実行することを強くお勧めします。 次のコマンドを使用して、デバッガーをアタッチし、再起動します。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

UMDF のバージョン2.0 以降では、ドライバーホストプロセス (Wudfhost) で[アプリケーション検証ツール](../debugger/debugger-download-tools.md)を実行すると、そのホストのすべての umdf 2.0 ドライバーと、今後のドライバーホストプロセスのすべての umdf 2.0 ドライバーに対して、umdf Verifier が自動的に有効になります。

UMDF 1.11 以前では、フレームワークの検証ツールは常にオンになっており、オフにすることはできません。

## <a name="enabling-and-disabling-umdf-verifier"></a>UMDF 検証機能の有効化と無効化


**VerifierOn**を手動で有効にするには、ドライバーの [ **\\パラメーター** ] に0以外の値を設定します。 **HKEY\_ローカル\_コンピューター\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;ドライバー名&gt;** レジストリキー。

**VerifierOn**値の存在がゼロに設定されていても、アプリケーション検証ツールとのリンケージがオーバーライドさ  **ことに注意**してください。 そのため、値を0に設定するのではなく、強制的に使用しない場合は、値を削除することをお勧めします。

 

UMDF 検証機能が有効になっているかどうかを判断するには、ドライバーが[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出した後、場所にブレークポイントを設定し、 [ **! wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)デバッガー拡張コマンドを使用します。

*&lt;ドライバー&gt;*  **** **0x1**の場合は、 **! wdfkd. wdfdriverinfo を使用します。**

デバッガー拡張機能のコマンドの詳細については、「[フレームワークベースのドライバーのデバッガー拡張](debugger-extensions-for-kmdf-drivers.md)」を参照してください。

## <a name="controlling-the-verifiers-behavior"></a>検証機能の動作の制御


レジストリの値を変更することで、UMDF Verifier の動作を制御できます。 または、 [WDF Verifier コントロールアプリケーション](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)を使用して、これらの値を設定することもできます。

次のレジストリ値は、UMDF 1 で使用できます。*x*ドライバー、および UMDF 2.0 以降のドライバー。

<a href="" id="verifydownlevel--------------reg-dword-"></a>**Verifydownlevel レベル**(**REG\_DWORD**)  
**Verifydownlevel レベル**が0以外の値に設定されていて、現在のバージョンより古いバージョンのフレームワークを使用してドライバーがビルドされている場合、フレームワークの検証ツールには、ドライバーのビルド後に追加されたテストが含まれます。 この値が存在しない場合、または0に設定されている場合、フレームワークの検証ツールには、ドライバーがビルドされたときに存在していたテストのみが含まれます。

たとえば、ドライバーがバージョン1.7 のフレームワークでビルドされ、コンピューターに framework のバージョン1.9 がインストールされている場合、 **Verifydownlevel レベル**を0以外に設定すると、検証ツールのバージョン1.9 に追加されたテストが検証ツールに含まれるようになります。ドライバーの実行時。

この値は、 **HKEY\_ローカル\_コンピューター\\ソフトウェア\\MICROSOFT\\Windows NT\\CurrentVersion\\Wudf\\Services\\Wdf のパラメーター\\サブキーにあります。ドライバー**1 * レジストリキー。

<a href="" id="trackobjects-----------------------------reg-dword-"></a>**Trackobjects** (**REG\_DWORD**)  
**Trackobjects**が0以外の値に設定されている場合、フレームワークは、(削除されていない) フレームワークベースのオブジェクトが[リーク](determining-if-a-driver-leaks-framework-objects.md)した場合に、ドライバーがアンロードされたときにデバッガーに入ります。

通常のテストでは、 **TrackRefCounts**ではなく**trackobjects**を有効にする必要があります。 検証ツールによって、ドライバーがフレームワークオブジェクトをリークしていることが報告された場合は、コントロールアプリケーションを使用して、 **TrackRefCounts** verifier オプションを有効にします。

この値は、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\Services**レジストリキーの*Defaulthostprocessguid*サブキーにあります。では、 *Defaulthostprocessguid*は、 **HKEY\_ローカル\_コンピューター\\ソフトウェア\\MICROSOFT\\Windows NT\\CurrentVersion\\wudf**サブキーで確認できる値です。

<a href="" id="trackrefcounts-----------------------------reg-dword-"></a>**TrackRefCounts** (**REG\_DWORD**)  
**TrackRefCounts**が0以外の値に設定されている場合、フレームワークは各フレームワークベースのオブジェクトへの参照の数を保持します。 [! Wudfrefhist](using-umdf-debugger-extensions.md)デバッガー拡張機能を使用して、オブジェクトの参照カウントの変更を表示できます。

**TrackRefCounts**を0以外の値に設定すると、ドライバーのパフォーマンスが低下するため、オブジェクトの削除に関するバグをデバッグする場合を除き、値を0のままにしておく必要があります。

この値は、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\WINDOWS NT\\CurrentVersion\\WUDF\\Services**レジストリキーの*Defaulthostprocessguid*サブキーにあります。では、 *Defaulthostprocessguid*は、 **HKEY\_ローカル\_コンピューター\\ソフトウェア\\MICROSOFT\\Windows NT\\CurrentVersion\\wudf**サブキーで確認できる値です。

上記のレジストリ値に加えて、UMDF 2.0 以降のドライバーでは、 [「KMDF Verifier の使用](using-kmdf-verifier.md)」に示されている多くのレジストリ値を使用することもできます。

 

 






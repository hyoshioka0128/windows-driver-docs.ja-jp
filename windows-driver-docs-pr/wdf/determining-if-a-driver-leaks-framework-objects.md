---
title: ドライバーが Framework オブジェクトをリークするかどうかを決定します。
description: このトピックでは、解放されていない参照によるドライバーのメモリ リークを検索する方法について説明します。 ユーザー モード ドライバー フレームワーク (UMDF) ドライバーのバージョン 1 と 2 に適用されます。
ms.assetid: 617cc678-e0db-4d2f-9d19-34b6cedad234
keywords:
- デバッグ シナリオ WDK UMDF、ドライバーのフレームワーク オブジェクト リークが発生するかどうかを決定します。
- UMDF WDK、デバッグする場合、ドライバーのフレームワーク オブジェクト リークが発生するかどうかを決定します。
- UMDF WDK、ドライバーのフレームワーク オブジェクト リークが発生するかどうかを決定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a302cc2cee7500b39622a2fb58a791eee969b0cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532121"
---
# <a name="determining-if-a-driver-leaks-framework-objects"></a>ドライバーが Framework オブジェクトをリークするかどうかを決定します。


このトピックでは、解放されていない参照によるドライバーのメモリ リークを検索する方法について説明します。 ユーザー モード ドライバー フレームワーク (UMDF) ドライバーのバージョン 1 と 2 に適用されます。

## <a name="umdf-1"></a>UMDF 1


UMDF バージョン 1 で呼び出し履歴はメモリ リークが発生への各呼び出しの場合**AddRef**が一致する**リリース**呼び出します。

UMDF ドライバー バージョン 1 フレームワーク オブジェクトのリークをテストするには、次の手順を使用します。

1.  使用して、 [WDF Verifier コントロール アプリケーション](https://msdn.microsoft.com/library/windows/hardware/ff556129)する検証のオプションを設定します。 定期的なテストの実行中に設定して開始**TrackObjects**なく**TrackRefCounts**します。

    ドライバーが読み込まれると、フレームワークのコードの検証機能が入力デバッガー framework オブジェクトが削除されていないと、使用するよう求められます、 [ **! wudfdumpobjects** ](using-umdf-debugger-extensions.md)デバッガー拡張機能。 このデバッガー拡張機能では、削除されていないオブジェクトの一覧が表示されます。

2.  コード検証機能では、ドライバーで framework のオブジェクトがリークしていることを示している場合、アプリケーションを使用してコントロールを設定、 [ **TrackRefCounts** ](using-umdf-verifier.md)オプション。

    このオプションが設定されている場合、検証機能の追跡ドライバーの実行中にフレームワーク オブジェクトへの参照。 使用することができます、 [ **! wudfrefhist** ](using-umdf-debugger-extensions.md)デバッガー拡張がそれぞれ表示する呼び出しスタック (関数呼び出しのセット) をインクリメントまたはデクリメント オブジェクトの参照カウントします。 調べることで、 **AddRef**と**リリース**呼び出しでは、これらの呼び出し履歴、オブジェクトの参照カウントをデクリメントしないと、リークするスタックを検索できる必要があります。

追加の検証のオプションについては、次を参照してください。 [UMDF Verifier を使用して](using-umdf-verifier.md)します。

Framework のオブジェクトを削除する場合については、次を参照してください。[オブジェクトの有効期間を管理する](managing-the-lifetime-of-objects.md)します。

## <a name="umdf-2"></a>UMDF 2


UMDF バージョン 2 で解放されていない参照はまれですが呼び出しの不一致によるを使用する場合に発生することが[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)と[ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739).

場合はバージョン 2 UMDF ドライバー framework オブジェクトのリークをテストするには、次の手順を使用します。

1.  記載されている手順に従います[ベスト プラクティス](enabling-a-debugger.md#bp)UMDF デバッグ用にコンピューターを構成します。
2.  タグの追跡を使用するには、UMDF Verifier とレジストリの追跡ハンドルの両方を有効にします。 これらの設定は、ドライバーに格納されている**パラメーター\\Wdf**のサブキー、 **HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス\\&lt;ドライバー名&gt;** キー。

    UMDF 検証機能を有効にする、0 以外の値を設定**VerifierOn します。**

    ハンドルの追跡を有効にするには、値を設定**TrackHandles** 1 つまたは複数のオブジェクトの種類の名前にアスタリスクを指定または (\*) すべてのオブジェクトの種類を追跡するためにします。

    使用して、UMDF 検証設定を変更することも、 [WdfVerifier.exe](https://msdn.microsoft.com/library/windows/hardware/ff556129)アプリケーション。

3.  再起動し、デバッガーの接続を確立し、次のデバッガー コマンドを使用します。

    -   [**! wdfkd.wdfdriverinfo 0x10** ](https://msdn.microsoft.com/library/windows/hardware/ff565724)ハンドルの階層を表示するには
    -   [**! wdfkd.wdftagtracker** ](https://msdn.microsoft.com/library/windows/hardware/ff566126)タグ情報を表示するには

UMDF 検証機能がオンの場合は、KMDF と同じように、ドライバーのアンロードでメモリ リークが検出されました。

参照の使用に関する追加情報は、KMDF および UMDF ドライバーのバージョン 2 でカウントを参照してください[Framework オブジェクトのライフ サイクル](framework-object-life-cycle.md)します。

 

 






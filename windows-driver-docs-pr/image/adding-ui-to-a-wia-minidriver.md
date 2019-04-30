---
title: WIA ミニドライバーへの UI の追加
description: WIA ミニドライバーへの UI の追加
ms.assetid: 70440de2-0554-4f5b-9ce4-fe060d3077a4
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3a010fe08a18d18d9e98c3d7f3c0c7b1821b5b70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367094"
---
# <a name="adding-ui-to-a-wia-minidriver"></a>WIA ミニドライバーへの UI の追加

UI の拡張を追加したり、WIA ミニドライバーを別個の DLL をインストールすることで、WIA ミニドライバーの UI コンポーネントを交換することができます。 TWAIN ドライバーとは異なり、WIA ドライバーの UI コンポーネントは実際の WIA ミニドライバー別です。 UI コンポーネントは、WIA ミニドライバーは、WIA サービスのプロセスで実行されているアプリケーションのプロセスで実行します。 そのため、UI と WIA ドライバーが直接表示されないことがドライバーの WIA UI 拡張機能モジュールでは、UI を表示する場合があります。

WIA を使用すると、システムによって提供されるダイアログ ボックスにプロパティ ページを追加のカスタム アイコンのイメージを指定するか、システムによって提供されるダイアログ ボックスを完全に置き換えることができます。 プロパティ ページの拡張メカニズムのシェルの定義に基づいて、 **IShellPropSheetExt** (Microsoft Windows SDK のドキュメントで説明) COM インターフェイスです。 このメカニズムは、プロパティ シート ハンドラーに登録 (**HKCR\\Clsid\\**&lt;*デバイス UI の Clsid* &gt;  **\\shellex\\PropertySheetHandlers**)。

[プロパティ ページ] を除く、すべてのデバイス] ダイアログ ボックス拡張を必要とする、 [IWiaUIExtension インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545078)を実装します。

実装する場合、 **IWiaUIExtension**インターフェイスを返す必要があります、システム UI を交換したくない E\_の NOTIMPL、 [ **IWiaUIExtension::DeviceDialog** ](https://msdn.microsoft.com/library/windows/hardware/ff545069)メソッド。 その他の戻り値は、デバイスのデバイス ダイアログ ボックスを表示しません。

デバイスのダイアログ ボックスをモーダル ダイアログに渡して、インプロセス COM サーバーとして実装する必要が*pDeviceDialogData* -&gt;*hwndParent* に親の**DialogBoxParam**関数 (Windows SDK のドキュメントで説明)。 デバイスのダイアログ ボックスを返す必要があります S\_成功した場合、S の OK\_ユーザーがダイアログ ボックスで、またはその他のエラーの COM エラー HRESULT を取り消した場合は FALSE。

[ **DEVICEDIALOGDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff540560)構造体には、すべてのカスタム デバイス] ダイアログを実装するために必要なデータが含まれています。

デバイスのカスタム アイコンを提供するには、実装、 [ **IWiaUIExtension::GetDeviceIcon** ](https://msdn.microsoft.com/library/windows/hardware/ff545075)メソッド。 アイコンが使用して呼び出し元によって破棄される**DestroyIcon** (Windows SDK のドキュメントで説明)。

**注**   WIA が非常にスクリプトのサポートが制限されています。 そのため、UI を置換することはできますは、単なるスクリプト内で抑制することはできません。

このセクションの残りの部分は次のとおりです。

["Hello World"WIA ミニドライバー UI 拡張機能の作成](creating-a--hello-world--wia-minidriver-ui-extension.md)、独自のカスタム UI を実装する方法の完全な例です。

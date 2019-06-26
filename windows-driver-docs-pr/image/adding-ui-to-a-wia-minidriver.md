---
title: WIA ミニドライバーへの UI の追加
description: WIA ミニドライバーへの UI の追加
ms.assetid: 70440de2-0554-4f5b-9ce4-fe060d3077a4
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: caba309270a6345a3cfb824cc0a5ce43c00e37f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383393"
---
# <a name="adding-ui-to-a-wia-minidriver"></a>WIA ミニドライバーへの UI の追加

UI の拡張を追加したり、WIA ミニドライバーを別個の DLL をインストールすることで、WIA ミニドライバーの UI コンポーネントを交換することができます。 TWAIN ドライバーとは異なり、WIA ドライバーの UI コンポーネントは実際の WIA ミニドライバー別です。 UI コンポーネントは、WIA ミニドライバーは、WIA サービスのプロセスで実行されているアプリケーションのプロセスで実行します。 そのため、UI と WIA ドライバーが直接表示されないことがドライバーの WIA UI 拡張機能モジュールでは、UI を表示する場合があります。

WIA を使用すると、システムによって提供されるダイアログ ボックスにプロパティ ページを追加のカスタム アイコンのイメージを指定するか、システムによって提供されるダイアログ ボックスを完全に置き換えることができます。 プロパティ ページの拡張メカニズムのシェルの定義に基づいて、 **IShellPropSheetExt** (Microsoft Windows SDK のドキュメントで説明) COM インターフェイスです。 このメカニズムは、プロパティ シート ハンドラーに登録 (**HKCR\\Clsid\\** &lt;*デバイス UI の Clsid* &gt;  **\\shellex\\PropertySheetHandlers**)。

[プロパティ ページ] を除く、すべてのデバイス ダイアログ ボックス拡張を必要とする、 [IWiaUIExtension インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545078(v=vs.85))を実装します。

実装する場合、 **IWiaUIExtension**インターフェイスを返す必要があります、システム UI を交換したくない E\_の NOTIMPL、 [ **IWiaUIExtension::DeviceDialog** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))メソッド。 その他の戻り値は、デバイスのデバイス ダイアログ ボックスを表示しません。

デバイスのダイアログ ボックスをモーダル ダイアログに渡して、インプロセス COM サーバーとして実装する必要が*pDeviceDialogData* -&gt;*hwndParent* に親の**DialogBoxParam**関数 (Windows SDK のドキュメントで説明)。 デバイスのダイアログ ボックスを返す必要があります S\_成功した場合、S の OK\_ユーザーがダイアログ ボックスで、またはその他のエラーの COM エラー HRESULT を取り消した場合は FALSE。

[ **DEVICEDIALOGDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiadevd/ns-wiadevd-tagdevicedialogdata)構造体には、すべてのカスタム デバイス ダイアログを実装するために必要なデータが含まれています。

デバイスのカスタム アイコンを提供するには、実装、 [ **IWiaUIExtension::GetDeviceIcon** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))メソッド。 アイコンが使用して呼び出し元によって破棄される**DestroyIcon** (Windows SDK のドキュメントで説明)。

**注**   WIA が非常にスクリプトのサポートが制限されています。 そのため、UI を置換することはできますは、単なるスクリプト内で抑制することはできません。

このセクションの残りの部分は次のとおりです。

["Hello World"WIA ミニドライバー UI 拡張機能の作成](creating-a--hello-world--wia-minidriver-ui-extension.md)、独自のカスタム UI を実装する方法の完全な例です。

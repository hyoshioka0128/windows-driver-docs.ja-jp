---
title: WIA ミニドライバーへの UI の追加
description: WIA ミニドライバーへの UI の追加
ms.assetid: 70440de2-0554-4f5b-9ce4-fe060d3077a4
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8a5e269ce93d340dd76e518a4fd83a500e311b76
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840905"
---
# <a name="adding-ui-to-a-wia-minidriver"></a>WIA ミニドライバーへの UI の追加

WIA ミニドライバーを使用して別の DLL をインストールすることにより、WIA ミニドライバーの拡張 UI または UI コンポーネントを置き換えることができます。 TWAIN ドライバーとは異なり、WIA ドライバーの UI コンポーネントは実際の WIA ミニドライバーとは分離されています。 UI コンポーネントはアプリケーションのプロセスで実行され、wia ミニドライバーは WIA サービスのプロセスで実行されます。 そのため、WIA ドライバーでは UI が直接表示されない場合があります。UI が表示されるのは、ドライバーの WIA UI 拡張モジュールだけです。

WIA では、システムに用意されているダイアログボックスにプロパティページを追加したり、カスタムアイコンイメージを提供したり、システムによって提供されるダイアログボックスを完全に置き換えたりすることができます。 プロパティページの拡張機能は、 **IShellPropSheetExt** COM インターフェイスのシェル定義に基づいています (Microsoft Windows SDK のドキュメントを参照)。 このメカニズムは、プロパティシートハンドラーに登録されています (**HKCR\\clsid\\** &lt;*デバイス UI の clsid*&gt; **\\shellex\\PropertySheetHandlers**)。

プロパティページを除く、デバイスダイアログボックスのすべての拡張機能では、 [Iwi/Extension インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545078(v=vs.85))を実装する必要があります。

**IwiNOTIMPL iextension**インターフェイスを実装し、システム UI を置き換えたくない場合は、 [**iwi iextension::D evicedialog**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))メソッドに対して E\_を返す必要があります。 その他の戻り値は、デバイスの [デバイス] ダイアログボックスを非表示にします。

[デバイス] ダイアログボックスは、インプロセス COM サーバーにモーダルダイアログとして実装し、 *Pdevicedialogdata* -&gt;*hwndParent* **を、親のプロパティ関数に**渡す必要があります (「Windows SDK」を参照してください)。ドキュメント)。 [デバイス] ダイアログボックスで、成功した場合は [OK]、S\_ユーザーがダイアログボックスをキャンセルした場合は [FALSE]、他のエラーの場合は [COM エラー HRESULT] が\_返されます。

[**Devicedialogdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiadevd/ns-wiadevd-tagdevicedialogdata)構造体には、カスタムデバイスダイアログの実装に必要なすべてのデータが含まれています。

デバイスのカスタムアイコンを提供するには、 [**Iwi/Iextension:: GetDeviceIcon**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))メソッドを実装します。 アイコンは、(Windows SDK のドキュメントで説明されている) **Destroyicon**を使用して、呼び出し元によって破棄されます。

**   WIA**では、スクリプトのサポートが非常に制限されています。 そのため、UI を置き換えることはできますが、スクリプト内で単に抑制することはできません。

このセクションの残りの部分は次のとおりです。

[「Hello World」 WIA ミニドライバー Ui 拡張機能の作成](creating-a--hello-world--wia-minidriver-ui-extension.md)。独自のカスタム ui を実装する方法の完全な例です。

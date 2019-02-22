---
title: プロパティ シートの拡張機能
description: プロパティ シートの拡張機能
ms.assetid: 36254759-882c-45af-92df-e0769b65ec55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e01c1fdbfacf01b6a39036b6131655f71e910e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557411"
---
# <a name="property-sheet-extensions"></a>プロパティ シートの拡張機能





プロパティのコンテキスト メニュー項目は、スキャナーにアクセスを提供します。 または、スキャナーでカメラのプロパティ シート (ルート項目) のデバイスのカメラ コントロール パネル フォルダーや、[マイ コンピューター] フォルダー。

プロパティ シートの拡張機能のカメラおよびスキャナーもインターフェイスを提供ユーザー固有のイメージの取得のセッション、つまり、ルート以外**IWiaItem** (Microsoft Windows SDK のドキュメントを参照してください)、オブジェクトがアクティブにします。ユーザーがダイアログのスキャン、既定値を使用します。 これらの拡張機能は、高度なプロパティを通じてアクセスするか、高度な設定がイメージの取得ダイアログ ボックスでリンクします。 プロパティのコンテキスト メニューからアクションを選択すると、WIA を構築しますプロパティ シートのベンダーから提供された実装を使用して、 **IShellExtInit**と**IShellPropSheetExt** (インターフェイス。Windows SDK のドキュメントを参照)。

両方プロパティ シートとコンテキスト メニュー UI の拡張機能、 **IDataObject** (Windows SDK のドキュメントで説明) インターフェイス、WIAItemNames 形式または WIAItemPointer 形式のいずれかを使用して、選択した項目を表します。 これらの形式とその形式名がで定義されている*wiadevd.h*します。

形式の名前は CFSTR WIAItemNames 形式\_WIAITEMNAMES を返しますの double 型の null で終わる一覧を指す、HGLOBAL **IWiaItem**識別子。 形式は、各識別子&lt;デバイス id&gt;::&lt;完全なパス名&gt;します。 ルートのアイテムの完全なパス名の部分は空です。

WIAItemPointer 形式は、Microsoft Windows XP 以降のバージョンでサポートされます。 形式名が CFSTR\_WIAITEMPTR します。 WIAItemPointer 形式は、(Windows SDK のドキュメントで宣言) STGMEDIUM 構造体を返しますが**tymed** TYMED にメンバーが設定されている\_ISTREAM。 ユーザーが 1 つの項目のみを選択すると、この形式を使用できます。 プロパティ シートまたはコンテキストの拡張機能を呼び出すことができます**CoUnmarshalInterface**上、 **IStream**オブジェクトを取得する STGMEDIUM 構造体に格納されている、 **IWiaItem**インターフェイス。 (Windows SDK ドキュメントの説明を参照して、 **CoUnmarshalInterface**関数、および**IStream**と**IWiaItem**インターフェイスです)。この形式を使用して、プロパティ シートのすべてのページを共有できます正しくマーシャ リングされた**IWiaItem**インターフェイスで、スキャン中には重要です。

 

 





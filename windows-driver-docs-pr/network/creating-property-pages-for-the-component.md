---
title: コンポーネントのプロパティ ページの作成
description: コンポーネントのプロパティ ページの作成
ms.assetid: f353844f-56f4-42cd-8f7d-2fa87f469d3c
keywords:
- ネットワー キング WDK オブジェクト、プロパティ ページに通知します。
- ネットワークがオブジェクトにプロパティ ページに通知します。
- プロパティ ページの WDK ネットワーク
- WDK ネットワークのプロパティ
- プロパティ ページのコールバック関数の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbbf2df400aab1e2672b19ea52c67d9e79532dc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374888"
---
# <a name="creating-property-pages-for-the-component"></a>コンポーネントのプロパティ ページの作成





通知オブジェクトは、ネットワーク構成のサブシステムの呼び出し、通知オブジェクトの後にカスタム プロパティ ページを作成します[ **INetCfgComponentPropertyUi::MergePropPages** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547746(v=vs.85))メソッド。 カスタム プロパティ ページは、コンポーネントのプロパティのページの既定のセットにマージできるシートを使用して、 **MergePropPages**メソッド。 **MergePropPages**適切なカスタム ページのマージ先の既定のページ数を返します。

カスタム プロパティのページを作成する**MergePropPages** COM を呼び出す**CoTaskMemAlloc** PROPSHEETPAGE 構造体へのハンドルのメモリを割り当てる関数。 これらのハンドルは、作成するプロパティ ページを表します。 場合**CoTaskMemAlloc**正常、ハンドルのメモリを割り当てて**MergePropPages**を宣言し、入力は**PROPSHEETPAGE**各プロパティ ページの構造体。 後**MergePropPages**構造体のこれらの塗りつぶし、Win32 呼び出し**CreatePropertySheetPage**関数の各プロパティ ページ。 この呼び出しで**MergePropPages**を作成する PROPSHEETPAGE 構造体のアドレスを渡します。

各プロパティ ページで、ダイアログ ボックスのコールバック関数を実装する必要がありますも**MergePropPages**を作成します。 ダイアログ ボックスのコールバック関数では、オペレーティング システムがそのダイアログ ボックスの関数に関連付けられているプロパティ ページに送信するメッセージを処理します。 プロパティ ページ ダイアログ ボックスの関数に関連付ける**MergePropPages**ポイントする必要があります、 **pfnDlgProc**各ページのページのダイアログ ボックスの関数に各 PROPSHEETPAGE 構造体のメンバー。

ダイアログ ボックスの関数は、次のメッセージを処理します。

-   WM\_INITDIALOG メッセージは、オペレーティング システムは、関連付けられているプロパティ ページを表示する直前に、ダイアログ ボックスの関数に送信されます。 プロパティ ページを初期化するために、プロパティ ページの外観に影響を与えるタスクを実行して、ダイアログ ボックスの機能は通常このメッセージを使用します。

-   WM\_プロパティ ページで、イベントが発生した後、ダイアログ ボックスの関数に送信される通知メッセージ。 どのようなイベントが発生したこのメッセージと共に送信されるその他の情報を識別します。 このイベントの情報は、NMHDR 構造体へのポインターに含まれます。 NMHDR にはできますプロパティ シートが含まれている情報が含まれている例。
    -   PSN\_適用イベントは、ユーザーが [ok] を閉じるクリックすることを示す、またはプロパティ ページに適用します。 ユーザーが閉じる、[ok] をクリックするか、[適用] ダイアログ ボックスの関数が呼び出すことができます、 **PropSheet\_Changed**プロパティ シートのページで情報が変更されたことを通知するためにマクロ。 この呼び出しでは、ダイアログ ボックスの関数は、プロパティ シートとページにハンドルを渡します。 ダイアログ ボックスの関数は、Win32 を呼び出すことができます**GetParent**関数し、プロパティ シートを識別するハンドルを取得するページに、ハンドルを渡します。

        ダイアログ ボックス関数では、プロパティ シートの変更について通知、ネットワーク構成のサブシステムは呼び出し、 [ **INetCfgComponentPropertyUi::ValidateProperties** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547755(v=vs.85))を確認する方法、すべての変更の有効性。 サブシステムに、通知オブジェクトの呼び出しのすべての変更が有効な場合は、 [ **INetCfgComponentPropertyUi::ApplyProperties** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547741(v=vs.85))メソッドを呼び出すすべての変更を有効にするとします。 ネットワーク構成のサブシステム呼び出し**ApplyProperties**前に、オペレーティング システムは、ダイアログ ボックスを閉じます。

        **ApplyProperties**通知オブジェクトのデータ メンバーに情報を設定して、ユーザーが入力した情報を取得するメソッドを実装することができます。

    -   PSN\_リセット イベントは、プロパティ ページを破棄しようと、オペレーティング システムがあることを示します。 ユーザーは、この操作を開始するプロパティ ページで [キャンセル] をクリックします可能性があります。 ユーザーは、[キャンセル] をクリックすると、ネットワーク構成のサブシステムを呼び出す、 [ **INetCfgComponentPropertyUi::CancelProperties** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547742(v=vs.85))メソッドを呼び出すと変更をすべて無視されます。 ネットワーク構成のサブシステム呼び出し**CancelProperties**の前に、ダイアログ ボックスが閉じられました。
    -   PSN\_KILLACTIVE イベントは、プロパティ ページが非アクティブになる直前にあることを示します。 このイベントは、ユーザーが別のページをアクティブにまたは、[ok] をクリックしたときに発生します。

*プロパティ ページのコールバック*の各プロパティ ページで、関数を実装することも**MergePropPages**を作成します。 プロパティ ページのコールバック関数は、初期化とページのクリーンアップ操作を実行します。 プロパティ ページのコールバック関数、プロパティ ページに関連付けるに**MergePropPages**ポイントする必要があります、 **pfnCallback**各ページのプロパティ ページのコールバックに各 PROPSHEETPAGE 構造体のメンバーそのページ関数です。

の詳細については、Microsoft Windows SDK ドキュメントを参照してください。

-   プロパティ ページを作成して構造体、関数、および通知のプロパティ ページ

-   コールバック プロシージャのダイアログ ボックス、メッセージ、および構造体

 

 






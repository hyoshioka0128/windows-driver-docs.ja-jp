---
title: スクラッチ パッドを使用します。
description: スクラッチ パッドを使用します。
ms.assetid: a0f6ce9c-7fad-4df6-bad8-0ea1bc5bfc52
keywords:
- デバッグ情報のウィンドウ、スクラッチ パッド
- スクラッチ パッド
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96ffc118e1fa01dc633ab4175c4f859944bb7f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536496"
---
# <a name="using-the-scratch-pad"></a>スクラッチ パッドを使用します。


## <span id="ddk_scratch_pad_dbg"></span><span id="DDK_SCRATCH_PAD_DBG"></span>


スクラッチ パッド ウィンドウを入力してテキストを保存、クリップボードです。

### <a name="span-idopeningthescratchpadwindowspanspan-idopeningthescratchpadwindowspanopening-the-scratch-pad-window"></a><span id="opening_the_scratch_pad_window"></span><span id="OPENING_THE_SCRATCH_PAD_WINDOW"></span>スクラッチ パッド ウィンドウを開く

開くかで WinDbg ウィンドウで、スクラッチ パッド ウィンドウに切り替え、**ビュー**  メニューのをクリックして**スクラッチ パッド**します。 (ALT + 8 キーを押すこともできますか、クリックして、**スクラッチ パッド (Alt + 8)** ボタン (![スクラッチ パッド ボタンのスクリーン ショット](images/tbspad.png)) ツールバーの)。

次のスクリーン ショットでは、スクラッチ パッド ウィンドウの例を示します。

![スクラッチ パッド ウィンドウのスクリーン ショット](images/window-scratchpad.png)

### <a name="span-idusingthescratchpadwindowspanspan-idusingthescratchpadwindowspanusing-the-scratch-pad-window"></a><span id="using_the_scratch_pad_window"></span><span id="USING_THE_SCRATCH_PAD_WINDOW"></span>スクラッチ パッド ウィンドウの使用

スクラッチ パッド ウィンドウでは、次の操作を行うことができます。

-   スクラッチ パッド ウィンドウで入力するには、ウィンドウのテキストを追加して、入力を開始するをクリックします。 標準的なコピーと貼り付け機能を使用することもできます。 スクラッチ パッド ウィンドウの内容は、デバッガーの操作には影響しません。 このウィンドウは、テキストの編集を支援するためだけに存在します。

-   スクラッチ パッド ウィンドウを閉じる場合、テキストは保持され、 ウィンドウを開く場合に使用します。 ファイルを関連付けることによって、スクラッチ パッド ウィンドウからテキストを保存することもできます。

スクラッチ パッド ウィンドウには、その他のコマンドのショートカット メニューがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウ (右上隅のアイコンをクリックします。![スクラッチ パッド ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/tbspad.png)). このメニューには、次のコマンドが含まれています。

-   (メニューのみ)**ファイルに関連付ける**テキスト ファイルを選択できるダイアログ ボックスを開きます。 ファイルを選択した後、スクラッチ パッドには、現在のテキストはクリアされ、選択したファイル内のテキストに置き換えられます。 入力したすべての新しいテキストにスクラッチ パッドは、このファイルに関連付けられて、スクラッチ パッドは、ファイルに保存されます。 選択するか、ファイルとの関連付けを終了することができます、**ファイルの関連付けを終了**ショート カット メニュー オプションまたはスクラッチ パッドを閉じています。

-   (メニューのみ)**ファイルの関連付けを終了**スクラッチ パッドの指定したテキスト ファイルの関連付けを終了します。 このオプションを選択する前に、スクラッチ パッドですべてのテキストは、ファイルに保存されます。 すべてのテキストに型指定されたスクラッチ パッドの関連付けが終了した後は、テキスト ファイルの保存されなくなります。

-   **ドッキング**または**ドッキング解除**によって、ウィンドウに入力するか、ドッキング状態のままにします。

-   (メニューのみ)**新しいドッキングするのには移動**スクラッチ パッドを閉じるし、新しいドッキング ステーションで開かれます。

-   (メニューのみ)**ウィンドウの種類のタブのドッキング先として設定**スクラッチ パッドでは使用できません。 このオプションは使用できますのみ[ソース](source-window.md)または[メモリ](memory-window.md)windows。

-   **常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   **フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、[、Windows の位置づけ](positioning-the-windows.md)を参照してください。

-   **ヘルプ**ツールを Windows のデバッグ ドキュメントのこのトピックを開きます。

-   **閉じる**このウィンドウを閉じます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Windows のドッキング、タブ、および浮動小数点の詳細については、[、Windows の位置づけ](positioning-the-windows.md)を参照してください。 デバッグ情報のウィンドウのコントロールに使用できるすべての手法の詳細については、[デバッグ情報の Windows を使用して](using-debugging-information-windows.md)を参照してください。

 

 






---
title: WinDbg での表示と編集を登録します
description: 、WinDbg では、表示し、コマンドを入力して、[レジスタ] ウィンドウを使用して、または [ウォッチ] ウィンドウを使用して、レジスタを編集します。
ms.assetid: bd7ced3b-7f71-4ea5-a45b-38339dc3e87c
keywords:
- デバッグ情報のウィンドウ、[レジスタ] ウィンドウ
- '[レジスタ] ウィンドウ'
- レジスタ、[レジスタ] ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 434e682405af1bff8054c49c5e6c915040a5bfd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535782"
---
# <a name="viewing-and-editing-registers-in-windbg"></a>WinDbg での表示と編集を登録します


レジスタは、CPU 上にある小さな揮発性メモリ単位です。 多くのレジスタは、特定の用途専用し、その他のレジスタが使用するユーザー モード アプリケーションで利用できます。 X86 ベースおよび x64 ベース プロセッサでは、使用可能なレジスタのさまざまなコレクションがあります。 各プロセッサの詳細については、レジスタは、次を参照してください。[プロセッサ アーキテクチャ](processor-architecture.md)します。

、WinDbg では、表示し、コマンドを入力して、[レジスタ] ウィンドウを使用して、または [ウォッチ] ウィンドウを使用して、レジスタを編集します。

## <a name="span-idcommandsspanspan-idcommandsspanspan-idcommandsspancommands"></a><span id="Commands"></span><span id="commands"></span><span id="COMMANDS"></span>コマンド


表示して入力して、レジスタを編集、 [ **r (レジスタ)** ](r--registers-.md)デバッガー コマンド] ウィンドウでコマンド。 画面をカスタマイズするには、いくつかのオプションを使用するかを使用して、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

レジスタは、ターゲットを停止するたびとも自動的に表示されます。 使用してコードをステップ実行する場合、 [ **p (ステップ)** ](p--step-.md)または[ **t (トレース)** ](t--trace-.md)コマンド、レジスタのあらゆる段階で表示を表示します。 この表示を停止するには、使用、 **r**これらのコマンドを使用する場合します。

X86 ベースのプロセッサでは、上、 **r**オプションもフラグと呼ばれるいくつかの 1 ビット レジスタを制御します。 これらのフラグを変更するには、ときに、通常のレジスタを変更するよりも若干異なる構文を使用します。 詳細については、これらのフラグとこの構文の詳細については、次を参照してください。 [x86 フラグ](x86-architecture.md#x86-flags)します。

## <a name="span-idtheregisterswindowspanspan-idtheregisterswindowspanspan-idtheregisterswindowspanthe-registers-window"></a><span id="The_Registers_Window"></span><span id="the_registers_window"></span><span id="THE_REGISTERS_WINDOW"></span>[レジスタ] ウィンドウ


### <a name="span-idopeningtheregisterswindowspanspan-idopeningtheregisterswindowspanspan-idopeningtheregisterswindowspanopening-the-registers-window"></a><span id="Opening_the_Registers_Window"></span><span id="opening_the_registers_window"></span><span id="OPENING_THE_REGISTERS_WINDOW"></span>[レジスタ] ウィンドウを開く

開くか、[レジスタ] ウィンドウに切り替えて、次のように選択します。**登録**から、**ビュー**メニュー。 (ALT + 4 キーを押すこともできます をクリックしてまたは、**登録**ボタン (![レジスタ ボタンのスクリーン ショット](images/tbreg.png))、ツールバーの。 ALT + SHIFT + 4 を閉じる [レジスタ] ウィンドウ。)

次のスクリーン ショットでは、[レジスタ] ウィンドウの例を示します。

![[レジスタ] ウィンドウのスクリーン ショット](images/window-registers.png)

[レジスタ] ウィンドウには、2 つの列が含まれています。 **Reg**列には、すべての対象となるプロセッサのレジスタが一覧表示されます。 **値**列には、各レジスタの現在の値が表示されます。 このウィンドウにも含まれています、**カスタマイズ**ツールバーを開く ボタン、**登録リストのカスタマイズ** ダイアログ ボックス。

### <a name="span-idusingtheregisterswindowspanspan-idusingtheregisterswindowspanspan-idusingtheregisterswindowspanusing-the-registers-window"></a><span id="Using_the_Registers_Window"></span><span id="using_the_registers_window"></span><span id="USING_THE_REGISTERS_WINDOW"></span>[レジスタ] ウィンドウを使用します。

[レジスタ] ウィンドウでは、次の操作を行うことができます。

-   **値**列には、各レジスタの現在の値が表示されます。 最近変更されたレジスタの値は、赤いテキストで表示されます。
    -   新しい値を入力するには、ダブルクリック、**値**セル、および、新しい値を入力または古い値を編集します。 (切り取り、コピー、および貼り付けコマンドは、編集するために使用できる)。
    -   新しい値を保存するには、ENTER キーを押します。
    -   新しい値を破棄するには、esc キーを押します。
    -   無効な値を入力すると、ENTER キーを押したときに、古い値が再び表示されます。
-   レジスタの値は、現在の基数に表示され、同じ基数に新しい値を入力する必要があります。 現在の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)デバッガー コマンド] ウィンドウでコマンド。

-   ユーザー モードでは、[レジスタ] ウィンドウには、現在のスレッドに関連付けられているレジスタが表示されます。 現在のスレッドの詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

-   カーネル モードで [レジスタ] ウィンドウを表示に現在関連付けられているレジスタ[コンテキストを登録](changing-contexts.md#register-context)します。 特定のスレッド、コンテキストのレコードを一致するように登録するコンテキストを設定したり、フレームをトラップします。 指定されたレジスタのコンテキストの最も重要なレジスタのみが実際に表示されます。その値を変更することはできません。

[レジスタ] ウィンドウが入っているツールバーを**カスタマイズ**ボタンをクリックし、その他のコマンドのショートカット メニューがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウの右上隅の近くのアイコンをクリックします (![レジスタ ウィンドウのショートカット メニューを表示するためのボタンのアイコンのスクリーン ショット](images/tbreg.png))。 ツールバーとメニューは、次のボタンとコマンドが含まれます。

-   (ツールバーとメニュー)**カスタマイズ**開きます、**登録リストのカスタマイズ**ダイアログ ボックスで、このトピックでは、次のセクションに記載されています。

-   (メニューのみ)**ツールバー**オンとオフは、ツールバーをオンにします。

-   (メニューのみ)**ドッキング**または**ドッキング解除**によって、ウィンドウに入力するか、ドッキング状態のままにします。

-   (メニューのみ)**新しいドッキングするのには移動**[レジスタ] ウィンドウを閉じ、新しいドッキング ステーションで開かれます。

-   (メニューのみ)**ウィンドウの種類のタブのドッキング先として設定**[レジスタ] ウィンドウでは使用できません。 このオプションでは、windows のソースまたはメモリの使用のみです。

-   (メニューのみ)**常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   (メニューのみ)**フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

-   (メニューのみ)**ヘルプ**ツールを Windows のデバッグ ドキュメントのこのトピックを開きます。

-   (メニューのみ)**閉じる**このウィンドウを閉じます。

### <a name="span-idcustomizeregisterlistdialogboxspanspan-idcustomizeregisterlistdialogboxspancustomize-register-list-dialog-box"></a><span id="customize_register_list_dialog_box"></span><span id="CUSTOMIZE_REGISTER_LIST_DIALOG_BOX"></span>レジスタの一覧 ダイアログ ボックスをカスタマイズします。

表示されるレジスタの一覧を変更するには、クリックして、**カスタマイズ**ボタンをクリックします。 **登録リストのカスタマイズ** ダイアログ ボックスが表示されます。

このダイアログ ボックスでは、レジスタが表示される順序を変更するレジスタの一覧を編集できます。 (を一覧から、該当するレジスタを実際に削除することはできません。 この場合、最後に表示されます)。レジスタ名の間にスペースが必要があります。

選択した場合、**変更表示値を最初に登録する** チェック ボックス、レジスタの値が変更された最も最近上部に表示します。

選択した場合、 **subregisters を表示しない**チェック ボックスをオン subregisters は表示されません。 たとえば、 **eax**は表示しない場合は**ax**、 **ah**、または**al**します。

をクリックして **[ok]** 、変更を保存または**キャンセル**変更を破棄します。

プロセッサの 1 つ以上の種類を持つマルチ プロセッサ コンピューターをデバッグする場合 WinDbg は各プロセッサの種類のカスタマイズ設定を個別に格納されます。 この分離には、同時に、各プロセッサのレジスタの表示をカスタマイズすることができます。

## <a name="span-idddkdebuggingbioscodedbgspanspan-idddkdebuggingbioscodedbgspanthe-watch-window"></a><span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>[ウォッチ] ウィンドウ


WinDbg を [ウォッチ] ウィンドウを使用して、レジスタを表示することができます。 [ウォッチ] ウィンドウを使用して、レジスタの値を変更することはできません。

[ウォッチ] ウィンドウを開くには、次のように選択します。**ウォッチ**から、**ビュー**メニュー。 ALT + 2 キーを押すこともできますかをクリックして、**ウォッチ**ツールバーのボタン:![ウォッチ式のボタンのスクリーン ショット](images/tbwatch.png)します。 ALT + SHIFT + 2 は、[ウォッチ] ウィンドウを閉じます。

次のスクリーン ショットでは、ウォッチ ウィンドウの例を示します。

![[ウォッチ] ウィンドウのスクリーン ショット ](images/window-watch.png)

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


レジスタのコンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

 

 






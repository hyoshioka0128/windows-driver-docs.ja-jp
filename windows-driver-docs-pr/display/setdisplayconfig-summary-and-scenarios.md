---
title: SetDisplayConfig の概要とシナリオ
description: SetDisplayConfig の概要とシナリオ
ms.assetid: f9bce5d4-b511-475c-8e0a-eb60765a3326
keywords:
- Windows 7 の WDK の表示、CCD Api、SetDisplayConfig 接続が表示されます。
- WDK の Windows Server 2008 R2 の表示、CCD Api、SetDisplayConfig 接続が表示されます。
- Windows 7 の WDK の表示、CCD Api、SetDisplayConfig 構成が表示されます。
- 構成するには、WDK Windows Server 2008 R2 の表示、CCD Api、SetDisplayConfig が表示されます。
- CCD WDK Windows 7 の概念の表示、SetDisplayConfig
- CCD 概念 WDK Windows Server 2008 R2 の表示、SetDisplayConfig
- SetDisplayConfig WDK Windows 7 の表示
- SetDisplayConfig WDK Windows Server 2008 R2 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 165248a1b71258c94ef524603cce17d60637c5fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365589"
---
# <a name="setdisplayconfig-summary-and-scenarios"></a>SetDisplayConfig の概要とシナリオ


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

次のセクションでは、呼び出し元が使用する方法をまとめると、 [ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig) CCD 関数を使用するためのシナリオを提供**SetDisplayConfig**します。

### <a name="span-idsetdisplayconfigsummaryspanspan-idsetdisplayconfigsummaryspansetdisplayconfig-summary"></a><span id="setdisplayconfig_summary"></span><span id="SETDISPLAYCONFIG_SUMMARY"></span>SetDisplayConfig の概要

呼び出し元が使用できる[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)トポロジとその他の表示設定を適用します。 つまり、呼び出し元が使用できます**SetDisplayConfig**トポロジ、レイアウト、印刷の向き、縦横比を設定するビット深度とにします。 呼び出し元が使用できる**SetDisplayConfig**次の操作を実行します。

-   ソースとターゲットの特定のトポロジを設定します。

-   各パスと共に、レイアウト、向き、およびスケール ファクターのソースとターゲットのモードを定義します。

-   ディスプレイの設定を適用するときに、データベースを更新します。

-   列挙されたパスを使用して構築された特定のトポロジが可能かどうかをテストします。

-   ホット キーから次の 4 つのオプションのいずれかにマップされるデータベースから最後の既知の設定を直接適用されます。

-   ターゲットの強制投影を有効にします。

-   新しいオペレーティング システムの最適なモード ロジックを呼び出します。

### <a name="span-idsetdisplayconfigscenariosspanspan-idsetdisplayconfigscenariosspansetdisplayconfig-scenarios"></a><span id="setdisplayconfig_scenarios"></span><span id="SETDISPLAYCONFIG_SCENARIOS"></span>SetDisplayConfig シナリオ

[**SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)は、次のシナリオで呼び出されます。

-   表示のコントロール パネル アプレット呼び出し[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)設定に使用できるすべてのオプションをテストする、 **multimon** ボックスの一覧。

-   表示のコントロール パネル アプレット呼び出し[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)ドロップダウン メニューから、ユーザーが選択した設定を適用します。

-   表示のコントロール パネル アプレット呼び出し[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)ユーザー インターフェイスから、ユーザーが選択した設定を適用します。 これらの設定は、解像度、レイアウト、印刷の向き、スケーリング、プライマリするには、ビット数、およびリフレッシュ レート。

-   表示がホット キーの呼び出しでユーザーが選択した後、 [ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)永続性データベースから適切な設定を適用します。

-   コントロール パネルの ユーザー タスク インターフェイス呼び出し[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)は、タスクの種類に基づいて、適切な設定を適用します。

-   表示のコントロール パネル アプレット呼び出し[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)を開始または特定のターゲットに強制プロジェクションを停止します。

 

 






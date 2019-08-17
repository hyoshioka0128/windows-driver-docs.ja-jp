---
title: SIM toolkit の概要
description: SIM toolkit の概要
ms.assetid: 39869948-d61c-438c-a90c-05dcb099acad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7eedc74a4bd6a9651ddc5c478eac63bdf0a4b0a
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565640"
---
# <a name="sim-toolkit-overview"></a>SIM toolkit の概要


SIM toolkit は、ネットワークイベントまたはユーザーのアクションによってライセンス認証を行うことができる、SIM 上の一連のアプリケーションです。 SIM toolkit アプリケーションは、3GPP および ETSI 仕様で定義されているプロアクティブコマンドによって表されます。 Windows 10 Mobile は、SIM toolkit コマンドのサブセットをサポートしています。 サポートされているコマンドの一覧については、「 [SIM toolkit コマンド](sim-toolkit-commands.md)」を参照してください。

## <a name="sim-toolkit-components"></a>SIM toolkit のコンポーネント


SIM toolkit には、次の3つの主要なコンポーネントがあります。

-   シリコンベンダが提供するモデムおよび無線インターフェイスレイヤー (RIL) ソフトウェア。

-   サービス。ネイティブコード DLL です。

-   ユーザーインターフェイス (UI)。

SIM toolkit サービスとユーザーインターフェイスは、どちらも Microsoft によって提供されます。

次の図は、SIM toolkit の主要なコンポーネントを示しています。

![sim toolkit のコンポーネント](images/sim-toolkit-components.png)

### <a name="sim-toolkit-service"></a>SIM toolkit サービス

SIM toolkit サービスは、Windows 10 Mobile OS の一部です。 バックグラウンドタスクとして実行され、SIM と SIM toolkit UI アプリケーションの間のコマンドインタープリターとして機能します。

### <a name="sim-toolkit-ui-application"></a>SIM toolkit UI アプリケーション

SIM toolkit UI には、SIM toolkit サービスによって指示されたテキストが表示されます。

SIM toolkit UI アプリケーションでは、次の2種類のテキスト文字列が表示されます。

-   アプリケーション管理文字列は、SIM toolkit UI の一部です。 Microsoft では、これらの文字列を Windows でサポートされている言語にローカライズしています。

-   SIM とのメッセージ操作の一部として表示されるテキスト文字列は、携帯電話会社が提供します。 Microsoft では、これらのテキスト文字列をローカライズしていません。

SIM toolkit UI アプリケーションは、トーンを再生し、ブラウザーを起動することもできます。

### <a name="sim-toolkit-customizations"></a>SIM toolkit のカスタマイズ

Oem は、既定値が携帯電話会社の要件を満たしていない場合に、特定のダイアログまたはメッセージの表示期間を変更できます。 これらのカスタマイズ設定は、使用する方法を選択できるように、MCSF と Windows の両方のプロビジョニングで使用できます。 既定の表示時刻は次のとおりです。

-   GETINPUT T>120秒

-   折り返し60秒

-   SELECTITEM:60秒

-   GETINKEY:60秒

これらのカスタマイズの詳細については、「 [SIM toolkit をカスタマイズする](https://docs.microsoft.com/windows-hardware/customize/mobile/mcsf/customize-the-sim-toolkit)」を参照してください。

### <a name="example-of-processing-a-sim-toolkit-command"></a>SIM toolkit コマンドを処理する例

SIM toolkit の表示テキストコマンドを処理する例を次に示します。

-   SIM によって、[テキストの表示] コマンドが送信されます。

-   SIM toolkit サービスは、表示テキストを受け取り、コマンドを SIM toolkit UI に渡します。

-   SIM toolkit UI には、テキスト文字列が表示されます。

## <a name="starting-the-sim-toolkit-ui-application"></a>SIM toolkit UI アプリケーションを起動しています


Sim toolkit UI アプリケーションがインストールされていると、**設定** &gt; **ネットワーク & ワイヤレス** &gt; **携帯電話 & sim** &gt; **詳細オプション**に **[sim アプリケーション]** ボタンが表示されます。ウィンドウ. アプリケーションを起動するには、[] ボタンをタップします。

次のいずれかに該当する場合、 **[SIM アプリケーション]** ボタンは非表示になります。

-   SIM PIN がロックされている (2G SIM 用)

-   PUK (パーソナルロック解除キー) がロックされています (2G SIM 用)

-   Sim に SIM アプリケーションがありません

-   SIM が存在しません

SIM toolkit UI アプリケーションが正常に起動すると、SIM toolkit UI にユーザーが選択するオプションが表示されます。 オプションは、SIM 上のアプリケーションによって決定されます。

## <a name="launching-the-sim-toolkit-using-another-app"></a>別のアプリを使用して SIM ツールキットを起動する


SIM toolkit をより見つけやすくするために、パートナーは予約済みの URI スキームを使用して、UWP アプリで SIM アプリケーション CPL を起動できるようにします。 これを行う方法の詳細については、「予約済み URI」を参照して、 [SIM toolkit を起動](reserved-uri-to-launch-sim-toolkit.md)してください。

## <a name="sim-toolkit-ui-notifications"></a>SIM toolkit UI の通知


Sim アプリケーション UI は、電話ダイヤラー画面で SIM コマンドを受信した場合には表示されません。 この場合、通知トーストが画面の上部に表示されます。 トーストをタップすると、SIM アプリケーション UI が起動します。 それ以外のすべてのシナリオでは、SIM toolkit UI アプリケーションが起動され、画面全体に表示されます。

## <a name="additional-reference"></a>その他の参照情報


次の設定をお勧めします。

-   テストの実行中にロック画面のタイムアウトを [なし] に設定します。これにより、ロック画面はテストに干渉しません。 既定では、1分に設定されています。

-   CDMA デバイスの場合は、APN がデバイスに設定されていることを確認します。

-   一部のテストスイートでは、タイマーの既定値が90秒に設定されています。 必要に応じて、タイムアウトのカスタマイズのレジストリ値が適切に設定されていることを確認します。

## <a name="related-topics"></a>関連トピック


[SIM toolkit のコマンド](sim-toolkit-commands.md)

 

 







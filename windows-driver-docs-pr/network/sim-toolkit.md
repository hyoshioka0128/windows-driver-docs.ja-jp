---
title: SIM ツールキット
description: SIM ツールキット
ms.assetid: 39869948-d61c-438c-a90c-05dcb099acad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 351dbe512f2009553db5ba0127db56d367b5fb10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579208"
---
# <a name="sim-toolkit"></a>SIM ツールキット


SIM toolkit には、ネットワーク イベントまたはユーザーの操作によってアクティブにできる SIM 上のアプリケーションのセットです。 SIM toolkit アプリケーションは、3 gpp と ETSI 仕様で定義されている事前対応型のコマンドで表されます。 Windows 10 Mobile には、SIM toolkit コマンドのサブセットがサポートされています。 サポートされているコマンドの一覧は、[SIM toolkit コマンド](sim-toolkit-commands.md)を参照してください。

## <a name="sim-toolkit-components"></a>SIM のツールキット コンポーネント全般


SIM toolkit の 3 つの主要なコンポーネントは次のとおりです。

-   モデムと無線シリコン ベンダーから提供された層 (RIL) ソフトウェアをインターフェイスします。

-   ネイティブ コード DLL は、サービスです。

-   ユーザー インターフェイス (UI)。

SIM toolkit サービスとユーザー インターフェイスの両方は、Microsoft によって提供されます。

次の図は、SIM toolkit の主要なコンポーネントを示しています。

![sim のツールキット コンポーネント全般](images/sim-toolkit-components.png)

### <a name="sim-toolkit-service"></a>SIM toolkit サービス

SIM toolkit サービスは、Windows 10 Mobile のオペレーティング システムの一部です。 バック グラウンド タスクとして実行し、SIM と SIM toolkit UI アプリケーションの間、コマンド インタープリターとして機能します。

### <a name="sim-toolkit-ui-application"></a>SIM toolkit UI アプリケーション

SIM toolkit UI には、SIM toolkit サービスによって指定されたテキストが表示されます。

SIM toolkit UI アプリケーションでは、2 種類のテキスト文字列が表示されます。

-   アプリケーション管理の文字列は、SIM toolkit UI の一部です。 Microsoft は、これらの文字列を Windows でサポートされる言語にローカライズします。

-   SIM とメッセージの相互作用の一部として表示されるテキスト文字列は、携帯電話会社によって提供されます。 Microsoft は、これらのテキスト文字列をローカライズしていません。

SIM toolkit UI アプリケーションは音を再生し、ブラウザーを起動できます。

### <a name="sim-toolkit-customizations"></a>SIM toolkit のカスタマイズ

Oem は、既定値は、携帯電話会社の要件を満たしていない場合、特定のダイアログ ボックスまたはメッセージの表示期間を変更できます。 これらのカスタマイズ設定 MCSF とプロビジョニングを使用する方法を選択できるように Windows の両方で利用できます。 既定の表示時間は次のとおりです。

-   GETINPUT:120 秒

-   表示テキスト。60 秒

-   SELECTITEM:60 秒

-   GETINKEY:60 秒

これらのカスタマイズについては、[カスタマイズ SIM toolkit](https://msdn.microsoft.com/library/windows/hardware/mt629102)を参照してください。

### <a name="example-of-processing-a-sim-toolkit-command"></a>SIM toolkit コマンドの処理の例

SIM toolkit 表示テキスト コマンドの処理の例を次に示します。

-   SIM では、表示するテキスト コマンドを送信します。

-   SIM toolkit サービスは、表示テキストを受信し、SIM toolkit UI にコマンドを渡します。

-   SIM toolkit UI には、テキスト文字列が表示されます。

## <a name="starting-the-sim-toolkit-ui-application"></a>SIM toolkit UI アプリケーションの起動


SIM toolkit UI アプリケーションがインストールされている場合、 **SIM アプリケーション**ボタンに表示されます、**設定** &gt; **ネットワークとワイヤレス** &gt;**移動体通信および SIM** &gt; **詳細オプション**画面。 アプリケーションを開始するには、ボタンをタップします。

**SIM アプリケーション**場合、次のいずれかのボタンは表示されません。

-   SIM 暗証番号 (pin) が (2 G SIM) のロック

-   PUK (個人的には、キーがロックを解除) (2 G SIM) のロック

-   SIM の SIM アプリケーションがありません。

-   存在しない SIM

SIM toolkit UI アプリケーションが正常に開始されると、SIM toolkit UI では、オプションを選択するユーザーを表示します。 オプションは、SIM 上のアプリケーションによって決定されます。

## <a name="launching-the-sim-toolkit-using-another-app"></a>別のアプリを使用して、SIM toolkit を起動します。


SIM toolkit を発見しやすくするためには、パートナーは CPL SIM アプリケーションを起動するのに UWP アプリを有効にするのに予約済みの URI スキームを使用できます。 これを行う方法の詳細については、[SIM toolkit を起動する予約済み URI](reserved-uri-to-launch-sim-toolkit.md)を参照してください。

## <a name="sim-toolkit-ui-notifications"></a>SIM toolkit UI の通知


電話のダイヤラー画面で SIM コマンドを受信した場合は、SIM アプリケーション UI は表示されません。 この場合は、画面の上部にある通知のトーストが表示されます。 SIM アプリケーション UI を起動、トーストをタップします。 他のすべてのシナリオでは、SIM toolkit UI アプリケーションが起動し、全体の画面に表示します。

## <a name="additional-reference"></a>その他の参照情報


次の設定がお勧めします。

-   Never にロック画面がテストに干渉しないように、テストの実行中にロック画面のタイムアウトを設定します。 既定では、1 分に設定されます。

-   CDMA デバイスは、APN がデバイスの設定を確認します。

-   テスト スイートの一部では、90 秒の既定のタイマー値があります。 該当する場合は、タイムアウトのカスタマイズのレジストリ値がそれに応じて設定を確認します。

## <a name="related-topics"></a>関連トピック


[SIM toolkit コマンド](sim-toolkit-commands.md)

 

 







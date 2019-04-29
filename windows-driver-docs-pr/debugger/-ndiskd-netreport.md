---
title: ndiskd.netreport
description: Ndiskd.netreport 拡張機能は、ネットワーク スタック全体のビジュアルのレポートを生成します。
ms.assetid: 0FC134A8-8D91-4299-8D15-4E8EDD9ED855
keywords:
- デバッグ ndiskd.netreport Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netreport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cfdd481115f52373b8b839f0bdcab1cab96da6e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335956"
---
# <a name="ndiskdnetreport"></a>!ndiskd.netreport


**! Ndiskd.netreport**拡張機能には、ネットワーク スタック全体のビジュアルのレポートが生成されます。 レポート **! ndiskd.netreport**生成された HTML ファイルは、その場所にリンクが提供されます。 HTML ファイルには、分析のため、これを共有する必要がある場合は、大規模なクラッシュ ダンプ ファイルを送信する代わりに電子メールできますので、ネットワーク スタックに関する詳細情報が含まれています。

```console
!ndiskd.netreport [-outputpath <str>] [-jsononly] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-outputpath______"></span><span id="_______-OUTPUTPATH______"></span> *-outputpath*   
レポート ファイルを記述する場所を指定します。

<span id="_______-jsononly______"></span><span id="_______-JSONONLY______"></span> *-jsononly*   
生データで HTML のみを書き込みません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

実行、 **! ndiskd.netreport**ネットワーク スタックのボックスの図を描画する拡張機能。

```console
1: kd> !ndiskd.netreport


NETWORK STACK REPORT


    Want more stuff?  Rerun with the -verbose flag
                                                                                            

    Report was saved to C:\Users\******\AppData\Local\Temp\NKDFE9F.html
    View the report                        Send in email
```

下部に、生成されたレポートを参照してください「レポートの表示」リンクをクリックします。 次の図は、クラッシュ ダンプ ファイルから生成された差分レポートを示します。 各垂直スタックは、ネットワーク アダプター、スタックのコンポーネントを示すレイヤーに分割されます。 レポートを実行するたびに、同じコンポーネントが同じ色でレンダリングされますを意味する、コンポーネントの名前をハッシュすることで、各ボックスの色が生成されます。 これは、ために問題をデバッグしている場合に簡単に特定のドライバーまたはアダプターを選択することができます。

![クラッシュ ダンプからネットワーク デバッグ レポート](images/!ndiskd-netreport-crashdump.png)

比較としては、次の図は、クラッシュ ダンプ ファイルの代わりに、アクティブなシステムから生成された差分レポートを示します。 「表示データのフロー」と「シミュレート パケット」する HTML ページの下部に、他のオプションの 2 つがあり、4 つ目は、「データ フローです」レポートの上部にあるタブがあることに注意してください。 これらのオプションが表示されていた、デバッグ対象のマシン NBL のあったため、追跡が有効になって、できる **! ndiskd.netreport**視覚的に情報を表示する NBL 追跡ログを解析します。 NBL の追跡が有効でない場合、これらのオプションは表示されません。 NBL の追跡と NBL ログの詳細については、次を参照してください。 [ **! ndiskd.nbllog**](-ndiskd-nbllog.md)します。

「データ フローの表示」ボックスをチェックして、データが送信場所のパスを確認できます。 「シミュレート パケット」ボックスをチェックするには、アニメーション化された円の上下のデータ フロー パスの移動を確認できます。 各円は、ネットワーク パケットを表します。

![アクティブなシステムからネットワーク デバッグ レポート](images/!ndiskd-netreport-activesystem.png)

作業中のシステムから 2 番目の例では、最初の例は、クラッシュ ダンプ ファイルの使用から別の相違点も表示されます。 デバッグ対象の対象コンピューターで 2 番目の例にはプロビジョニングされたカーネルは、データ フローで、スタック上のネットワーク アダプターは、Microsoft カーネル デバッグ ネットワーク アダプターを確認できるように、ネットワーク経由でデバッグします。 このアダプターは通常、カーネルのデバッグが有効になっていない、デバッグ対象のマシン上に表示します。 実際には、トラフィックがイーサネットを介して送信されるため、カーネル デバッグ ネットワーク アダプターが、デバッグ セッションのコンピューターのイーサネット アダプターを予約します。

ネットワーク スタックを視覚化し、トラフィックが流れているを参照してください。 機能を使用して、問題がありますをすばやく特定することができます。 これは、仮想スイッチまたはサーバーで、前の例よりもネットワーク図が複雑に特に役立つことができます。 たとえば、NIC チーミングを使用する Windows サーバーで複数のネットワーク スタックは、トラフィックの負荷を分散し、別のスタックに影響する 1 つのスタックの一番下にある問題がある場合に互いに交差してかどうかを確認できます。 これを示すレポートをデバッグ、ネットワークの例を表示するには、次を参照してください。[ネットワーク スタックをデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)します。 NIC チーミングの詳細については、次を参照してください。[ネットワーク サブシステムのパフォーマンスのための NIC チーミングを使用して](https://msdn.microsoft.com/library/windows/hardware/dn567652)します。

**! ndiskd.netreport**システム、概要、およびデータ フロー (該当する) 場合、ページの上部にあるその他のタブもあります。 これらのタブがさらにネットワーク スタックの状態に関する有用な情報に含まれています。 次の図は、ネットワーク インターフェイス タブの 概要 タブを示します。このタブで、テーブルでは、システムの名前と識別子のネットワーク インターフェイスの詳細についてを参照できます。

![デバッグ レポートのネットワークのネットワーク インターフェイス](images/!ndiskd-netreport-activesystem-networkinterfaces.png)

NBL の追跡は、ターゲット システムで有効にした場合に表示され、データ フロー タブは、トラフィック イベントとの詳細については、それぞれのテーブルを示しています。 次の図は、前に説明した 2 つ目の例のデバッグ レポートでのアクティブなシステムからのデータ フロー タブを示します。

![ネットワーク デバッグ レポートのデータ フロー](images/!ndiskd-netreport-activesystem-dataflows.png)

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.nbllog**](-ndiskd-nbllog.md)

[ネットワーク サブシステムのパフォーマンスのための NIC チーミングを使用してください。](https://msdn.microsoft.com/library/windows/hardware/dn567652)

 

 







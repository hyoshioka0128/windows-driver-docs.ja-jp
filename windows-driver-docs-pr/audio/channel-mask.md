---
title: チャネル マスク
description: チャネル マスク
ms.assetid: 875ed000-ac53-4365-8381-3fe08d45cbcc
keywords:
- データ形式の WDK オーディオ
- WDK のオーディオ、データを書式設定します。
- オーディオ データ形式 WDK
- WDK のオーディオ、マルチ チャネルを書式設定します。
- マルチ チャネルの形式の WDK オーディオ
- ホーム シアター システム WDK オーディオ
- スピーカーの WDK オーディオ、ホーム threater システム
- オーディオ ドライバー WDK、ホーム シアター システム
- WDM オーディオ ドライバー WDK、ホーム シアター システム
- ホーム シアターを 7.1 スピーカー WDK オーディオ
- 全体の構成を 7.1 スピーカー WDK オーディオ
- スピーカー WDK オーディオの全体の構成
- LFE スピーカー
- サブウーファー WDK オーディオ
- 形式の WDK オーディオの録音
- WDK オーディオを再生
- チャネル マスク WDK オーディオ
- マスク ビット WDK オーディオ
- PCM の形式の WDK オーディオ
- WDK オーディオの位置
- データ形式の WDK オーディオ、チャンネル マスク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6154059f7b282e3bef75a8c295868f67129fa26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539430"
---
# <a name="channel-mask"></a>チャネル マスク


Windows、 [ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)構造は、マルチ チャネル、PCM のオーディオ ストリームのデータ形式を定義します。 この構造体は、PCM あたりのビット数のサンプル、ストリーム、およびチャネル マスク内のチャネルの数などのパラメーターを指定します。 チャネル マスクには、スピーカーへのチャネルのマッピングを指定します。 次の図は、チャネル マスクに個別のビットを示します。

![チャネル マスク内の個々 のビットを示す図](images/spkrcfg3.png)

チャネル マスク内の各ビットは、特定のスピーカー位置を表します。 その位置を表すマスクのビットが 1; に設定されている場合は、マスクは、特定のスピーカー位置にチャネルを割り当てます、未割り当てのスピーカー位置のすべてのマスク ビットが 0 に設定されます。 WAVEFORMATEXTENSIBLE 構造上の図に示されていないチャネル マスクのビット数を定義しますが、これらのビット ディスカッションのホーム シアターのスピーカー構成の影響はありません。 してわかりやすくするため省略しています。

スピーカー位置を前の図に、チャネル マスク内のエンコーディングは、プロパティの値に使用するときと同様、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff537250)プロパティ要求。 詳細については、次を参照してください。 [ **KSAUDIO\_チャネル\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff537083)します。

次の表は、前の図に、マスクのビットごとの意味を示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット数</th>
<th align="left">スピーカー位置</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>FL</p></td>
<td align="left"><p>表面左</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>FR</p></td>
<td align="left"><p>前面の右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>FC</p></td>
<td align="left"><p>フロント センター</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>LFE</p></td>
<td align="left"><p>低頻度の効果</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>BL</p></td>
<td align="left"><p>左に戻る</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>BR</p></td>
<td align="left"><p>右に戻る</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>FLC</p></td>
<td align="left"><p>前面がセンターの左</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>FRC</p></td>
<td align="left"><p>Center の右の前面</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>ビジネス継続性</p></td>
<td align="left"><p>Center をバックアップします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>SL</p></td>
<td align="left"><p>左にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>記憶域レプリカ</p></td>
<td align="left"><p>右側にあります。</p></td>
</tr>
</tbody>
</table>

 

たとえば、**ホーム シアターの 7.1 スピーカー** 0x63F で、次のスピーカー位置 (と次の順序で) ストリームに 8 つのチャネルが割り当てられていることを示しますのチャネル マスクの値によって構成が説明されています。:FL、FR、FC、LFE、BL、BR、SL、および SR. 氏 別の例として、**全体の構成の 7.1 スピーカー**構成はチャネル マスクの値は 0 xff は、次のスピーカー位置をストリームに 8 つのチャネルが割り当てられていることを示します。FL、FR、FC、LFE、BL、BR、FLC、および FRC

次の図は、チャネル マスク 0x63F 間の通信と**ホーム シアターの 7.1 スピーカー**構成します。

![7.1 ホーム シアターのスピーカーの記録と再生を示す図](images/spkrcfg4.png)

上記の図の左側にあるがオーディオの録音にコンテンツの表示、**ホーム シアターの 7.1 スピーカー**ストリーム形式。 グリッドの中央に小さな円では、リスナーの位置を表します。 各小規模、黒の四角形は、マイクを表します。 8 つのチャネルには、0 から 7 への番号が付けられます。 0、FR マイク レコードへのチャネルに FL マイク レコードでは、チャンネル 1 など。

上記の図の右側にある、8 スピーカー サラウンド構成を通じて再生される同じ 7.1 チャネル ストリームを示します。 この場合は、それぞれ小さな、黒の四角形は、講演者を表します。 スピーカーの 7 は、リスナーを囲むグリッド上の位置にマップされます。 マッピングが LFE スピーカー (サブウーファー); にグリッドの位置を割り当てられませんこの省略は、これらのスピーカーが通常は矢印無しのみ頻度の低いサウンドを生成することを前提に基づいています。

 

 





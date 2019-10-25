---
title: チャネル マスク
description: チャネル マスク
ms.assetid: 875ed000-ac53-4365-8381-3fe08d45cbcc
keywords:
- データ形式 WDK オーディオ
- WDK オーディオ、データをフォーマットします
- WDK のオーディオデータ形式
- WDK オーディオ、マルチチャネルをフォーマットします。
- マルチチャネル形式 WDK オーディオ
- ホームシアターシステム WDK オーディオ
- スピーカー WDK オーディオ、ホーム-月、システム
- オーディオドライバー WDK、ホームシアターシステム
- WDM オーディオドライバー WDK、ホームシアターシステム
- 7.1 ホームシアタースピーカー WDK オーディオ
- 7.1 wide 構成スピーカー WDK オーディオ
- wide 構成スピーカー WDK オーディオ
- LFE スピーカー
- subwoofers WDK オーディオ
- 記録形式 WDK オーディオ
- WDK オーディオの再生
- チャネルマスク WDK オーディオ
- マスク bits WDK オーディオ
- PCM 形式 WDK オーディオ
- WDK オーディオを配置する
- データ形式 WDK オーディオ、チャネルマスク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9697219ee6b7bdfe1a83e88d1436b354e19d38b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833639"
---
# <a name="channel-mask"></a>チャネル マスク


Windows では、 [**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体によって、マルチチャネル PCM オーディオストリームのデータ形式が定義されます。 この構造体は、PCM サンプルあたりのビット数、ストリーム内のチャネル数、チャネルマスクなどのパラメーターを指定します。 チャンネルマスクは、チャンネルとスピーカーのマッピングを指定します。 次の図は、チャネルマスク内の個々のビットを示しています。

![チャネルマスク内の個々のビットを示す図](images/spkrcfg3.png)

チャネルマスクの各ビットは、特定のスピーカーの位置を表します。 マスクが特定のスピーカー位置にチャネルを割り当てる場合、その位置を表すマスクビットが1に設定されます。割り当てられていないスピーカーの位置のすべてのマスクビットが0に設定されます。 WAVEFORMATEXTENSIBLE 構造体は、前の図に示されていないチャネルマスクの追加のビットを定義しますが、これらのビットはホームシアタースピーカーの構成については説明しません。わかりやすくするために省略されています。

前の図のチャネルマスクでのスピーカーの位置のエンコードは、 [**Ksk プロパティ\_AUDIO\_channel\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)プロパティ要求のプロパティ値に使用されるものと似ています。 詳細については、「 [**Ksk audio\_CHANNEL\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)」を参照してください。

次の表は、前の図の各マスクビットの意味を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット番号</th>
<th align="left">スピーカーの位置</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>FL</p></td>
<td align="left"><p>前面へ移動</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>FR</p></td>
<td align="left"><p>フロント右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>FC</p></td>
<td align="left"><p>フロントセンター</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>LFE</p></td>
<td align="left"><p>低頻度の効果</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
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
<td align="left"><p>中央のフロント左</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>FRC</p></td>
<td align="left"><p>中央のフロント右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>BC</p></td>
<td align="left"><p>バックセンター</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>法</p></td>
<td align="left"><p>左揃え</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>SR</p></td>
<td align="left"><p>左右</p></td>
</tr>
</tbody>
</table>

 

たとえば、 **7.1 ホームシアタースピーカー**の構成は、"0x63f" というチャネルマスク値によって示されます。これは、ストリーム内の8個のチャネルが、FL、FR、FC、LFE、BL、BR の各スピーカーの位置に割り当てられていることを示します。、SL、および SR。 別の例では、 **7.1 wide configuration スピーカー**の構成は、チャネルマスクの値が0xff で表されます。これは、ストリーム内の8個のチャネルが、FL、FR、FC、LFE、BL、BR、FLC、FRC の各スピーカーの位置に割り当てられていることを示します。

次の図は、チャネルマスク0x63F と**7.1 ホームシアタースピーカー**構成の対応を示しています。

![7\.1 ホームシアタースピーカーの記録と再生を示す図](images/spkrcfg4.png)

前の図の左側には、 **7.1 ホームシアタースピーカー**のストリーム形式でのオーディオコンテンツの記録が示されています。 グリッドの中心にある小さい円は、リスナーの位置を表します。 各小さい黒い四角形はマイクを表します。 8つのチャネルには、0 ~ 7 の番号が付けられます。 FL マイクはチャネル0に記録され、FR マイクは channel 1 に記録されます。

上の図の右側には、8スピーカーのサラウンド構成で再生される同じ7.1 チャネルストリームが示されています。 この場合、それぞれの小さい四角形、黒い四角形はスピーカーを表します。 スピーカーの7つは、リスナーを囲むグリッド上の位置にマップされます。 このマッピングでは、LFE スピーカー (サブウーファー) にグリッド位置が割り当てられません。この省略は、通常、これらのスピーカーが低頻度のサウンド (無指向性) のみを生成するという前提に基づいています。

 

 





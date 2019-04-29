---
title: 音声の割り当て
description: 音声の割り当て
ms.assetid: fb1e6c36-02b4-41a6-b9c4-09f393d389db
keywords:
- DirectMusic カーネル モードの WDK 音声、音声割り当て
- カーネル モード シンセサイザー WDK 音声、音声割り当て
- 音声割り当て WDK オーディオ
- ハードウェア アクセラレータ WDK オーディオ
- ミニポート ドライバー WDK オーディオ、カーネル モード ハードウェア アクセラレーション
- シンセサイザー WDK オーディオ、カーネル モードのハードウェア アクセラレーション
- シンセサイザー WDK の音声、音声の割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b55579b261ddf9fe7e45bd5ba010ce5332da8f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335237"
---
# <a name="voice-allocation"></a>音声の割り当て


## <span id="voice_allocation"></span><span id="VOICE_ALLOCATION"></span>


シンセサイザーのミニポート ドライバーが含まれているほとんどのアダプターのドライバーには、DirectSound のハードウェア高速化も含まれます。 シンセサイザーの音声とハードウェア アクセラレータによる DirectSound バッファー間の音声の割り当ての質問が表示されます。

DirectMusic シンセサイザー - ハードウェアとソフトウェアの両方の同時実行クライアントの数を最大化するための複数のインスタンスをサポートする必要があります。 シンセサイザー ライターでは、音声シンセサイザーを静的に割り当てることはしたくなるかもしれませんが、共通の動的な音声プールからの図面としてシンセサイザーの使用可能なすべてのインスタンスを考慮する必要があります可能性があります。 各インスタンスは、プールの合計数と、音声の使用可能な数を報告します。

この方法を実装すると、物理的なボイスの限られた数のハードウェア シンセサイザーでもは多数のシンセサイザーのインスタンスをサポートできます。 リアルタイムの STATS 呼び出しに音声を各インスタンス数のクライアントが現在使用して通知します。 動的プールが使い果たされてシンセサイザー インスタンスには、新しい音声が必要な場合は、そのシンセサイザー インスタンスからそのインスタンス内の音声を解放する音声スティー リング スキームを実装しなければなりません。

次の割り当てる方式は、音声シンセサイザーで使用されるより簡単に共有されることが DirectSound バッファーよりもドライバーはどのようなデータはどのような音声と音声を盗む (DLS レベルに記載されているに関する意思決定を行えるを制御するための考え方に基づいた1 仕様)。

すべて、音声、ミニポート ドライバー (ハードウェア、ソフトウェア、またはハードウェアとソフトウェアの組み合わせ) を使用できるは、2 つのプールに分割されます。 最初のプールの空きプールは、どこでもコミットされていないボイスで構成されます。 シンセサイザーのインスタンスでコミットを使用する音声の 2 つ目のプールでは、動的のプールで構成されます。 これらの音声は、シンセサイザー インスタンスによって使用されるのでは現在ありません。 動的プールの空きプールの現在の内容に従って、任意のシンセサイザー インスタンスによって要求された音声の最大数とサイズします。 DirectSound バッファーを割り当て時に空きプールから削除され、割り当て解除で返されます。

次の表には、実際には、スキームを示す音声割り当ての一連例にはが含まれています。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">時間</th>
<th align="left">要求</th>
<th align="left">空きプール</th>
<th align="left">動的プール</th>
<th align="left">ミニポート ドライバー アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>T0</p></td>
<td align="left"><p>電源を入れます</p></td>
<td align="left"><p>64</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T1</p></td>
<td align="left">DSound (4)</td>
<td align="left"><p>60</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>DirectSound バッファーを 4 つの音声を静的に割り当てます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T2</p></td>
<td align="left">シンセサイザー (32)</td>
<td align="left"><p>28</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>32 の音声を動的にプールを増やします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T3</p></td>
<td align="left">シンセサイザー (24)</td>
<td align="left"><p>28</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>操作はありません。 動的プールでは 24 個以上の音声が既に存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T4</p></td>
<td align="left">DSound (24)</td>
<td align="left"><p>4</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>DirectSound バッファーへの 24 の音声を静的に割り当てます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T5</p></td>
<td align="left">シンセサイザー (48 個)</td>
<td align="left"><p>0</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>36 の音声を動的にプールを増やします。 (ポートを作成するメソッドは、S_FALSE を返すし、DMUS_PORTPARAMS を設定します。<strong>dwVoices</strong> = 36)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>T6</p></td>
<td align="left">DSound (10)</td>
<td align="left"><p>0</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>失敗します。 空きプール内の音声がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>T7</p></td>
<td align="left">DSound (-5)</td>
<td align="left"><p>5</p></td>
<td align="left"><p>36</p></td>
<td align="left"><p>5 つの音声を解放します。 許可された複数の最後の要求 (時 T5) 場合でもこれらが動的のプールに戻す説明しないでに注意してください。</p></td>
</tr>
</tbody>
</table>

 

DirectSound バッファーが 1 つずつを実際に割り当てられた、読みやすくするために、テーブルにまとめられていることに注意してください。

シンセサイザー暗証番号 (pin) のインスタンスを作成すると、直後に音声割り当てる必要があるないそれに基づきます。 作成後すぐ、 [ **KSPROPERTY\_シンセサイザー\_PORTPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff537405)プロパティ項目を受信します。 このプロパティの項目には、このインスタンスに関連付けられているボイスの数がその他のものを示します。 この項目は、すべての音声要求された場合に、動的プールの実際の新しいサイズを報告する機会を割り当てられていないミニポート ドライバーも提供します。

 

 





---
title: KSEVENT\_チューナー\_開始\_スキャン
description: KSEVENT\_チューナー\_開始\_スキャン イベントが、ドライバーがスキャン操作を開始して、ユーザー モードのクライアント ドライバーには、チューニングのデバイスに関連付けられたときに、スキャン操作が完了すると通知を要求します。
ms.assetid: 63f6917e-30d2-4734-92fa-49a4291efafd
keywords:
- KSEVENT_TUNER_INITIATE_SCAN ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSEVENT_TUNER_INITIATE_SCAN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff8630acc99a3a65d13de67cb18ad7c26fe170da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553849"
---
# <a name="kseventtunerinitiatescan"></a>KSEVENT\_チューナー\_開始\_スキャン


KSEVENT\_チューナー\_開始\_スキャン イベントが、ドライバーがスキャン操作を開始して、ユーザー モードのクライアント ドライバーには、チューニングのデバイスに関連付けられたときに、スキャン操作が完了すると通知を要求します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>イベント記述子の種類</th>
<th>イベント値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561901" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561901)"><strong>KSEVENT_TUNER_INITIATE_SCAN_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

すべてのスキャン要求は、非ブロッキング必要があります。 ドライバーは、スキャン操作が制御を返す前に完了するを待ちません。 実際には、ドライバーで別のスレッドを使用して、スキャン操作を実行する必要があります。

一方、KSEVENT\_チューナー\_開始\_スキャン イベントがの独立した[ **KSPROPERTY\_チューナー\_頻度**](ksproperty-tuner-frequency.md)、KSEVENT\_チューナー\_開始\_スキャンに対応する、 **KS\_チューナー\_チューニング\_EXACT**チューニングでは、フラグ、 **TuningFlags**のメンバー、 [ **KSPROPERTY\_チューナー\_頻度\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565839)構造体。 これは、スキャンは常にしようとする次のチャネルの正確な頻度を決定することを意味します。 ドライバーによって、チューニングのデバイスに続くチューニング戦略を制御することも、(KS\_チューナー\_戦略\_ドライバー\_から調整、**戦略**のメンバー[ **KSPROPERTY\_チューナー\_モード\_CAP\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872)構造)。 これらの固定のフラグと戦略が後に常に別のフラグと戦略を使用してコントロールする場合でも**KSPROPERTY\_チューナー\_頻度**します。

つまり、KSTUNER\_チューニング\_フラグと KSTUNER\_戦略値 KSEVENT の動作には影響しません\_チューナー\_開始\_をスキャンします。

***<em>入力候補および状態</em>***

スキャンの status プロパティ[ **KSPROPERTY\_チューナー\_スキャン\_状態**](ksproperty-tuner-scan-status.md)現在頻度とシグナル ロックの状態に関する情報を提供します。 アプリケーションが、KSPROPERTY からロックの状態をクエリ\_チューナー\_スキャン\_STATUS プロパティ。 またクエリを実行[ **KSPROPERTY\_チューナー\_標準\_モード**](ksproperty-tuner-standard-mode.md)プロパティについては、信号標準の自動検出します。 信号が見つからないかどうか、KSPROPERTY、要求された範囲\_チューナー\_スキャン\_状態プロパティが返す、**チューナー\_LockType\_None** 内の値**LockStatus**のメンバー、 [ **KSPROPERTY\_チューナー\_スキャン\_状態\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565898)構造体。 チューニングのデバイスが信号をチューナーの標準を自動的に検出代替の標準でのシグナルが見つかった場合は、チューニング デバイス自体がへの要求を処理できる、 [ **KSPROPERTY\_チューナー\_標準**](ksproperty-tuner-standard.md)プロパティ。 チューニングのデバイスはを超えて段階的に、ロック、ループ (PLL) ロックでは、先に進むこと可能性がありますが、標準が不明指定可能性があります。 または、チューニングのデバイスは標準の異なるシグナルに自動調整可能性があります。 また、チューニングのデバイスがそのシグナル標準に完全なロックを取得でもと代替の標準を決定可能性があります。 このような状況は、周波数範囲にシグナルで複数の標準がある場合に発生する可能性です。

***<em>境界条件</em>***

ドライバーでは、アプリケーションが範囲外のチャネルの中心周波数が検出されると場合、ドライバーする必要がありますシグナルを無視し、次のシグナルに移動ドライバーでは、指定した範囲内で可能な最も近いは返されませんする必要があります。 ドライバーは、アプリケーションがチャネルの一覧をコンパイルしようとした場合、チャネルの重複するカウントを回避するために次のシグナルに移動する必要があります。

同じ理由で、アプリケーションは、期待されるチャネルの半分の帯域幅によってクエリの範囲をシフトする必要があります (約 6/2 = 3 のアナログおよびデジタル テレビ MHz)、ハードウェアに信号が検出した場合に特にが二重チャネルがないことを確認するカウントをハードウェアデコードできません。 このような状況では、ドライバーは、特定のチャンネルを二重にカウントを回避するが困難なをは。

***<em>複数の標準のスペクトル</em>***

たびに新しいチャネル、スキャン操作が完了する必要があります。 または信号を検出します。 ドライバーがを介してスキャン状態に戻ります、 [ **KSPROPERTY\_チューナー\_スキャン\_状態**](ksproperty-tuner-scan-status.md)プロパティ。 場合でも、ドライバーは、新しく見つかったチャネルでは、以前に適用された標準が一致しないことを決定します。 新しいチャネルが検出されるたびに、スキャンが完了する必要があります。 アプリケーションでは、新しいチャネル情報を処理する必要があり、標準的な信号と同じで別のチャネルを探すスキャン要求を再送信する必要があります。

## <a name="see-also"></a>関連項目


[**KSEVENT\_チューナー\_開始\_スキャン\_S**](https://msdn.microsoft.com/library/windows/hardware/ff561901)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**KSPROPERTY\_チューナー\_スキャン\_状態**](ksproperty-tuner-scan-status.md)

[**KSPROPERTY\_チューナー\_スキャン\_キャップ**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY\_チューナー\_標準**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_チューナー\_標準\_モード**](ksproperty-tuner-standard-mode.md)

 

 







---
title: バグチェック 0x19 BAD_POOL_HEADER
description: BAD_POOL_HEADER バグチェックの値は0x00000019 です。 これは、プールヘッダーが破損していることを示します。
ms.assetid: a3e84703-d778-426b-80e6-e143f5d8f869
keywords:
- バグチェック 0x19 BAD_POOL_HEADER
- BAD_POOL_HEADER
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- BAD_POOL_HEADER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a066f2700b6698cdc3adb9155349d00ce95a0b9e
ms.sourcegitcommit: a54b96c52b0c7009dfa05bcc68d210b13711f2ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77601720"
---
# <a name="bug-check-0x19-bad_pool_header"></a>バグチェック 0x19: 無効な\_プール\_ヘッダー

無効な\_プール\_ヘッダーのバグチェックの値が0x00000019 になっています。 これは、プールヘッダーが破損していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="bad_pool_header-parameters"></a>\_プール\_ヘッダーパラメーターが正しくありません

パラメーター1は違反の種類を示します。 他のパラメーターの意味は、パラメーター1の値によって異なります。

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
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>チェックされるプールエントリ</p></td>
<td align="left"><p>プールブロックのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>特別なプールパターンチェックに失敗しました。</p>
<p>(所有者がプールブロックを破損している可能性があります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>チェックされるプールエントリ</p></td>
<td align="left"><p>読み取り戻る<strong>flink</strong> freelist 値</p></td>
<td align="left"><p>読み取り戻る<strong>点滅</strong>の freelist 値</p></td>
<td align="left"><p>プール freelist が破損しています。</p>
<p>(正常な一覧では、パラメーター2、3、および4の値は同一である必要があります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>プールエントリの1つ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>その他のプールエントリ</p></td>
<td align="left"><p>隣接するプールエントリのペアには、互いに矛盾するヘッダーがあります。 少なくとも1つは破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>誤って計算された1つのエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>誤差の原因となった無効なエントリ</p></td>
<td align="left"><p>プールブロックヘッダーの前のサイズが大きすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>無効なプールエントリ</p></td>
<td align="left"><p>プールブロックヘッダーのサイズが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>無効なプールエントリ</p></td>
<td align="left"><p>プールブロックヘッダーのサイズが0です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>誤って計算された1つのエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>誤差の原因となった無効なエントリ</p></td>
<td align="left"><p>プールブロックヘッダーのサイズが破損しています (大きすぎます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>検出されたプールエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールエントリを含む必要があるページの仮想アドレス</p></td>
<td align="left"><p>プールブロックヘッダーのサイズが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD、0Xd、0Xf です、0x23、0x24、0x25</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>解放されたブロックのプールヘッダーは、解放された後で変更されています。 これは、通常、解放されたブロックの前の所有者のエラーではありません。代わりに、解放されたブロックがオーバーランする前のブロックにより、通常は (常にではありませんが) 発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>検出されたプールエントリ</p></td>
<td align="left"><p>次のプールエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールブロックヘッダーのサイズが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0X21</p></td>
<td align="left"><p>解放されているプールポインター</p></td>
<td align="left"><p>プールブロックに割り当てられたバイト数</p></td>
<td align="left"><p>プールブロックの後に破損した値が見つかりました</p></td>
<td align="left"><p>解放されているプールブロックに続くデータが破損しています。 通常、これはコンシューマー (呼び出し履歴) がブロックをオーバーランさせることを意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0X22</p></td>
<td align="left"><p>解放されているアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>解放されているアドレスに追跡エントリがありません。 これは、通常、呼び出し履歴が既に解放されているポインター、またはから開始するように割り当てられていないポインターを解放しようとしているためです。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

現在の要求の時点で、プールは既に破損しています。

これは、呼び出し元によって異なる場合があります。

<a name="resolution"></a>解決方法
----------

内部プールリンクは、問題の考えられる原因を解明するために、カーネルデバッガーを使用してウォークする必要があります。

その後、問題のあるプールタグに特別なプールを使用するか、問題のあるドライバーでドライバー検証ツールの "特別なプール" オプションを使用することができます。 [ **! 分析**](-analyze.md)拡張機能は、問題のあるドライバーを特定するのに役立つ場合がありますが、多くの場合、プール corrupters の場合はそうではありません。

「 [**Blue Screen Data**](blue-screen-data.md) 」で説明されている手順を使用して、Stop コードパラメーターを収集します。 Stop コードパラメーターを使用して、追跡する特定の種類のコード動作を決定します。

**ドライバーの検証ツール**

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 ドライバーコードの実行中にエラーが発生した場合は、ドライバーコードのその部分をさらに詳しく調べることを許可する例外が事前に作成されています。 Driver verifier マネージャーは Windows に組み込まれており、すべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 *verifier* 」と入力します。 確認するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバー数を試してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

**Windows メモリ診断**

このバグチェックが一貫して表示されない場合は、問題のある物理メモリに関連している可能性があります。

Windows メモリ診断ツールを実行して、メモリをテストします。 コントロールパネルの検索ボックスに「Memory」と入力し、 **[コンピューターのメモリの問題を診断する]** をクリックします。テストの実行後、イベントビューアーを使用して、システムログの下に結果を表示します。 結果を表示するには、 *Memorydiagnostics-results*エントリを探します。

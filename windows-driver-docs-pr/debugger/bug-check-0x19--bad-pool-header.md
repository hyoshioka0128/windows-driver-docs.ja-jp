---
title: バグ チェック 0x19 BAD_POOL_HEADER
description: BAD_POOL_HEADER のバグ チェックでは、0x00000019 の値を持ちます。 これは、プールのヘッダーが壊れていることを示します。
ms.assetid: a3e84703-d778-426b-80e6-e143f5d8f869
keywords:
- (開発者向けコンテンツ)バグ チェック 0x19 BAD_POOL_HEADER
- BAD_POOL_HEADER
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- BAD_POOL_HEADER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b64fb39b576b67b81776ee55f7052e0c60f74172
ms.sourcegitcommit: 91db84a97ce13a851f500acd4af67aa0b0a05aa8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "58319234"
---
# <a name="developer-content-bug-check-0x19-badpoolheader"></a>(開発者向けコンテンツ)0x19 チェックをバグします。不適切な\_プール\_ヘッダー


不適切な\_プール\_ヘッダーのバグ チェックが 0x00000019 の値を持ちます。 これは、プールのヘッダーが壊れていることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="badpoolheader-parameters"></a>不適切な\_プール\_ヘッダー パラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>チェックされているプール エントリ</p></td>
<td align="left"><p>プールのブロックのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>特別なプールのパターンのチェックに失敗しました。</p>
<p>(所有者は、プールのブロックを破損が可能性があります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>チェックされているプール エントリ</p></td>
<td align="left"><p>読み戻し<strong>flink</strong> freelist 値</p></td>
<td align="left"><p>読み戻し<strong>点滅</strong>freelist 値</p></td>
<td align="left"><p>プール空きリストが壊れています。</p>
<p>(正常な状態の一覧でパラメーター 2、3、および 4 の値と同じなります。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>1 つのプール エントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>その他のプール エントリ</p></td>
<td align="left"><p>2 つの隣接するプールのエントリには、互いに矛盾するヘッダーがあります。 少なくとも 1 つが壊れています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>1 つの計算が正しくないエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>計算式の原因となった無効なエントリ</p></td>
<td align="left"><p>プールのブロック ヘッダーの前のサイズが大きすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>無効なプール エントリ</p></td>
<td align="left"><p>プールのブロック ヘッダーのサイズが壊れています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>無効なプール エントリ</p></td>
<td align="left"><p>プールのブロック ヘッダーのサイズには 0 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>1 つの計算が正しくないエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>計算式の原因となった無効なエントリ</p></td>
<td align="left"><p>プールのブロック ヘッダーのサイズが破損しています (これが大きすぎます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>検出されたプール エントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールのエントリが含まれている必要がありますページの仮想アドレス</p></td>
<td align="left"><p>プールのブロック ヘッダーのサイズが壊れています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xd、0xE、0 xf、0x23、0x24、0x25</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>それが解放された後、解放されたブロックのプールのヘッダーは変更されています。 一般的にはこれが、解放されたブロック; の以前の所有者の障害になることはありません。代わりには、通常 (必ずではありません) により、ブロックの前に、解放されたブロックのオーバーランが発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>検出されたプール エントリ</p></td>
<td align="left"><p>プールの次のエントリ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールのブロック ヘッダーのサイズが壊れています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0X21</p></td>
<td align="left"><p>解放されてプールへのポインター</p></td>
<td align="left"><p>プールのブロックに割り当てられたバイト数</p></td>
<td align="left"><p>次のプールのブロックが見つかりました破損した値</p></td>
<td align="left"><p>解放されてプールのブロックの後のデータが壊れています。 通常、コンシューマー (コール スタック) が、ブロックをオーバーラン意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0X22</p></td>
<td align="left"><p>解放されているアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>解放されているアドレスの追跡のエントリではありません。 呼び出し履歴が既に解放されたか、始めに割り当てられていないポインターを解放しようとしたため、通常です。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

プールは既に現在の要求時に破損しています。

これは、呼び出し元によりできない可能性がありますもかまいません。

<a name="resolution"></a>解決方法
----------

カーネル デバッガーを使用して、問題の考えられる原因を解明内部プールへのリンクを処理する必要があります。

問題のあるプール タグの特別なプールを使用したり、Driver Verifier を使用し、問題のあるドライバーの「特別なプール」オプション。 [ **! 分析**](-analyze.md)未確認のドライバーを特定することでヘルプの拡張機能がありますが、これは頻繁にプール corrupters の場合。

説明する手順を使用して、 [**青い画面データ**](blue-screen-data.md)停止コード パラメーターを収集します。 停止コード パラメーターを使用して、コードの動作追跡するために作業しているは、特定の種類を決定します。

**ドライバーの検証ツール**

Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 ドライバー コードの実行でエラーが参照してください、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifier*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)を参照してください。

**Windows メモリ診断**

このバグ チェックが一貫性なく表示されている場合は、物理メモリを関係可能性があります。

メモリをテストする、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして **、コンピューターのメモリの問題を診断**します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

 

 





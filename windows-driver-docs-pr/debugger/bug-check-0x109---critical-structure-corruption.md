---
title: バグチェック 0x109 CRITICAL_STRUCTURE_CORRUPTION
description: CRITICAL_STRUCTURE_CORRUPTION バグチェックの値は0x00000109 です。 これは、カーネルが重要なカーネルコードまたはデータの破損を検出したことを示します。
ms.assetid: 38d4d722-a915-4f17-899b-2a0b4aa69d95
keywords:
- バグチェック 0x109 CRITICAL_STRUCTURE_CORRUPTION
- CRITICAL_STRUCTURE_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CRITICAL_STRUCTURE_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a1d3a0577d7b6481c146fa1cb7c11c8ae167313
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534665"
---
# <a name="bug-check-0x109-critical_structure_corruption"></a>バグチェック 0x109: 重大な \_ 構造の \_ 破損


重大な \_ 構造 \_ 破損のバグチェックには、0x00000109 の値が含まれています。 これは、カーネルが重要なカーネルコードまたはデータの破損を検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="critical_structure_corruption-parameters"></a>重大な \_ 構造の \_ 破損パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>破損した領域の型。 (このページの後の表を参照してください)。</p></td>
</tr>
</tbody>
</table>

 

パラメーター4の値は、破損した領域の種類を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター4</th>
<th align="left">破損した領域の種類、破損の種類、または破損の原因となった操作の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>汎用データ領域</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>関数の変更または Itanium ベースの関数の場所</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>プロセッサ割り込みディスパッチテーブル (IDT)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>プロセッサのグローバル記述子テーブル (GDT)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>種類1のプロセス一覧の破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>タイプ2のプロセス一覧の破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>デバッグルーチンの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>重要な MSR の変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>オブジェクトの種類</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>プロセッサ IVT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>システムサービス関数の変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>汎用セッションデータ領域</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xC</p></td>
<td align="left"><p>セッション関数または pdata の変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xD</p></td>
<td align="left"><p>インポートテーブルの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xE</p></td>
<td align="left"><p>セッションインポートテーブルの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xF</p></td>
<td align="left"><p>Ps Win32 のコールアウトの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>デバッグスイッチルーチンの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>IRP アロケーターの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x12</p></td>
<td align="left"><p>ドライバー呼び出しディスパッチャーの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x13</p></td>
<td align="left"><p>IRP 完了ディスパッチャーの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x14</p></td>
<td align="left"><p>IRP デアロケーターの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15</p></td>
<td align="left"><p>プロセッサコントロールレジスタ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x16</p></td>
<td align="left"><p>重大な浮動小数点コントロールのレジスタの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x17</p></td>
<td align="left"><p>ローカルの APIC 変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>カーネル通知の吹き出しの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>読み込まれたモジュールの一覧の変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>種類3プロセス一覧の破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>種類4プロセス一覧の破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>ドライバーオブジェクトの破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>エグゼクティブコールバックオブジェクトの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>モジュールの埋め込みの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>保護されたプロセスの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>汎用データ領域</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>ページハッシュが一致しません</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>セッションページのハッシュが一致しません</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>構成ディレクトリの変更の読み込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>反転関数テーブルの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>セッション構成の変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>拡張プロセッサコントロールレジスタ</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>種類1のプールの破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x28</p></td>
<td align="left"><p>タイプ2のプールの破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x29</p></td>
<td align="left"><p>種類3プールの破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>一般的なプールの破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>Win32k の変更</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常、このバグチェックには3つの異なる原因があります。

1.  ドライバーにより、重要なカーネルコードまたはデータが誤って、または故意に変更されました。 Microsoft Windows Server 2003 Service Pack 1 (SP1) 以降のバージョンの x64 ベースのコンピューターでは、Microsoft が開始した修正プログラムを除き、カーネルにパッチを適用することはできません。

2.  開発者が、システムの起動時にアタッチされていないカーネルデバッガーを使用して、通常のカーネルブレークポイントを設定しようとしました。 通常のブレークポイント ([**bp**](bp--bu--bm--set-breakpoint-.md)) は、デバッガーが開始時にアタッチされている場合にのみ設定できます。 プロセッサブレークポイント ([**ba**](ba--break-on-access-.md)) は、いつでも設定できます。

3.  ハードウェアの破損が発生しました。 たとえば、カーネルコードまたはデータが、失敗したメモリに格納されている可能性があります。

<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

開始するには、 [**k、kb、kc、kd、kp、kp、kv (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用して、スタックトレースを確認します。 プロセッサ番号を指定して、すべてのプロセッサのスタックを調べることができます。

また、コード内でこの停止コードまでのブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。

詳細については、以下のトピックを参照してください。

[Windows デバッガー (WinDbg) を使用したクラッシュ ダンプ分析](crash-dump-files.md)

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用できます。

-   このバグチェックの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   Windows メモリ診断ツールを実行して、メモリをテストします。 コントロールパネルの検索ボックスに「Memory」と入力し、[**コンピューターのメモリの問題を診断する**] をクリックします。テストの実行後、イベントビューアーを使用して、システムログの下に結果を表示します。 結果を表示するには、 *Memorydiagnostics-results*エントリを探します。

-   システムの製造元から提供されているハードウェア診断を実行できます。

-   インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

-   一般的なトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。

 

 





---
title: バグ チェック 0x109 CRITICAL_STRUCTURE_CORRUPTION
description: CRITICAL_STRUCTURE_CORRUPTION のバグ チェックでは、0x00000109 の値を持ちます。 これは、カーネルの重大なカーネル コードまたはデータの破損が検出されたことを示します。
ms.assetid: 38d4d722-a915-4f17-899b-2a0b4aa69d95
keywords:
- バグ チェック 0x109 CRITICAL_STRUCTURE_CORRUPTION
- CRITICAL_STRUCTURE_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CRITICAL_STRUCTURE_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba60f66549979d0865e0648536352f4e2e907350
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582476"
---
# <a name="bug-check-0x109-criticalstructurecorruption"></a>バグ チェック 0x109:重要な\_構造\_破損


CRITICAL\_構造\_破損バグ チェックが 0x00000109 の値を持ちます。 これは、カーネルの重大なカーネル コードまたはデータの破損が検出されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="criticalstructurecorruption-parameters"></a>重要な\_構造\_破損パラメーター


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
<td align="left"><p>破損した領域の種類。 (参照次の表に、後でこのページ)。</p></td>
</tr>
</tbody>
</table>

 

パラメーター 4 の値では、破損した領域の種類を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 4</th>
<th align="left">破損した領域、種類の破損、またはを実行するアクションの種類の型には、破損が原因となった</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>汎用的なデータのリージョン</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>関数の変更または Itanium ベースの関数の場所</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>プロセッサの割り込みディスパッチ テーブル (IDT)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>プロセッサのグローバル記述子テーブル (GDT)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>タイプ 1 プロセスの一覧の破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>種類 2 のプロセスの一覧の破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>デバッグ ルーチンの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>重要な MSR 変更</p></td>
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
<td align="left"><p>0 xa</p></td>
<td align="left"><p>システム サービスの機能の変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>汎用的なセッションのデータ領域</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xc</p></td>
<td align="left"><p>セッションの関数または .pdata の変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xd</p></td>
<td align="left"><p>インポートのテーブルの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xE</p></td>
<td align="left"><p>セッションのインポート テーブルの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xf です.</p></td>
<td align="left"><p>Ps Win32 コールアウトの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>スイッチの日常的な変更をデバッグします。</p></td>
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
<td align="left"><p>IRP の完了ディスパッチャーの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x14</p></td>
<td align="left"><p>IRP デアロケーターの変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15</p></td>
<td align="left"><p>プロセッサ レジスタを制御します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x16</p></td>
<td align="left"><p>重要なポイント制御レジスタの変更を浮動小数点</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x17</p></td>
<td align="left"><p>ローカルで APIC の変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>カーネル通知 callout の変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>読み込まれたモジュール一覧の変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>タイプの 3 つのプロセスの一覧の破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>タイプ 4 のプロセス一覧の破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>ドライバー オブジェクトの破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>Executive コールバック オブジェクトの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>モジュールの余白の変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>保護されたプロセスの変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>汎用的なデータのリージョン</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>ページのハッシュが一致しません</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>セッション ページ ハッシュが一致しません</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>ディレクトリ変更の構成を読み込む</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>テーブルの逆関数を変更</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>セッション構成の変更</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>コントロールを拡張プロセッサを登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>タイプの 1 つのプールの破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x28</p></td>
<td align="left"><p>種類 2 のプールの破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x29</p></td>
<td align="left"><p>タイプの 3 つのプールの破損</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>一般的なプールの破損</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>Win32k.sys の変更</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

一般には、このバグ チェックの 3 つのさまざまな原因があります。

1.  ドライバーに誤って、または意図的に、クリティカルなカーネル コードまたはデータを変更します。 Microsoft Windows Server 2003 Service Pack 1 (SP1) および x64 ベースのコンピューターに Windows の以降のバージョンでは、承認された Microsoft 主導のホット パッチ適用以外に、カーネルは許可されません。 詳細については、[x64 ベース システム用の修正プログラムの適用ポリシー](https://go.microsoft.com/fwlink/p/?linkid=50719)を参照してください。

2.  開発者は、システムが起動されたときにアタッチされませんでしたをカーネル デバッガーを使用して通常のカーネル ブレークポイントを設定しようとしました。 通常のブレークポイント ([**bp**](bp--bu--bm--set-breakpoint-.md)) 開始時に、デバッガーがアタッチされている場合にのみ設定できます。 プロセッサのブレークポイント ([**ba**](ba--break-on-access-.md)) いつでもでも設定できます。

3.  ハードウェアの破損が発生しました。 などのカーネル コードまたはデータが格納されている失敗したメモリ内。

<a name="resolution"></a>解決方法
----------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

開始するには、スタック トレースを使用してを調べる、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。 すべてのプロセッサでスタックを確認するプロセッサ数を指定できます。

また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   メモリをテストする、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして **、コンピューターのメモリの問題を診断**します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

-   システム製造元から提供されたハードウェア診断を実行して確認することができます。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

 

 





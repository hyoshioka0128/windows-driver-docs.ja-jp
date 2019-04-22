---
title: バグ チェック 0x12 TRAP_CAUSE_UNKNOWN
description: TRAP_CAUSE_UNKNOWN のバグ チェックでは、0x00000012 の値を持ちます。 これは、不明な例外が発生したことを示します。
ms.assetid: 43cbcc34-9df0-4d5f-b823-1cc3cafaa811
keywords:
- バグ チェック 0x12 TRAP_CAUSE_UNKNOWN
- TRAP_CAUSE_UNKNOWN
ms.date: 06/26/2018
topic_type:
- apiref
api_name:
- TRAP_CAUSE_UNKNOWN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2262c46d340fc92e602618d00844eb03b43e01d4
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239211"
---
# <a name="bug-check-0x12-trapcauseunknown"></a>バグ チェック 0x12:トラップ\_原因\_不明


トラップ\_原因\_不明なバグ チェックが 0x00000012 の値を持ちます。 これは、不明な例外が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="trapcauseunknown-parameters"></a>トラップ\_原因\_不明なパラメーター


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
<td align="left"><p>TRAP_CAUSE_UNKNOWN の種類</p>
<p><B>VALUES</B></p>
<p>1-予期しない中断します。 (パラメーター 2 – 割り込みベクター)</p>
<p>2-不明な浮動小数点例外。 </p>
<p>3 - (プロセッサの定義を参照してください) が有効なとアサートされたステータス ビットです。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>Arg1 に依存</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>解決方法
----------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

開始するには、スタック トレースを使用してを調べる、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。 すべてのプロセッサでスタックを確認するプロセッサ数を指定できます。 

また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

[! Idt](-idt.md)指定割り込みディスパッチ テーブル (IDT) の割り込みサービス ルーチン (Isr) を表示する拡張機能を使用できます。 

説明する手法のいくつか[デバッグ中断の Storm](debugging-an-interrupt-storm.md)予期しない割り込みで使用できます。

クラッシュ ダンプの使用方法の概要については、次を参照してください。 [Windows デバッガー (WinDbg) を使用してクラッシュ ダンプ分析](crash-dump-files.md)します。

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

 

 

 





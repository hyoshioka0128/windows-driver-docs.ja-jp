---
title: Bug Check 0x9C MACHINE_CHECK_EXCEPTION
description: MACHINE_CHECK_EXCEPTION のバグ チェックでは、0x0000009c の解説の値を持ちます。 このバグ チェックでは、致命的なマシン チェック例外が発生したことを示します。
ms.assetid: b8945dba-c515-4a30-a36c-ef4feaadabbe
keywords:
- Bug Check 0x9C MACHINE_CHECK_EXCEPTION
- MACHINE_CHECK_EXCEPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MACHINE_CHECK_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5c6f5b6e770c497d7339634163718f2968271fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361700"
---
# <a name="bug-check-0x9c-machinecheckexception"></a>バグ チェック 0x9C:マシン\_確認\_例外


マシン\_確認\_例外のバグ チェックが 0x0000009c の解説の値を持ちます。 このバグ チェックでは、致命的なマシン チェック例外が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="machinecheckexception-parameters"></a>マシン\_確認\_例外パラメーター


メッセージに記載されている 4 つのパラメーターでは、プロセッサの種類に応じて、異なる意味を持ちます。

場合は、プロセッサは、以前の x86 ベースのアーキテクチャに基づいており、マシン チェック例外 (MCE) 機能は、マシン チェック アーキテクチャ (MCA) 機能 (Intel Pentium プロセッサなど) ではありませんが、パラメーターは、次の意味を持ちます。

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
<td align="left"><p>P5_MC_TYPE マシン サービス レポート (MSR) の下位 32 ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>MCA_EXCEPTION 構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>P5_MC_ADDR MSR の上位 32 ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>P5_MC_ADDR MSR の下位 32 ビット</p></td>
</tr>
</tbody>
</table>

 

パラメーターがある場合は、プロセッサは、x86 ベースの新しいアーキテクチャに基づいており、MCA 機能があり、MCE 機能 (たとえば、すべて Intel プロセッサ ファミリの 6 か月または Pentium Pro、Pentium IV、Xeon などの上位の)、またはプロセッサが x64 ベースのプロセッサの場合は、次の意味です。

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
<td align="left"><p>銀行番号</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>MCA_EXCEPTION 構造体のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>エラーが発生した MCA 銀行の MCi_STATUS MSR の上位 32 ビット</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>エラーが発生した MCA 銀行の MCi_STATUS MSR の下位 32 ビット</p></td>
</tr>
</tbody>
</table>

 

Itanium ベースのプロセッサでは、パラメーターは、次の意味を持ちます。

**注**  パラメーター 1 が違反の種類を示します。

 

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
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>エラー コード</p></td>
<td align="left"><p>システムの抽象化レイヤー (SAL) は、SAL_GET_STATEINFO の MCA の処理中にエラーを返しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>エラー コード</p></td>
<td align="left"><p>SAL を MCA 処理中に、SAL_CLEAR_STATEINFO のエラーが返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ファームウェア (FW) は、致命的な MCA を報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>2 つの原因が考えられます。</p>
<ul>
<li><p>SAL に回復可能な MCA が報告されますが、この回復はサポートされていません。</p></li>
<li><p>SAL は、MCA を生成しますが、エラー レコードを作成できませんでした。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xc</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>エラー コード</p></td>
<td align="left"><p>SAL は、SAL_GET_STATEINFO の INIT イベントの処理中にエラーを返しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xd</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>エラー コード</p></td>
<td align="left"><p>SAL では、INIT イベントを処理中に、SAL_CLEAR_STATEINFO のエラーが返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xE</p></td>
<td align="left"><p>ログのアドレス</p></td>
<td align="left"><p>ログのサイズ</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows Vista およびそれ以降のオペレーティング システムでは、このバグ チェックは、次の状況でのみ発生します。

-   WHEA が完全に初期化されていません。
-   すべてのプロセッサが rendezvous のレジスタにはエラーあるありません。

その他の状況では、このバグ チェックに置き換えられました[**チェック 0x124 のバグします。WHEA\_修正不可能な\_エラー** ](bug-check-0x124---whea-uncorrectable-error.md) Windows Vista 以降のオペレーティング システムでします。

マシン チェック アーキテクチャ (MCA) に関する詳細については、Intel または AMD の Web サイトを参照してください。

 

 





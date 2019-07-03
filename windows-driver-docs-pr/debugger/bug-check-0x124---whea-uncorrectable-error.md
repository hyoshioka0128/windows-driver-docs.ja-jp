---
title: Bug Check 0x124 WHEA_UNCORRECTABLE_ERROR
description: WHEA_UNCORRECTABLE_ERROR のバグ チェックでは、0x00000124 の値を持ちます。 このバグ チェックでは、ハードウェアの致命的なエラーが発生したことを示します。
ms.assetid: b3b7c6dd-3891-4ccb-96d1-49e8a2de34c8
keywords:
- Bug Check 0x124 WHEA_UNCORRECTABLE_ERROR
- WHEA_UNCORRECTABLE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WHEA_UNCORRECTABLE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75f7b16c3d1f8e98e20c79b8b9d11753bd7eb98e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520782"
---
# <a name="bug-check-0x124-wheauncorrectableerror"></a>バグ チェック 0x124:WHEA\_修正不可能な\_エラー


WHEA\_修正不可能な\_エラーのバグ チェックが 0x00000124 の値を持ちます。 このバグ チェックでは、ハードウェアの致命的なエラーが発生したことを示します。 このバグ チェックでは、Windows ハードウェア エラー アーキテクチャ (WHEA) によって提供されるエラー データを使用します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="wheauncorrectableerror-parameters"></a>WHEA\_修正不可能な\_エラー パラメーター


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
<td align="left"><p>0x0</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>エラーが発生した MCA 銀行の MCi_STATUS MSR の上位 32 ビット。</p></td>
<td align="left"><p>エラーが発生した MCA 銀行の MCi_STATUS MSR の下位 32 ビットです。</p></td>
<td align="left"><p>マシン チェック例外が発生しました。</p>
<p>これらのパラメーターの説明が、x64、プロセッサが基づいている場合に適用アーキテクチャ、または x86 MCA 機能が利用可能な (たとえば、Intel Pentium Pro、Pentium IV の場合、または Xeon) アーキテクチャ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正済みのマシン チェック例外が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正済みのプラットフォームのエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>マスク不可能割り込み (NMI) エラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>PCI Express 修正不可能なエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>汎用ハードウェア エラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>初期化エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>起動エラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>拡張性の高い一貫したインターフェイス (SCI) の一般的なエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>長さをバイト単位で SAL ログ。</p></td>
<td align="left"><p>SAL のログのアドレス。</p></td>
<td align="left"><p>修正不可能な Itanium ベースのマシン チェック中止エラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正済みの Itanium ベースのマシン チェック エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正された Itanium プラットフォームのエラーが発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックは通常、物理ハードウェア障害に関連します。 関連ヒート、欠陥のあるハードウェア、メモリまたは開始して失敗するかが失敗するプロセッサでもを指定できます。 過剰なクロックが有効になって場合、は、無効にすることをお試しください。 ファンなどの任意の冷却システムが機能していることを確認します。 システム メモリに欠陥がないことを確認するシステム診断を実行します。 ドライバーのこのバグ チェックで失敗するハードウェアが原因であることが勧め可能性は低く、します。

その他の一般的なバグ チェックがトラブルシューティング情報について、次を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

<a name="remarks"></a>注釈
-------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

パラメーター 1 では、エラーが報告されたエラーのソースの種類を識別します。 2 番目のパラメーターは、WHEA のアドレスを保持\_エラー\_レコード構造のエラー条件について説明します。

ハードウェア エラーが発生したときに、WHEA はハードウェアのエラー状態に関連付けられているエラー情報を格納するエラー レコードを作成します。 各 error レコードには、WHEA によって記述\_エラー\_レコードの構造体。 Windows カーネルには、システム イベント ログにエラー レコードが保存されるように、エラー応答を生成した Event Tracing for Windows (ETW) のハードウェア エラー イベントのエラー レコードが含まれています。 WHEA で使用されるエラー レコードの形式は、Unified Extensible Firmware Interface (UEFI) 仕様のバージョン 2.2 の付録 N」の説明に従って、共通のプラットフォーム エラー レコードに基づいています。 詳細については、次を参照してください。 [WHEA\_エラー\_レコード](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_record)と[Windows ハードウェア エラー アーキテクチャ (WHEA)](https://docs.microsoft.com/windows-hardware/drivers/whea)します。

使用することができます[ **! errrec** ](-errrec.md) &lt;addr&gt; WHEA を表示する\_エラー\_パラメーター 2 で提供されるアドレスを使用してレコードの構造体。 [ **! Whea** ](-whea.md)と[ **! errpkt** ](-errpkt.md) WHEA 情報を表示する拡張機能を使用できます。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用して、! 拡張機能を分析](using-the--analyze-extension.md)と[! 分析](-analyze.md)

このバグ チェックでは、Windows Vista より前の Windows バージョンでサポートされていません。 マシン チェック例外を報告する代わりに、 [**バグ チェック 0x9C**](bug-check-0x9c--machine-check-exception.md)します。

 

 





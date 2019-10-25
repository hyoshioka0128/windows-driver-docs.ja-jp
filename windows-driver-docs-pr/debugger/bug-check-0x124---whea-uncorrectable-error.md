---
title: バグチェック 0x124 WHEA_UNCORRECTABLE_ERROR
description: WHEA_UNCORRECTABLE_ERROR のバグチェックの値は0x00000124 です。 このバグチェックは、致命的なハードウェアエラーが発生したことを示します。
ms.assetid: b3b7c6dd-3891-4ccb-96d1-49e8a2de34c8
keywords:
- バグチェック 0x124 WHEA_UNCORRECTABLE_ERROR
- WHEA_UNCORRECTABLE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WHEA_UNCORRECTABLE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d891e4291d171d477976d281a38e7f5001d3516c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837833"
---
# <a name="bug-check-0x124-whea_uncorrectable_error"></a>バグチェック 0x124: WHEA\_修正不可能\_エラー


WHEA\_修正不可能な\_エラーのバグチェックの値は0x00000124 です。 このバグチェックは、致命的なハードウェアエラーが発生したことを示します。 このバグチェックでは、Windows ハードウェアエラーアーキテクチャ (WHEA) によって提供されるエラーデータを使用します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="whea_uncorrectable_error-parameters"></a>WHEA\_修正不可能\_エラーパラメーター


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
<td align="left"><p>0x0</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>エラーが発生した MCA bank の MCi_STATUS MSR の上位32ビット。</p></td>
<td align="left"><p>エラーが発生した MCA bank の MCi_STATUS MSR の低32ビット。</p></td>
<td align="left"><p>コンピューターチェックの例外が発生しました。</p>
<p>これらのパラメーターの説明は、プロセッサが x64 アーキテクチャに基づいている場合、または MCA 機能を利用できる x86 アーキテクチャ (Intel Pentium Pro、Pentium IV、Xeon など) の場合に適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正されたコンピューターチェックの例外が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正されたプラットフォームエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>Nonmaskable Interrupt (NMI) エラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正できない PCI Express エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>一般的なハードウェアエラーが発生しました。</p></td>
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
<td align="left"><p>ブートエラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>スケーラブルな一貫性のあるインターフェイス (SCI) の一般的なエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>SAL ログの長さ (バイト単位)。</p></td>
<td align="left"><p>SAL ログのアドレス。</p></td>
<td align="left"><p>修正できない Itanium ベースのマシンチェック中止エラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正された Itanium ベースのコンピューター確認エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>WHEA_ERROR_RECORD 構造体のアドレス。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>予約済み。</p></td>
<td align="left"><p>修正された Itanium プラットフォームエラーが発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグチェックは、通常、物理的なハードウェア障害に関連しています。 これには、ヒート関連、欠陥のあるハードウェア、メモリ、または障害または障害が発生し始めたプロセッサもあります。 オーバークロックが有効になっている場合は、無効にしてみてください。 ファンなどの冷却システムが機能していることを確認します。 システム診断を実行して、システムメモリに欠陥がないことを確認します。 このバグチェックでは、ドライバーによってハードウェアの障害が発生する可能性は低くなります。

その他の一般的なバグチェックのトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

パラメーター1は、エラーを報告したエラーソースの種類を識別します。 パラメーター2には、エラー状態を説明する WHEA\_ERROR\_レコード構造体のアドレスが保持されます。

ハードウェアエラーが発生すると、WHEA は、ハードウェアエラー状態に関連付けられたエラー情報を格納するエラーレコードを作成します。 各エラーレコードは、WHEA\_エラー\_レコードの構造によって記述されます。 Windows カーネルには、エラーレコードがシステムイベントログに保存されるようにエラーに応答して発生する、Windows イベントトレーシング (ETW) ハードウェアエラーイベントを含むエラーレコードが含まれています。 WHEA によって使用されるエラーレコードの形式は、「Unified Extensible Firmware Interface (UEFI) 仕様のバージョン2.2 の付録 N」で説明されている一般的なプラットフォームエラーレコードに基づいています。 詳細については、「 [WHEA\_エラー\_レコード](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_record)と[Windows ハードウェアエラーアーキテクチャ (WHEA)](https://docs.microsoft.com/windows-hardware/drivers/whea)」を参照してください。

[ **! Errrec**](-errrec.md) &lt;addr&gt; を使用すると、パラメーター2に指定されたアドレスを使用して、WHEA\_エラー\_レコード構造を表示できます。 [ **! Whea**](-whea.md)および[ **! errpkt**](-errpkt.md)拡張機能を使用して、追加の whea 情報を表示できます。

詳細については、以下のトピックを参照してください。

[Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)

[WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[! Analyze 拡張機能](using-the--analyze-extension.md)と[! Analyze](-analyze.md)を使用する

Windows Vista より前のバージョンでは、このバグチェックはサポートされていません。 代わりに、コンピューターチェックの例外は、[**バグチェック 0x9C**](bug-check-0x9c--machine-check-exception.md)によって報告されます。

 

 





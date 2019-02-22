---
title: バグ チェック 0x79 MISMATCHED_HAL
description: MISMATCHED_HAL のバグ チェックでは、HAL のリビジョン レベルまたは構成が一致しないこと、カーネルまたはコンピューターのことを示します 0x00000079 の値を持ちます。
ms.assetid: 2d063c2a-c647-4436-b005-04f71a4d2b66
keywords:
- バグ チェック 0x79 MISMATCHED_HAL
- MISMATCHED_HAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MISMATCHED_HAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ce15f43fcb4cfaa25b5c2542232f3e7983d8a1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528628"
---
# <a name="bug-check-0x79-mismatchedhal"></a>バグ チェック 0x79 の。一致しない\_HAL


不一致\_HAL のバグ チェックが 0x00000079 の値を持ちます。 このバグ チェックでは、ハードウェア アブストラクション レイヤー (HAL) のリビジョン レベルまたは構成が一致しないこと、カーネルまたはコンピューターのことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="mismatchedhal-parameters"></a>一致しない\_HAL パラメーター


パラメーター 1 では、不一致の型を示します。

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
<th align="left">発生します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Ntoskrnl.exe の主要なプロセッサの制御ブロック (PRCB) レベル。</p></td>
<td align="left"><p>Hal.dll の主要な PRCB レベルです。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>PRCB リリース レベルが一致しません。 (何かが古くなっている。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>Ntoskrnl.exe のビルドの種類。</p></td>
<td align="left"><p>Hal.dll のビルドの種類。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ビルドの種類が一致しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>ローダーのパラメーターの拡張機能のサイズ。</p></td>
<td align="left"><p>ローダーのパラメーターの拡張機能のメジャー バージョン。</p></td>
<td align="left"><p>ローダーのパラメーターの拡張機能のマイナー バージョン。</p></td>
<td align="left"><p>ローダー (ntldr) と HAL のバージョンが一致しません。</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 では、0x2 が等しくなると、次のビルドの種類のコードが使用されます。

-   0:マルチプロセッサが有効な無料のビルド

-   1:マルチプロセッサ対応のチェック ビルド

-   2:シングル プロセッサの無料のビルド

-   3:シングル プロセッサ チェック ビルド

<a name="cause"></a>原因
-----

不一致\_Ntoskrnl.exe または Hal.dll ユーザーを手動で更新するときに多くの場合、HAL のバグ チェックが発生します。

エラーは、これら 2 つのファイルのいずれかが最新でないことも指定できます。 コンピューターがマルチプロセッサ HAL およびインストールするには、シングル プロセッサのカーネルが誤って可能性がありますまたはその逆です。

カーネルの Ntoskrnl.exe のファイルはシングル プロセッサ システムあり Ntkrnlmp.exe はマルチプロセッサ システム。 ただし、これらのファイル名は、インストール メディア上のファイルに対応します。Windows オペレーティング システムをインストールした後、ファイルが使用されるソース ファイルに関係なく Ntoskrnl.exe が変更されます。 HAL ファイルも Hal.dll 名前、インストール後は、インストール メディアにいくつかの可能な HAL ファイルがあります。 詳細については、「インストール チェック ビルド」Windows Driver Kit (WDK) で参照してください。

<a name="resolution"></a>解決方法
----------

製品 CD または Windows セットアップ ディスクを使用して、コンピューターを再起動します。 [ようこそ] 画面で、f10 キーを押して回復コンソールを起動します。 使用して、**コピー**オリジナルの CD から、ハード_ディスク上の適切なフォルダーに正しい HAL またはカーネルのファイルをコピーするコマンド。 **コピー**コマンドをコピーするファイルが Microsoft の圧縮ファイル形式かどうかを検出します。 そうである場合、ターゲット ドライブにコピーされるファイルが自動的に展開します。

 

 





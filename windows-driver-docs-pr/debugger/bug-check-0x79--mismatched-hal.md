---
title: 0x79 MISMATCHED_HAL のバグチェック
description: MISMATCHED_HAL のバグチェックには、HAL のリビジョンレベルまたは構成がカーネルまたはコンピューターのリビジョンと一致しないことを示す値0x00000079 があります。
ms.assetid: 2d063c2a-c647-4436-b005-04f71a4d2b66
keywords:
- 0x79 MISMATCHED_HAL のバグチェック
- MISMATCHED_HAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MISMATCHED_HAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 367a52541abb076111bf92461b94cff7fd7cfabf
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209312"
---
# <a name="bug-check-0x79-mismatched_hal"></a>バグの確認 0x79:\_HAL が一致しません


一致しない\_HAL のバグチェックには、0x00000079 の値が含まれています。 このバグチェックは、ハードウェアアブストラクションレイヤー (HAL) のリビジョンレベルまたは構成が、カーネルまたはコンピューターのリビジョンレベルまたは構成と一致しないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="mismatched_hal-parameters"></a>\_HAL パラメーターが一致しません


パラメーター1は、不一致の種類を示します。

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
<th align="left">こと.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Ntoskrnl.exe の主要プロセッサ制御ブロック (PRCB) レベル。</p></td>
<td align="left"><p>Hal.dll の主要な PRCB レベル。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>PRCB リリースレベルが一致しません。 (古いものがあります)。</p></td>
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
<td align="left"><p>ローダーパラメーター拡張のサイズ。</p></td>
<td align="left"><p>ローダーパラメーター拡張のメジャーバージョン。</p></td>
<td align="left"><p>ローダーパラメーター拡張のマイナーバージョン。</p></td>
<td align="left"><p>ローダー (ntldr) と HAL のバージョンが一致しません。</p></td>
</tr>
</tbody>
</table>

 

パラメーター1が0x2 の場合、次のビルドの種類のコードが使用されます。

-   0: マルチプロセッサ対応の無料ビルド

-   1: マルチプロセッサ対応のチェックされたビルド

-   2: シングルプロセッサの無料ビルド

-   3: シングルプロセッサのチェックされたビルド

<a name="cause"></a>原因
-----

ユーザーが Ntoskrnl.exe または Hal.dll を手動で更新すると、一致しない\_HAL のバグチェックが頻繁に発生します。

このエラーは、これら2つのファイルのいずれかが古くなっていることを示している場合もあります。 または、コンピューターにマルチプロセッサ HAL とシングルプロセッサカーネルがインストールされている場合や、その逆の場合もあります。

Ntoskrnl.exe カーネルファイルはシングルプロセッサシステム用で、Ntkrnlmp はマルチプロセッサシステム用です。 ただし、これらのファイル名は、インストールメディアのファイルに対応しています。Windows オペレーティングシステムをインストールすると、使用されているソースファイルに関係なく、ファイルの名前が Ntoskrnl.exe に変更されます。 HAL ファイルはインストール後に Hal.dll という名前を使用しますが、以前のバージョンの Windows のインストールメディアには、いくつかの HAL ファイルがあります。

<a name="resolution"></a>解像度
----------

製品 CD または Windows セットアップディスクを使用して、コンピューターを再起動します。 ようこそ画面で、F10 キーを押して回復コンソールを起動します。 **コピー**コマンドを使用して、正しい HAL またはカーネルファイルを元の CD からハードディスク上の適切なフォルダーにコピーします。 **コピー**コマンドは、コピーするファイルが Microsoft の圧縮ファイル形式であるかどうかを検出します。 その場合は、ターゲットドライブにコピーされたファイルを自動的に展開します。

 

 





---
title: バグチェック 0x1 APC_INDEX_MISMATCH
description: 0x00000001.
ms.assetid: 01e64516-809c-49ce-9aaa-b4e439ac575b
keywords:
- バグチェック 0x1 APC_INDEX_MISMATCH
- APC_INDEX_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- APC_INDEX_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c9fe93aa10b095035653271c6954fc0b2238f6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837641"
---
# <a name="bug-check-0x1-apc_index_mismatch"></a>バグチェック 0x1: APC\_インデックス\_不一致

APC\_のインデックス\_不一致のバグチェックには、0x00000001 の値が指定されています。 これは、非同期プロシージャ呼び出し (APC) の状態インデックスが一致していないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)」を参照してください。


## <a name="apc_index_mismatch-parameters"></a>APC\_インデックス\_パラメーターが一致しません

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
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
<td align="left"><p>システム関数 (システム呼び出し) またはワーカールーチンのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left">現在のスレッドの<strong>Apcstateindex</strong>フィールドの値。</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>現在のスレッドの連結<strong>Edapcdisable</strong>フィールドの値。 このフィールドは、次の2つの異なる16ビットフィールドで構成されています: (<em>スレッド</em>&gt;特別<strong>apcdisable</strong> &lt;&lt; 16) |<em>スレッド</em>&gt;<strong>KernelApcDisable</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>呼び出しの種類:</p><ul><li>0-システム呼び出し</li><li>1-ワーカールーチン</li></ul></p></td>
</tr>
</tbody>
</table>

 
<a name="cause"></a>原因
-----

このバグチェックの最も一般的な原因は、ファイルシステムまたはドライバーに、Apc を無効にして再度有効にするための呼び出しのシーケンスが一致しない場合です。 キーデータ項目は、*スレッド*&gt; 連結**Edapcdisable**フィールドです。 連結**Edapcdisable**フィールドは、2つの異なる16ビットフィールドで構成されています: KernelApcDisable **apcdisable**と。 どちらかのフィールドの負の値は、ドライバーによって特殊な Apc または通常の Apc が無効にされたことを示します (それぞれの場合)。 正の値は、ドライバーが特殊な Apc または通常の Apc を何度も有効にしたことを示します。


<a name="resolution"></a>解像度
----------

### <a name="debugging-with-windbg"></a>WinDbg を使用したデバッグ

[ **! Analyze**](-analyze.md)デバッガー拡張機能は、バグチェックに関する情報を表示し、根本原因を特定するのに役立ちます。

[ **! Apc**](-apc.md)拡張機能を使用して、1つまたは複数の非同期プロシージャ呼び出し (apc) の内容を表示できます。

また、この stop コードの前にあるコードにブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。

WinDbg の使用方法の詳細については、「 [Windows デバッガー (windbg) を使用したクラッシュダンプ分析](crash-dump-files.md)」を参照してください。


### <a name="debugging-without-windbg"></a>WinDbg を使用しないデバッグ

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用できます。

-   このバグチェックの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

一般的なトラブルシューティング情報については、「 [Blue screen data](blue-screen-data.md)」を参照してください。


<a name="remarks"></a>注釈
-------

このバグチェックは、カーネルで内部エラーが発生した結果です。 このエラーは、システムコールの終了時に発生します。 このバグチェックの考えられる原因は、保護された領域または重大な領域を入力または残すためのシステムコールの順序が一致しないファイルシステムまたはドライバーです。 たとえば、 [**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)を呼び出すたびに、 [**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)への呼び出しが一致している必要があります。 

ドライバーを開発している場合は、ドライバーを出荷する前にコードの問題を検出するために、Windows Driver Kit に用意されている静的分析ツールである[静的ドライバー検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)ツールを使用できます。 [CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)規則を使用して静的ドライバー検証ツールを実行し、ソースコードがこれらのシステム呼び出しを正しい順序で使用していることを確認します。


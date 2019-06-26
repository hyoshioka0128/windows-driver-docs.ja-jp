---
title: バグ チェック 0x1 APC_INDEX_MISMATCH
description: 0x00000001 します。
ms.assetid: 01e64516-809c-49ce-9aaa-b4e439ac575b
keywords:
- バグ チェック 0x1 APC_INDEX_MISMATCH
- APC_INDEX_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- APC_INDEX_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9396d9c9857af0d86a7925104127dcaf3826d609
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362390"
---
# <a name="bug-check-0x1-apcindexmismatch"></a>バグ チェック 0x1:APC\_インデックス\_が一致しません


APC\_インデックス\_の不一致のバグ チェックが 0x00000001 の値を持ちます。 APC (非同期プロシージャ コール) の状態のインデックスで不一致が生じていますが、これを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="apcindexmismatch-parameters"></a>APC\_インデックス\_不一致パラメーター


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
<td align="left"><p>システム関数 (システムの呼び出し) またはワーカーのルーチンのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left">現在のスレッドの値<strong>ApcStateIndex</strong>フィールド。</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>現在のスレッドの CombinedApcDisable フィールドの値。 このフィールドは、2 つの独立した 16 ビット フィールドで構成されます。(<em>スレッド</em>-&gt;<strong>SpecialApcDisable</strong> &lt; &lt; 16) |<em>スレッド</em>-&gt;<strong>KernelApcDisable</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>呼び出し (0 - システムの呼び出し、1 - worker ルーチン) の型。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cause"></a>原因
-----

このバグ チェックの最も一般的な原因は、ファイル システムまたはドライバーが一致しない一連の呼び出しを無効にし、Apc を再度有効にします。 キーのデータ項目は、*スレッド*-&gt;**CombinedApcDisable**フィールド。 **CombinedApcDisable**別々 の 2 つの 16 ビット フィールドのフィールドで構成されます。**SpecialApcDisable**と**KernelApcDisable**します。 負の値のいずれかのフィールドでは、ドライバーが無効になっている特別なまたは通常の Apc (それぞれ) せずに再度有効にすることを示します。 正の値は、ドライバーが有効になっているか、特殊な通常の Apc 回数が多すぎますを示します。

## <a name="resolution"></a>解決方法
----------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

使用することができます、 [ **! apc** ](-apc.md)の拡張機能は、1 つの内容を表示します。 または、複数の非同期プロシージャ呼び出し (Apc)。

また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

## <a name="remarks"></a>注釈
-------

これは、カーネルの内部エラーです。 このエラーは、システムの呼び出しからの終了時に発生します。 このバグ チェックの考えられる原因は、ファイル システムまたはドライバーが一致しない、一連のシステム呼び出しを入力するか、保護された、または重要な領域のままにします。 に対する各呼び出しなど[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)に一致する呼び出しがあります。 [ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)します。 ドライバーを開発している場合を使用できます[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)、静的分析ツールが、ドライバーを出荷する前に、コード内の問題を検出するために、Windows ドライバー キットで使用できます。 Static Driver Verifier の実行、 [CriticalRegions](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-criticalregions)ソース コードがこれらのシステムを使用することを確認するルールを正しい順序で呼び出します。

 

 





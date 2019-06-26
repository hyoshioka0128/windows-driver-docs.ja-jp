---
title: C28110
description: 警告 C28110 ドライバーでは、浮動小数点演算ハードウェアの状態を保護する必要があります。 参照してください float を使用します。
ms.assetid: 2f6045e3-92b2-4773-a8de-3d0ec09c5d31
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28110
ms.openlocfilehash: 6a2593b288ad5cb1688c3db0b974ee778a858a24
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364154"
---
# <a name="c28110"></a>C28110


C28110 を警告します。ドライバーは、浮動小数点演算ハードウェアの状態を保護する必要があります。 参照してください float 型の使用

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>使用<strong>KeSaveFloatingPointState</strong>と<strong>KeRestoreFloatingPointState</strong>浮動小数点演算にします。 ディスプレイ ドライバーが、対応するを使用する必要があります<strong>エンジニア リング ・.</strong>ルーチン。</p></td>
</tr>
</tbody>
</table>

 

この警告では、カーネル モードで該当するのみです。 コードが保護されていないときに、変数または float 型の定数を使用しようとして、ドライバー [ **KeSaveFloatingPointState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate)と[ **KeRestoreFloatingPointState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate)、または[ **EngSaveFloatingPointState** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)と[ **EngRestoreFloatingPointState** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate).

通常、ドライバーが最新のアプリケーションとどのように使用して保護されていない浮動小数点の浮動小数点のコンテキストで実行[ **KeSaveFloatingPointState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesavefloatingpointstate)と[ **KeRestoreFloatingPointState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kerestorefloatingpointstate)他のプロセスの結果を変更することができ、ドライバーで正しくないか、予期しない結果が多くの場合、発生することができます。

ディスプレイ ドライバーを使用する必要があります[ **EngSaveFloatingPointState** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)と[ **EngRestoreFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)します。

任意の特定のフロー パスに沿ったこのエラーのインスタンスが検出されると、コード分析ツールは、後続のようなエラーを抑制します。 コード分析ツールでは、呼び出し元が使用を報告するための浮動小数点型の引数を受け取るまたは返す浮動小数点型、関数定義には、このエラーは報告されません。

この警告は、呼び出された関数の浮動小数点演算を実行すると、プログラムの保存し関数の呼び出しでは、浮動小数点状態を復元エラーでトリガーできます。

使用して、関数の注釈を設定する必要があります関数が意図的に、浮動小数点演算を使用する浮動小数点が安全なコンテキストで呼び出されることが予想する場合 **\_カーネル\_float\_使用\_** . この注釈し、関数本体で警告を非表示の両方により、呼び出し元のコンテキストを浮動小数点演算の呼び出しが安全に保護されていることを確認します。 浮動小数点演算では、引数を表示または戻り値、効果が使用する場合と同じ **\_カーネル\_float\_使用\_** します。

使用して **\_カーネル\_float\_使用\_** 上 (または、適切な保存し、復元への呼び出しの追加) 浮動小数点を使用するすべての関数のポイントまでの警告が残っていない、ドライバーを指定できます浮動小数点演算ハードウェアの不正使用の無料ことを保証します。 詳細については、次を参照してください。[ドライバーのフローティング ポイント注釈](floating-point-annotations-for-drivers.md)します。

 

 






---
title: C28110
description: 警告 C28110 ドライバーは、浮動小数点のハードウェアの状態を保護する必要があります。 「Float の使用」を参照してください。
ms.assetid: 2f6045e3-92b2-4773-a8de-3d0ec09c5d31
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28110
ms.openlocfilehash: 13448082e60bf8a8a33d3b7768039dc4c5df3087
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839604"
---
# <a name="c28110"></a>C28110


警告 C28110: ドライバーは、浮動小数点のハードウェア状態を保護する必要があります。 「Float の使用」を参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>浮動小数点演算については、 <strong>Kesavefloatingpointstate</strong>と<strong>Kerestorefloatingpointstate</strong>を使用します。 ディスプレイドライバーは、対応する<strong>Eng...</strong>ルーチンを使用する必要があります。</p></td>
</tr>
</tbody>
</table>

 

この警告は、カーネルモードでのみ適用されます。 ドライバーが[**KesavefloEngSaveFloatingPointState pointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)と[**kerestoreflopointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)、または[](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)と[**EngRestoreFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)によって保護されていない場合、ドライバーは float 型の変数または定数を使用しようとしています。

通常、ドライバーは最新のアプリケーションの浮動小数点コンテキストで実行されます。また、 [**Kesavefloの状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)によって保護されていない浮動小数点を使用すると、 [**Kerestorefloatingpointstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kerestorefloatingpointstate)によって他のを処理し、ドライバーの結果が正しくない、または予期しない結果になることがあります。

ディスプレイドライバーでは、 [**EngSaveFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)と[**EngRestoreFloatingPointState**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)を使用する必要があります。

このエラーのインスタンスが特定のフローパスに沿って検出されると、コード分析ツールによって後続の同様のエラーが抑制されます。 コード分析ツールでは、浮動小数点型引数を受け取る関数定義または浮動小数点型を返す関数定義では、このエラーは報告されません。これは、呼び出し元が使用を報告するためです。

この警告は、プログラムが関数呼び出しの周囲の浮動小数点の状態を保存および復元し、呼び出された関数が浮動小数点演算を実行する場合に、エラーとして発生することがあります。

関数が浮動小数点演算を意図的に使用していて、浮動小数点が安全であるコンテキストで呼び出されることを想定している場合は、関数に **\_カーネル\_float\_使用**して\_に注釈を付ける必要があります。 この注釈は、関数本体の警告を抑制し、呼び出しコンテキストが浮動小数点演算で安全に保護されていることを確認します。 浮動小数点演算が引数または戻り値に含まれている場合、結果は **\_カーネル\_float\_\_** 使用した場合と同じです。

\_カーネル\_使用することによって **\_使用される float\_** (または、適切な保存と復元の呼び出しを追加する) を使用して、警告が残っていない状態になるまでは、浮動小数点を使用するすべての関数は、浮動小数点の誤用を防ぐことができます。デバイス. 詳細については、「[ドライバーの浮動小数点注釈](floating-point-annotations-for-drivers.md)」を参照してください。

 

 






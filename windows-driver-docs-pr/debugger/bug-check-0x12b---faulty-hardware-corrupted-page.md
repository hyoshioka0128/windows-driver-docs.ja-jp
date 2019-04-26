---
title: バグ チェック 0x12B FAULTY_HARDWARE_CORRUPTED_PAGE
description: FAULTY_HARDWARE_CORRUPTED_PAGE のバグ チェックでは、0x0000012B の値を持ちます。 このバグ チェックでは、Windows メモリ マネージャーには、破損が検出されたことと、破損でしたのみが原因である物理アドレス指定を使用してメモリにアクセスするコンポーネントを示します。
ms.assetid: caa57d76-946f-4394-bfcf-1dbf3813a55b
keywords:
- バグ チェック 0x12B FAULTY_HARDWARE_CORRUPTED_PAGE
- FAULTY_HARDWARE_CORRUPTED_PAGE
ms.date: 01/18/2019
topic_type:
- apiref
api_name:
- FAULTY_HARDWARE_CORRUPTED_PAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 02cd8f6a04923fb0da6d64e7f2bb8e77fee732fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358969"
---
# <a name="bug-check-0x12b-faultyhardwarecorruptedpage"></a>バグ チェック 0x12B:障害のある\_ハードウェア\_破損した\_ページ

不良\_ハードウェア\_破損した\_ページのバグ チェックが 0x0000012B の値を持ちます。 このバグ チェックでは、Windows メモリ マネージャーには、破損が検出されたことと、破損でしたのみが原因である物理アドレス指定を使用してメモリにアクセスするコンポーネントを示します。  

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="faultyhardwarecorruptedpage-parameters"></a>障害のある\_ハードウェア\_破損した\_ページ パラメーター

メモリ マネージャーが FAULTY_HARDWARE_CORRUPTED_PAGE バグ チェックでは、2 つの異なるパラメーター セットを発生させるは 2 つのシナリオがあります。 

パラメーター 3 と 4 が両方とも 0 の場合は、バグのチェックは、メモリ マネージャーにゼロに設定すると想定されているページで、シングル ビット エラーが検出されたことを示します。

パラメーター 3 と 4 が 0 以外の場合は、物理メモリの破損のためのページを圧縮解除に失敗したため、圧縮されたストア マネージャーによってバグ チェックが発生します。


### <a name="memory-manager-page-not-zero-error-parameters"></a>メモリ マネージャー ページ エラー パラメーターに 0 以外 

このバグ チェックでは、このページで、シングル ビット エラーが見つかったことを示します。 これは、ハードウェア メモリのエラーです。

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
<td align="left"><p>仮想アドレスが破損したページにマップされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>物理的なページ数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Zero</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>Zero</p></td>
</tr>
</tbody>
</table>


### <a name="compressed-store-manager-error-parameters"></a>圧縮されたストア マネージャーのエラーのパラメーター 

 このバグ チェックでは、ストア マネージャー メモリ エラーが発生したことを示します。 認証の失敗、CRC エラー、または圧縮解除エラーがあります。

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
<td align="left"><p>FailStatus - エラーの種類を示します</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>読み取られているページの CompressedSize</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ソース バッファー</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ターゲット バッファー</p></td>
</tr>
</tbody>
</table>


## <a name="cause"></a>原因
-----

このバグチェックが物理メモリ アクセスによるメモリの破損によってのみ実行できます。 物理メモリの破損の原因は次のとおりです。

1.  欠陥のある RAM ハードウェア
2.  ドライバーまたはデバイスが正しくない DMA 操作または関連付けられている MDL 経由で物理ページを正しく変更します。
3.  ハードウェア デバイスまたはファームウェアのファームウェアが不正に電力の変化全体で物理的なページの変更などのメモリの破損が原因で破損しています。

注: 破損は、シングル ビット エラーによって発生したし、のバグ チェックが生成することがなく、この条件を自動的に修正がある場合、圧縮されたストア マネージャーを検出できます。 このバグチェックは、単一ビット エラーによって破損の原因がない場合、圧縮されたストア マネージャーによって報告されます。

Windows メモリ マネージャーとメモリの圧縮の詳細については、次を参照してください。[内部 7 の Windows エディションのパート 1](https://docs.microsoft.com/en-us/sysinternals/learn/windows-internals) Pavel Yosifovich、E. のある Mark Russinovich、David A. Solomon、Alex Ionescu でします。


## <a name="resolution"></a>解決方法
-----

**Windows メモリ診断ツール**

このバグ チェックが RAM ハードウェアの欠陥によって発生した場合、調査には、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして *、コンピューターのメモリの問題を診断*します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

[Windows カーネル モードのメモリ マネージャー](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager)

[Channel 9 ビデオ メモリ圧縮](https://channel9.msdn.com/Blogs/Seth-Juarez/Memory-Compression-in-Windows-10-RTM)

 

 





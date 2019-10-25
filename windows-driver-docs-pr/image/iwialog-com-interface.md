---
title: IWiaLog COM インターフェイス
description: IWiaLog COM インターフェイス
ms.assetid: e5d42b5d-796f-42f3-9c01-4234b8765ca6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ba8c608708f11feca58d20042732625aeaad079
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840799"
---
# <a name="iwialog-com-interface"></a>IWiaLog COM インターフェイス





[**IWiaLog インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwialog)は、MICROSOFT Windows XP 以降では廃止されており、現在はサポートされていません。 代わりに、WIA 診断ログマクロを使用してください。

旧バージョンとの互換性のためだけに用意されています。 このインターフェイスのメソッドを使用すると、ミニドライバーは、エラー、トレース、警告メッセージをログに書き込むことができます。 **IWiaLog**インターフェイスには、次のメソッドが用意されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-initializelog" data-raw-source="[&lt;strong&gt;IWiaLog::InitializeLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-initializelog)"><strong>IWiaLog:: InitializeLog</strong></a></p></td>
<td><p>ログユーティリティを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-log" data-raw-source="[&lt;strong&gt;IWiaLog::Log&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-log)"><strong>IWiaLog:: Log</strong></a></p></td>
<td><p>ファイルまたはその他のターゲットにメッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-hresult" data-raw-source="[&lt;strong&gt;IWiaLog::hResult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwialog-hresult)"><strong>IWiaLog:: hResult</strong></a></p></td>
<td><p>HRESULT を文字列に変換します。</p></td>
</tr>
</tbody>
</table>

 

このインターフェイスの詳細については、「 [IWiaLog interface And Diagnostics Log Macros](https://docs.microsoft.com/windows-hardware/drivers/ddi/_image/index)」を参照してください。

 

 





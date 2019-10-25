---
title: ドキュメントフィーダーの自動コマンド
description: ドキュメントフィーダーの自動コマンド
ms.assetid: dd6664d6-4853-4f97-85cc-39a7879d523e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3fec4b9c709a1657ba84aed479b55c3ac067d98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840892"
---
# <a name="automatic-document-feeder-commands"></a>ドキュメントフィーダーの自動コマンド


## <span id="ddk_automatic_document_feeder_commands_si"></span><span id="DDK_AUTOMATIC_DOCUMENT_FEEDER_COMMANDS_SI"></span>


このセクションのコマンドは、自動ドキュメントフィーダー (ADF) をサポートするマイクロドライバー用です。 マイクロドライバが自動ドキュメントフィーダーをサポートしていることを報告するには、コマンド\_INITIALIZE コマンドの実行中に、 [**Scaninfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)構造体の**adf**メンバーを 1 (ADF が両面印刷装置の場合は 2) に設定します。 これにより、WIA フラットドライバーは、ADF コントロールに必要なプロパティを追加し、このセクションのコマンドを使用します。

<span id="CMD_LOAD_ADF"></span><span id="cmd_load_adf"></span>CMD\_ロード\_ADF  
ページを ADF に読み込むために、WIA フラット化ドライバーによって呼び出されます。 このコマンドがデバイスに適用されない場合は、E\_NOTIMPL を返します。 このコマンドは、ページに自動的にフィードするデバイスに対しては省略可能です。

<span id="CMD_UNLOAD_ADF"></span><span id="cmd_unload_adf"></span>CMD\_\_ADF をアンロードします  
ADF からページをアンロードするために、WIA フラットドライブによって呼び出されます。 このコマンドがデバイスに適用されない場合は、E\_NOTIMPL を返します。 このコマンドは、ページのフィードを自動的に解除するデバイスに対しては省略可能です。

<span id="CMD_GETADFAVAILABLE"></span><span id="cmd_getadfavailable"></span>CMD\_GETADFAVAILABLE  
ADF が使用可能かどうかを判断するために、WIA フラットドライブによって呼び出されます。 ADF が使用可能な場合は、S\_OK を返します。 このコマンドがデバイスに適用されない場合は、E\_NOTIMPL を返します。

<span id="CMD_GETADFHASPAPER"></span><span id="cmd_getadfhaspaper"></span>CMD\_GETADFHASPAPER  
デバイスの ADF の紙の状態を取得するために、WIA フラットドライバーによって呼び出されます。 渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーを適切な状態の値に設定します。 (使用可能な状態の値については、「CMD\_ADFGETSTATUS」を参照してください)。

<span id="CMD_GETADFOPEN"></span><span id="cmd_getadfopen"></span>CMD\_GETADFOPEN  
CMD\_GETADFREADY と同じです。 このコマンドは、現在、WIA フラットドライブでは使用されていません。

<span id="CMD_GETADFSTATUS"></span><span id="cmd_getadfstatus"></span>CMD\_GETADFSTATUS  
デバイスにアタッチされている ADF の状態を取得するために、WIA フラットドライバーによって呼び出されます。 渡された[**VAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-val)構造体の**lVal**メンバーを適切な状態の値に設定します。 使用できる状態の値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Status</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MCRO_ERROR_GENERAL_ERROR</p></td>
<td><p>一般エラーです。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_OFFLINE</p></td>
<td><p>ADF またはデバイスがオフラインです。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_ERROR_PAPER_EMPTY</p></td>
<td><p>ADF には用紙がありません。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_PAPER_JAM</p></td>
<td><p>ADF で紙詰まりが発生しています。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_ERROR_PAPER_PROBLEM</p></td>
<td><p>ADF に用紙の問題があります。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_USER_INTERVENTION</p></td>
<td><p>ユーザーは、デバイスと対話する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_STATUS_OK</p></td>
<td><p>報告するエラーはありません。</p></td>
</tr>
</tbody>
</table>

 

<span id="CMD_GETADFUNLOADREADY"></span><span id="cmd_getadfunloadready"></span>CMD\_GETADFUNLOADREADY  
ADF がページのアンロードの準備ができているかどうかを判断するために、WIA フラットドライバーによって呼び出されます。 その場合は、S\_OK を返します。 このコマンドがデバイスに適用されない場合は、E\_NOTIMPL を返します。

 

 






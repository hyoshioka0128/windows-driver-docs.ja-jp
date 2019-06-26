---
title: 自動ドキュメント フィーダー コマンド
description: 自動ドキュメント フィーダー コマンド
ms.assetid: dd6664d6-4853-4f97-85cc-39a7879d523e
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76f590dd32e9c205031a17cf2c2d990e3dc50f3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366750"
---
# <a name="automatic-document-feeder-commands"></a>自動ドキュメント フィーダー コマンド


## <span id="ddk_automatic_document_feeder_commands_si"></span><span id="DDK_AUTOMATIC_DOCUMENT_FEEDER_COMMANDS_SI"></span>


このセクションのコマンドでは自動ドキュメント フィーダー (ADF) をサポートする microdrivers です。 設定、microdriver が自動ドキュメント フィーダーをサポートしていることを報告する、 **ADF**内のメンバー、 [ **SCANINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-_scaninfo) CMD 中に構造体を 1 (または 2 の場合は、ADF がある両面印刷ユニット)\_初期化コマンド。 ADF のコントロールの必要なプロパティを追加し、このセクションでは、コマンドを使用して、WIA ベッド ドライバーになります。

<span id="CMD_LOAD_ADF"></span><span id="cmd_load_adf"></span>CMD\_ロード\_ADF  
ADF にページを読み込む WIA ベッド ドライバーによって呼び出されます。 このコマンドが戻り、デバイスに適用されない場合\_NOTIMPL します。 このコマンドは、ページが自動的に提供するデバイスでは省略可能です。

<span id="CMD_UNLOAD_ADF"></span><span id="cmd_unload_adf"></span>CMD\_アンロード\_ADF  
ADF からページをアンロードする WIA ベッド ドライバーによって呼び出されます。 このコマンドが戻り、デバイスに適用されない場合\_NOTIMPL します。 このコマンドは、ページを自動的に unfeeds デバイスでは省略可能です。

<span id="CMD_GETADFAVAILABLE"></span><span id="cmd_getadfavailable"></span>CMD\_GETADFAVAILABLE  
ADF を使用できるかどうかを WIA ベッド ドライバーによって呼び出されます。 ADF が使用可能な戻り値の秒の場合\_ok をクリックします。 このコマンドが戻り、デバイスに適用されない場合\_NOTIMPL します。

<span id="CMD_GETADFHASPAPER"></span><span id="cmd_getadfhaspaper"></span>CMD\_GETADFHASPAPER  
デバイスの ADF の用紙の状態を取得する WIA ベッド ドライバーによって呼び出されます。 設定、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体を適切な状態の値。 (「Cmd」を参照してください。\_ADFGETSTATUS の状態の値。)

<span id="CMD_GETADFOPEN"></span><span id="cmd_getadfopen"></span>CMD\_GETADFOPEN  
「Cmd」と同じ\_GETADFREADY します。 現在、このコマンドは、WIA ベッド ドライバーによって使用されていません。

<span id="CMD_GETADFSTATUS"></span><span id="cmd_getadfstatus"></span>CMD\_GETADFSTATUS  
デバイスに接続されている、ADF の状態を取得する、WIA ベッド ドライバーによって呼び出されます。 設定、 **lVal**の渡されたメンバー [ **VAL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamicro/ns-wiamicro-val)構造体を適切な状態の値。 状態の値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状況</th>
<th>説明</th>
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
<td><p>ADF には、ホワイト ペーパーはありません。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_PAPER_JAM</p></td>
<td><p>ADF では、紙詰まりがあります。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_ERROR_PAPER_PROBLEM</p></td>
<td><p>ADF では、用紙の問題があります。</p></td>
</tr>
<tr class="even">
<td><p>MCRO_ERROR_USER_INTERVENTION</p></td>
<td><p>ユーザーは、デバイスと対話する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>MCRO_STATUS_OK</p></td>
<td><p>エラー レポートにはありません。</p></td>
</tr>
</tbody>
</table>

 

<span id="CMD_GETADFUNLOADREADY"></span><span id="cmd_getadfunloadready"></span>CMD\_GETADFUNLOADREADY  
ADF にロードするページの準備があるかどうかを判断、WIA ベッド ドライバーによって呼び出されます。 そうである場合は、返す S\_ok をクリックします。 このコマンドが戻り、デバイスに適用されない場合\_NOTIMPL します。

 

 






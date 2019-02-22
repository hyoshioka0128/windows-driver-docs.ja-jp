---
title: WIA\_DPS\_ドキュメント\_処理\_状態
description: WIA\_DPS\_ドキュメント\_処理\_STATUS プロパティには、スキャナーのインストール済みのフラット ベッド、ドキュメント フィーダー付きまたは両面印刷ユニットの現在の状態が含まれています。
ms.assetid: b95c64ee-b06c-4786-87d3-d8a0f91dcba2
keywords:
- WIA_DPS_DOCUMENT_HANDLING_STATUS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ca93425375b610ad3eaa5c77da7916b4df5e20b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536674"
---
# <a name="wiadpsdocumenthandlingstatus"></a>WIA\_DPS\_ドキュメント\_処理\_状態


WIA\_DPS\_ドキュメント\_処理\_STATUS プロパティには、スキャナーのインストール済みのフラット ベッド、ドキュメント フィーダー付きまたは両面印刷ユニットの現在の状態が含まれています。

## <span id="ddk_wia_dps_document_handling_status_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_STATUS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPS\_ドキュメント\_処理\_STATUS プロパティ スキャナー デバイスが使用する準備がかどうかを判断します。 このプロパティの読み取りは、ユーザーがイメージを取得する前に、用紙がフィーダーがかどうかを確認する最適な方法です。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表では、Windows 8 および Windows の以降のバージョンで有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IMPRINTER_READY</p></td>
<td><p>・ インプリント ・/承認者の・ インプリント ・機能を有効にして使用できる状態です。</p></td>
</tr>
<tr class="even">
<td><p>ENDORSER_READY</p></td>
<td><p>・ インプリント ・/承認者の裏書き機能を有効にして使用できる状態です。</p></td>
</tr>
<tr class="odd">
<td><p>BARCODE_READER_READY</p></td>
<td><p>バーコード リーダーが有効で使用できる状態です。</p></td>
</tr>
<tr class="even">
<td><p>PATCH_CODE_READER_READY</p></td>
<td><p>修正プログラム コードのリーダーが有効で使用できる状態です。</p></td>
</tr>
<tr class="odd">
<td><p>MICR_READER_READY</p></td>
<td><p>MICR リーダーが有効で使用できる状態です。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows Vista と Windows XP の両方で有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DUP_READY</p></td>
<td><p>両面印刷ユニットは有効になっているを使用する準備が整います。</p></td>
</tr>
<tr class="even">
<td><p>FEED_READY</p></td>
<td><p>ドキュメント フィーダー付きでは、読み込まれたページがあるしが使用できる状態。</p></td>
</tr>
<tr class="odd">
<td><p>FLAT_COVER_UP</p></td>
<td><p>フラット ベッド カバーです。</p></td>
</tr>
<tr class="even">
<td><p>FLAT_READY</p></td>
<td><p>フラット ベッドは、使用できる状態です。</p></td>
</tr>
<tr class="odd">
<td><p>PAPER_JAM</p></td>
<td><p>ドキュメントがドキュメント フィーダー付きでスタックします。</p></td>
</tr>
<tr class="even">
<td><p>PATH_COVER_UP</p></td>
<td><p>用紙のパスはカバーされ、適切な操作が原因です。</p></td>
</tr>
</tbody>
</table>

 

次の表では、だけで Windows vista では有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FILM_TPA_READY</p></td>
<td><p>透明度のアダプターがインストールされ、使用できる状態です。</p></td>
</tr>
<tr class="even">
<td><p>STORAGE_READY</p></td>
<td><p>記憶域デバイスがインストールされ、使用できる状態です。</p></td>
</tr>
<tr class="odd">
<td><p>STORAGE_FULL</p></td>
<td><p>記憶域がいっぱいです。アップロード操作することはできません。</p></td>
</tr>
<tr class="even">
<td><p>MULTIPLE_FEED</p></td>
<td><p>複数のフィードが発生しました。この種類のフィードは、通常は PAPER_JAM 値で発生します。</p></td>
</tr>
<tr class="odd">
<td><p>DEVICE_ATTENTION</p></td>
<td><p>スキャナーのユーザーの介入を必要とするエラーがあります。</p></td>
</tr>
<tr class="even">
<td><p>LAMP_ERR</p></td>
<td><p>スキャナーは、lamp に問題があるし、準備ができていません。</p></td>
</tr>
</tbody>
</table>

 

**注**  基本定義のカスタム定義はありません。 状態フラグの値のカスタム拡張機能を作成することはできません。 カスタム状態レポートが必要な場合は、カスタム プロパティを定義する必要があります。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 






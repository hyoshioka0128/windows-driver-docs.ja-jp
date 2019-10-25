---
title: WDI TLV パーサー インターフェイスの概要
description: このセクションでは、WDI TLV parser インターフェイスの概要について説明します。
ms.assetid: FD204F24-0336-4A54-992C-ACF46565D8D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a543c6910e950a2d5a3810db2ac9b2e18ec2b2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838022"
---
# <a name="wdi-tlv-parser-interface-overview"></a>WDI TLV パーサー インターフェイスの概要


## <a name="callee-allocation-model"></a>呼び出し先割り当てモデル


ドライバー内のエントリポイントは、TLVs を含むメッセージまたは通知を受信します。 コードは、メッセージ ID を抽出し、処理する ID であるかどうかを判断した後、汎用解析ルーチンを呼び出し、TLV blob ( [**WDI\_message\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)) を渡して、Tlvs を C 構造体に解析します。

```c
ndisStatus = Parse(
    cbBufferLength,
    pvBuffer,
    messageId,
    &Context,
    &pParsed);
```

返されたエラーを確認した後、次の例のように、コードは出力バッファー (*Pparsed*) を具象型にキャストできます。

```c
((WDI_INDICATION_BSS_ENTRY_LIST_PARAMETERS*)pParsed)
```

解析されたデータを呼び出し元が終了すると、呼び出し元はメモリをパーサーに戻す必要があります。 パーサーは、適切なデータを解放するために、割り当てに使用される元のメッセージ ID を認識している必要があります。

```c
FreeParsed(messageId, pParsed);
pParsed = NULL;
```

## <a name="caller-allocation-model"></a>呼び出し元の割り当てモデル


このモデルでは、呼び出し元は、解析する正しい特定の TLV を既に決定しており、ヒープへの割り当てを回避するためにスタックローカルを使用している可能性があります。 呼び出し元は、ローカルのを作成し、特定の解析ルーチンを呼び出します。 API にはメッセージ ID は必要ありません。パラメーターは、1つ少ないレベルの間接参照を使用して厳密に型指定されます。

```c
WDI_GET_ADAPTER_CAPABILITIES_PARAMETERS adapterCapabilitiesParsed;

ndisStatus = ParseWdiGetAdapterCapabilities(
    cbBufferLength,
    pvBuffer,
    &Context
    &adapterCapabilitiesParsed);
```

構造体を使用して呼び出し元が終了した後、呼び出し元は解析中に作成された割り当てをクリーンアップする機会をパーサーに提供し、再利用できるように構造をワイプする必要があります。 パラメーターは厳密に型指定されているため、呼び出し先は追加のパラメーターを必要としません。

```c
CleanupParsedWdiGetAdapterCapabilities(&adapterCapabilitiesParsed);
```

CleanupParse API を呼び出した後、構造内のすべてのデータが無効になります。

一部のメッセージには、関連付けられたデータがありません。 API の完全性を実現するために、適切に名前を付けた Parse メソッドが用意されています。 これらのメソッドは、バイトストリームが空であることを検証します。 パラメーターの型には typedef が用意されていますが、呼び出し元の割り当てモデルを使用している場合は、呼び出し元が out パラメーターに NULL を渡すこともできます。 いずれの場合も、パーサーは、空の定数解析構造体を返すことによって割り当てを回避します。 呼び出し元は、この返された空の構造体に書き込むことはできません (したがって、唯一のフィールドは **\_Reserved**という名前になります)。 これらのメッセージについては、「追加データなし」と記載されています。 ヘッダー内のデータは十分です。

## <a name="message-direction"></a>メッセージの方向


ほとんどのメッセージの形式は、M1 と M0、M3、M4 によって異なります。 このために対応するために、このようなメッセージの解析と生成には異なる Api があります。 M1 メッセージの場合、Api は、解析<em>&lt;messagename&gt;</em>toihv の命名規則に従い、<em>&lt;messagename&gt;</em>toihv を生成します。 M0、M3、または M4 メッセージの場合、Api は、fromihv の解析<em>&lt;messagename&gt;</em>の名前付け規則に従います。または、<em>&lt;messagename&gt;</em>Fromihv を生成します。 ただし、IHV ミニポートのコードを簡略化するために、<em>&lt;messagename&gt;</em>Toihv を解析し、<em>&lt;Messagename&gt;</em>を生成して生成するために、エイリアス解析<em>&lt;messagename&gt;</em>に追加され<em>&lt;MessageName&gt;</em>fromihv。 IHV コードは、独自の M3 を解析する必要がある場合、または M1 を生成する必要がある場合にのみ、このエイリアスを認識する必要があります。

## <a name="error-codes"></a>エラー コード


TLV パーサージェネレーターは、いくつかの異なる NDIS\_状態コードを返すことができます。 詳細については、WPP トレースログを参照してください。 ログは常に根本原因を示す必要があります。 最も一般的なエラーコードとその意味の一覧を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>解析時に、固定サイズの TLV のサイズが正しくないことを示します。 リストについては、全体のサイズが個々の要素のサイズの倍数ではなく、要素の数が多いことを意味します。 これは、1つ以上が必要な場合に、リストに0個の要素が含まれていることも意味します。 0個の要素が必要な場合は、 <em>Optional_IsPresent</em>を false に設定する必要があります (TLV ヘッダーをバイトストリームにすることはできません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_BUFFER_OVERFLOW</p></td>
<td align="left"><p>生成時に、配列内の要素数 (list) が原因で、TLV ヘッダー内の2バイト<strong>長</strong>フィールドがオーバーフローすることを示します。 要素の数を減らす必要があります。 これは、外側の TLV が内部 TLVs 超えている (または大きすぎる) 場合にも発生し、ヘッダーの2バイト<strong>長</strong>フィールドは再びオーバーフローします。</p>
<p>解析時に、TLV ヘッダーの<strong>長さ</strong>フィールドが外側の TLV またはバイトストリームよりも大きいことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_FILE_NOT_FOUND</p></td>
<td align="left"><p>解析時に、必要な TLV がバイトストリームに存在しないことを示します。 これは通常、バイトストリームのジェネレーターを使用するバグです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_RESOURCES</p></td>
<td align="left"><p>生成時に、アロケーターが失敗したことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_UNSUPPORTED_REVISION</p></td>
<td align="left"><p>解析時または生成時に、<strong>コンテキスト</strong>パラメーターが NULL であるか、または<strong>Peerversion</strong>が<strong>WDI_VERSION_MIN_SUPPORTED</strong>未満です。</p></td>
</tr>
</tbody>
</table>

 

 

 






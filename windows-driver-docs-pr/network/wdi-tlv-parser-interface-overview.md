---
title: WDI TLV パーサー インターフェイスの概要
description: このセクションでは、WDI TLV パーサー インターフェイスの概要を説明します
ms.assetid: FD204F24-0336-4A54-992C-ACF46565D8D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296a68189d454f66f7097d14200cc676f7f44be8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385065"
---
# <a name="wdi-tlv-parser-interface-overview"></a>WDI TLV パーサー インターフェイスの概要


## <a name="callee-allocation-model"></a>呼び出し先の割り当てのモデル


ドライバー内のエントリ ポイントは、メッセージまたは TLVs を含むを示す値を受け取ります。 コードのメッセージ ID を抽出しますと、汎用的な解析ルーチンを呼び出すが、ID を処理する場合と判断したと TLV blob を渡します (範囲を超えた後に、 [ **WDI\_メッセージ\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_message_header)) C 構造体に、TLVs を解析します。

```c
ndisStatus = Parse(
    cbBufferLength,
    pvBuffer,
    messageId,
    &Context,
    &pParsed);
```

エラーの戻り値を確認するには、後に、コードが出力バッファーをキャストできます (*pParsed*) などで具象型に、次の例です。

```c
((WDI_INDICATION_BSS_ENTRY_LIST_PARAMETERS*)pParsed)
```

呼び出し元が完了すると、解析されたデータと、呼び出し元は、パーサーにメモリを返す必要があります。 パーサーは、ID が正しいデータを解放するための割り当てに使用する元のメッセージを把握する必要があります。

```c
FreeParsed(messageId, pParsed);
pParsed = NULL;
```

## <a name="caller-allocation-model"></a>呼び出し元割り当てモデル


このモデルでは、呼び出し元は、解析を正しく特定 TLV が既に決定し、ヒープ上の割り当てを回避するためにローカル スタックを使用して可能性があります。 呼び出し元は、ローカルを作成し、特定の解析ルーチンを呼び出します。 API では、メッセージ ID を必要はありませんし、パラメーターが 1 つ小さいレベルの間接参照を厳密に型指定します。

```c
WDI_GET_ADAPTER_CAPABILITIES_PARAMETERS adapterCapabilitiesParsed;

ndisStatus = ParseWdiGetAdapterCapabilities(
    cbBufferLength,
    pvBuffer,
    &Context
    &adapterCapabilitiesParsed);
```

呼び出し元が終了したら、構造を使用して、呼び出し元が、解析時に行った、すべての割り当てをクリーンアップする機会をパーサーに渡すし、を再利用できるように、構造体をワイプする必要があります。 パラメーターは厳密に型指定、ので、呼び出し先では、その他のパラメーターは必要はありません。

```c
CleanupParsedWdiGetAdapterCapabilities(&adapterCapabilitiesParsed);
```

CleanupParse API を呼び出した後、構造内のすべてのデータは無効です。

一部のメッセージには、関連付けられたデータはありません。 API の完全を期すため、適切に名前付きの Parse メソッドが提供されます。 これらのメソッドは、バイト ストリームが空であることを検証します。 Typedef は、パラメーターの型に提供されますが、呼び出し元は、また、呼び出し元割り当てモデルを使用している場合、out パラメーターの NULL を渡すことができます。 すべてのケースでは、パーサーは、定数の空の解析の構造体を返すことによって割り当てを回避します。 呼び出し元がこの返される空の構造体に書き込むことはありません必要があります (唯一のフィールドの名前はそのため **\_占有**)。 これらのメッセージは"その他のデータがありませんとして記載されています。 ヘッダー内のデータで十分です"。

## <a name="message-direction"></a>メッセージの方向


ほとんどのメッセージと、M0、M3、または M4、M1 の別の形式であります。 これに対応するためには、このようなメッセージは、別の解析があるし、Api を生成します。 M1 のメッセージの解析の名前付け規則に従う Api<em>&lt;MessageName&gt;</em>ToIhv または生成<em>&lt;MessageName&gt;</em>ToIhv します。 M0、M3、または M4 のメッセージの解析の名前付け規則に従う Api<em>&lt;MessageName&gt;</em>FromIhv または生成<em>&lt;MessageName&gt;</em> FromIhv します。 ただし、IHV ミニポート内のコードを簡略化する次のように定義します解析の別名に追加されます<em>&lt;MessageName&gt;</em> 解析を<em>&lt;MessageName&gt;</em>ToIhv と。生成<em>&lt;MessageName&gt;</em> を生成する<em>&lt;MessageName&gt;</em>FromIhv します。 IHV コードのみ、独自の M3 を解析するか、M1 を生成する必要がある場合、このエイリアスを意識する必要があります。

## <a name="error-codes"></a>エラー コード


TLV パーサー ジェネレーターがいくつかの異なる NDIS を返す\_状態コード。 詳細については、WPP トレース ログを参照してください。 ログは根本原因を常に示す必要があります。 最も一般的なエラー コードとその意味の一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_INVALID_DATA</p></td>
<td align="left"><p>、解析時に、固定サイズの TLV が不適切なサイズであることを示します。 一覧についてには全体のサイズが個々 の要素のサイズの倍数かが必要以上の要素があることを意味します。 一覧には 0 の要素が含まれる 1 つ以上が必要な場合も可能性。 0 の要素が必要な場合<em>Optional_IsPresent</em> (TLV ヘッダーは、バイト ストリームではない必要があります) を false に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_BUFFER_OVERFLOW</p></td>
<td align="left"><p>配列 (リスト) 内の要素の数、により、2 バイトをオーバーフローしたことを示しますこの生成するとき、<strong>長さ</strong>TLV ヘッダー内でフィールド。 要素の数を減らす必要があります。 これは、外部の TLV がある多すぎる (またはの大きすぎます) 内部 TLVs、もう一度 2 バイトのオーバーフロー時にも発生<strong>長さ</strong>ヘッダーのフィールド。</p>
<p>解析するには、このこと TLV ヘッダーの<strong>長さ</strong>フィールドが外部 TLV またはバイト ストリームを超えています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_FILE_NOT_FOUND</p></td>
<td align="left"><p>を解析するときに、必要な TLV がバイト ストリームに存在しないことを示します。 バイト ストリームのジェネレーターのバグでは、通常は。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_STATUS_RESOURCES</p></td>
<td align="left"><p>生成するとき、アロケーターが失敗したことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NDIS_STATUS_UNSUPPORTED_REVISION</p></td>
<td align="left"><p>解析やを生成するときに、<strong>コンテキスト</strong>パラメーターが null の場合、または<strong>PeerVersion</strong>がより小さい<strong>WDI_VERSION_MIN_SUPPORTED</strong>します。</p></td>
</tr>
</tbody>
</table>

 

 

 






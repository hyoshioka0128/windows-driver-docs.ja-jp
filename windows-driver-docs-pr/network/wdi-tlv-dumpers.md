---
title: WDI TLV ダンパー
description: パーサーのジェネレーターのライブラリには、トレース ステートメントに TLV バイト配列をデコードするルーチンがあります。
ms.assetid: 4F8B53E5-1F51-4119-AC06-7A710340E4A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4158a0d1865763c55a67d0340844830e823324
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358565"
---
# <a name="wdi-tlv-dumpers"></a>WDI TLV ダンパー


パーサーのジェネレーターのライブラリには、トレース ステートメントに TLV バイト配列をデコードするルーチンがあります。

```C++
    typedef _Function_class_( TlvDumperCallback ) void( __stdcall *TlvDumperCallback )(_In_ UINT_PTR Context, _In_z_ _Printf_format_string_ PCSTR Format, ...);

    void __stdcall TraceUnknownTlvByteStream(
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer );

    void __stdcall TraceMessageTlvByteStream(
        _In_ ULONG MessageId,
        _In_ BOOLEAN fToIhv,
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer );

    void __stdcall DumpUnknownTlvByteStream(
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer,
        _In_opt_ ULONG_PTR Context,
        _In_opt_ TlvDumperCallback pCallback );

    void __stdcall DumpMessageTlvByteStream(
        _In_ ULONG MessageId,
        _In_ BOOLEAN fToIhv,
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer,
        _In_opt_ ULONG_PTR Context,
        _In_opt_ TlvDumperCallback pCallback );
```

WPP トレースのみ必要がある場合は、コードのサイズとログのサイズ (より少ない文字列で ETL ファイル) に影響を最小限に最適化されているようにトレース Api を使用します。 一般的な必要がある場合ダンパーを目的、WPP トレースを含めるし、コールバック ルーチンを含めることも、ダンプの Api を使用します。 スタブのドライバーでは、このコールバック ルーチンを使用して、DebugPrint Api を使用してカーネル デバッガーに出力をリダイレクトする例があります。

ダンパーとは異なり、解析と Api の生成には、非常に制限の少ないです。 指定したメッセージまたは TLV の正規の形式に関係なく、可能な限り TLV バイトの意味を作成しようとします。 つまりダンパーのデコードおよびパーサーを拒否したことをダンプが正しくです。

**警告**  ダンパーは、バイトを人間が読める形式に正常にデコードする場合、でも、必ずしも、バイトは、整形式の TLV します。

 

などの解析 Api、 *pBuffer*ポインターと*BufferLength*パラメーター ヘッダーを除外し、最初の TLV を直接ポイントします。

Api のメッセージのバリアントは、メッセージ ID を含めるし、メッセージの方向を強化、TLV あいまいさを解消します。 同じ TLV ID は、コンテキストに応じてさまざまな方法でデコードできますので便利です。 たとえば、 [ **WDI\_TLV\_BSSID** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)直接含めることができます、 [ **WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)の一部に[OID\_WDI\_タスク\_スキャン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-scan)の一覧を含めることができますか**WDI\_MAC\_アドレス**の一部に[ **WDI\_TLV\_P2P\_属性**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes)します。

 

 






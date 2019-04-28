---
title: WDI TLV ダンパー
description: パーサーのジェネレーターのライブラリには、トレース ステートメントに TLV バイト配列をデコードするルーチンがあります。
ms.assetid: 4F8B53E5-1F51-4119-AC06-7A710340E4A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cee50be2223923c03fa3ebcd1874dd9152f150a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380871"
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

Api のメッセージのバリアントは、メッセージ ID を含めるし、メッセージの方向を強化、TLV あいまいさを解消します。 同じ TLV ID は、コンテキストに応じてさまざまな方法でデコードできますので便利です。 たとえば、 [ **WDI\_TLV\_BSSID** ](https://msdn.microsoft.com/library/windows/hardware/dn926153)直接含めることができます、 [ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)の一部に[OID\_WDI\_タスク\_スキャン](https://msdn.microsoft.com/library/windows/hardware/dn925959)の一覧を含めることができますか**WDI\_MAC\_アドレス**の一部に[ **WDI\_TLV\_P2P\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn897863)します。

 

 






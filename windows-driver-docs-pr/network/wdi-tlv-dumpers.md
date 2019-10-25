---
title: WDI TLV ダンパー
description: パーサージェネレーターライブラリには、TLV バイト配列をトレースステートメントにデコードするルーチンがあります。
ms.assetid: 4F8B53E5-1F51-4119-AC06-7A710340E4A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88cbfdefeee3f0e5c0bbfae2894c28492b5f75cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834103"
---
# <a name="wdi-tlv-dumpers"></a>WDI TLV ダンパー


パーサージェネレーターライブラリには、TLV バイト配列をトレースステートメントにデコードするルーチンがあります。

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

WPP トレースのみが必要な場合は、トレース Api を使用して、コードサイズとログサイズ (ETL ファイル内の文字列の数) に最小限の影響を与えるように最適化します。 より汎用的なダンパーが必要な場合は、そのダンプ Api を使用します。これには、WPP トレースが含まれ、コールバックルーチンも含まれます。 スタブドライバーには、このコールバックルーチンを使用して、DebugPrint Api 経由でカーネルデバッガーに出力をリダイレクトする例が含まれています。

解析と生成 Api とは異なり、ダンパーは非常に制限されていません。 指定されたメッセージまたは TLV の正規の形式に関係なく、可能な限りの TLV バイトを意味します。 これは、ダンパーが、パーサーによって拒否されたものを正しくデコードおよびダンプする可能性があることを意味します。

**警告**  ダンパーがバイトを人間が判読できる形式に正常にデコードした場合、バイトが適切な形式の TLV であることを意味するわけではありません。

 

解析 Api と同様に、 *Pbuffer*ポインターと*bufferlength*パラメーターでは、ヘッダーを除外し、最初の TLV を直接ポイントする必要があります。

Api のメッセージバリアントには、TLV をより明確に区別するためのメッセージ ID とメッセージの方向が含まれます。 これは、コンテキストに応じて異なる方法で同じ TLV ID をデコードできるため便利です。 たとえば、 [**WDI\_TLV\_BSSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)には、 [OID\_WDI\_タスク\_スキャン](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-scan)の一部の場合に[**WDI\_mac\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)を直接含めることができます。また、WDI\_mac の一覧を含めることもでき **\_** WDI\_TLV の一部の場合は、 [**P2P\_属性\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes)ます。

 

 






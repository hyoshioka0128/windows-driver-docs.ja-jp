---
title: UEFI のシンプルな I/O プロトコル
description: UEFI のシンプルな I/O プロトコル
ms.assetid: 0cb55bf5-71e9-4b59-aef1-7d74eb331a18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833dd66b6dcf8c302842bf6bcf542c0f1634b867
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337377"
---
# <a name="uefi-simple-io-protocol"></a>UEFI のシンプルな I/O プロトコル


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサ アーキテクチャにのみ適用可能性があります。

 

単純な I/O プロトコルは、デバイスとプリブート環境でのホスト コンピューター間の通信を有効にするツールの点滅によって使用されます。

**注**  点滅ツールに関する情報がこのドキュメントの今後のリリースでことができます。

 

## <a name="efisimplewinphoneioprotocol"></a>EFI\_単純\_WINPHONE\_IO\_プロトコル


このセクションの詳細な説明を提供する**EFI\_単純\_WINPHONE\_IO\_プロトコル**します。 このプロトコルは、ホストと、プリブート環境でデバイスの単純な通信に使用します。

**GUID**

```cpp
// {BDE900DD-190A-4c7d-9663-16BA8ED88B55}
#define EFI_SIMPLE_WINPHONE_IO_PROTOCOL_GUID \
  { 0xbde900dd, 0x190a, 0x4c7d, 0x96, 0x63, 0x16, 0xba, 0x8e, \
   0xd8, 0x8b, 0x55 };
```

**リビジョン番号**

```cpp
#define EFI_SIMPLE_WINPHONE_IO_PROTOCOL_REVISION   0x00010001
```

**プロトコル インターフェイス構造体**

```cpp
typedef struct _EFI_SIMPLE_WINPHONE_IO_PROTOCOL {
  UINT32                                        Revision;
  EFI_SIMPLE_WINPHONE_IO_INITIALIZE             Initialize;
  EFI_SIMPLE_WINPHONE_IO_READ                   Read;
  VOID*                                         Reserved;
  EFI_SIMPLE_WINPHONE_IO_WRITE                  Write;
  EFI_SIMPLE_WINPHONE_IO_GET_MAXPACKET_SIZE     GetMaxPacketSize;
} EFI_SIMPLE_WINPHONE_IO_PROTOCOL;
```

### <a name="members"></a>メンバー

<a href="" id="revision"></a>**リビジョン**  
リビジョン、 **EFI\_単純\_WINPHONE\_IO\_プロトコル**準拠します。 すべての将来のリビジョンは、旧バージョンと互換性のあるである必要があります。 場合は、今後のバージョンは旧バージョンと互換性のある、別の GUID を使用する必要があります。

<a href="" id="initialize"></a>**初期化します。**  
この関数は、ホスト コンピューターからの接続を待機します。 参照してください[EFI\_単純\_WINPHONE\_IO\_プロトコル。初期化](efi-simple-winphone-io-protocolinitialize.md)します。

<a href="" id="read"></a>**読み取り**  
ホスト コンピューターからバイトのバッファーを受け取ります。 参照してください[EFI\_単純\_WINPHONE\_IO\_プロトコル。読み取り](efi-simple-winphone-io-protocolread.md)します。

<a href="" id="reserved-"></a>**予約されています**   
将来使用するために予約されています。

<a href="" id="write"></a>**書き込み**  
バイトのバッファーをホスト コンピューターに送信します。 参照してください[EFI\_単純\_WINPHONE\_IO\_プロトコル。書き込み](efi-simple-winphone-io-protocolwrite.md)します。

<a href="" id="getmaxpacketsize"></a>**GetMaxPacketSize**  
このプロトコルによってサポートされる最大パケット サイズを返します。 参照してください[EFI\_単純\_WINPHONE\_IO\_プロトコル。GetMaxPacketSize](efi-simple-winphone-io-protocolgetmaxpacketsize.md)します。


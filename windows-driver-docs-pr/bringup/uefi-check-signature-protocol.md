---
title: UEFI チェック署名プロトコル
description: UEFI チェック署名プロトコル
ms.assetid: 71df491f-c507-4ca4-831b-50ca95167fb3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0bbaf1dd52f10bccb68f234e32bc1071874716a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558795"
---
# <a name="uefi-check-signature-protocol"></a>UEFI チェック署名プロトコル


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサ アーキテクチャにのみ適用可能性があります。

 

チェック署名プロトコルには、点滅ツール、FFU でカタログ ファイルの署名を検証し、ハッシュ テーブルのハッシュが、カタログ ファイルで指定されたハッシュと一致していることを確認ができます。

**注**  FFU ファイルおよび点滅ツールの構造に関する情報は、このドキュメントの今後のリリースで提供されます。

 

## <a name="efichecksigprotocol"></a>EFI\_CHECKSIG\_プロトコル


このセクションの詳細な説明を提供する、 **EFI\_CHECKSIG\_プロトコル**します。

**GUID**

```cpp
// {E52500C3-4BF4-41A5-9692-6DF73DBFB9FE}
#define EFI_CHECKSIG_PROTOCOL_GUID \
  { 0xe52500c3, 0x4bf4, 0x41a5, { 0x96, 0x92, 0x6d, 0xf7, 0x3d, 0xbf, 0xb9, 0xfe } }
```

**リビジョン番号**

```cpp
#define EFI_SIMPLE_WINPHONE_IO_PROTOCOL_REVISION   0x00000000
```

**プロトコル インターフェイス構造体**

```cpp
struct _EFI_CHECKSIG_PROTOCOL {
  UINT32 Revision;
  EFI_CHECK_SIG_AND_HASH EfiCheckSignatureAndHash;
};
```

**メンバー**

<a href="" id="revision"></a>**リビジョン**  
リビジョン、 **EFI\_CHECKSIG\_プロトコル**準拠します。 すべての将来のリビジョンは、旧バージョンと互換性のあるである必要があります。 場合は、今後のバージョンは旧バージョンと互換性のある、別の GUID を使用する必要があります。

<a href="" id="efichecksignatureandhash"></a>**EfiCheckSignatureAndHash**  
署名と FFU カタログ ファイルのハッシュを確認します。 参照してください[EFI\_CHECKSIG\_プロトコル。EfiCheckSignatureAndHash](efi-checksig-protocolefichecksignatureandhash.md)

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

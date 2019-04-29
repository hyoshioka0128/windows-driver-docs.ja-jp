---
title: EFI_RNG_PROTOCOL
description: EFI_RNG_PROTOCOL は、EFI ドライバーからランダムな数の生成 (RNG) 値を取得するために使用します。
ms.assetid: 927E2C40-973B-49AB-ACD5-2A3532827D74
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dfd1242d96af53444de42881f89b8410e1cb5a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335089"
---
# <a name="efirngprotocol"></a>EFI\_RNG\_プロトコル


EFI\_RNG\_プロトコルを使用して、EFI ドライバーからランダムな数の生成 (RNG) 値を取得します。

## <a name="syntax"></a>構文


```cpp
#define EFI_RNG_PROTOCOL_GUID \
  {0x3152bca5, 0xeade, 0x433d, 0x86, 0x2e, 0xc0, 0x1c, 0xdc, 0x29, 0x1f, 0x44};

typedef struct _EFI_RNG_PROTOCOL {
    EFI_RNG_GET_INFO    GetInfo;
    EFI_RNG_GET_RNG     GetRNG;
} EFI_RNG_PROTOCOL;
```

## <a name="members"></a>Members


<a href="" id="getinfo"></a>**GetInfo**  
ドライバー RNG アルゴリズムに関する情報を返しますをサポートしています。 詳細については、次を参照してください。 [EFI\_RNG\_プロトコル。GetInfo](efi-rng-protocol-getinfo.md)します。

<a href="" id="getrng"></a>**GetRNG**  
省略可能な RNG アルゴリズムを使用して RNG 値を返します。 詳細については、次を参照してください。 [EFI\_RNG\_プロトコル。GetRNG](efi-rng-protocol-getrng.md)します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 





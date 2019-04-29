---
title: EFI_RNG_ALGORITHM_LIST 構造体
description: このデータ構造体には、サポートされているランダムな数の生成 (RNG) アルゴリズムの一覧が含まれています。
ms.assetid: 1481330F-78F3-4C18-BD19-3B4984E0138F
keywords:
- EFI_RNG_ALGORITHM_LIST 構造体
- PEFI_RNG_ALGORITHM_LIST 構造体のポインター
topic_type:
- apiref
api_name:
- EFI_RNG_ALGORITHM_LIST
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8437c21fd7e2895330f60f09798eedcb4fc55026
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328007"
---
# <a name="efirngalgorithmlist-structure"></a>EFI\_RNG\_アルゴリズム\_リスト構造


このデータ構造体には、サポートされているランダムな数の生成 (RNG) アルゴリズムの一覧が含まれています。

<a name="syntax"></a>構文
------

```cpp
typedef struct _EFI_RNG_ALGORITHM_LIST {
  UINT32     AlgorithmsCount;
  EFI_GUID * Algorithms;
} EFI_RNG_ALGORITHM_LIST, *PEFI_RNG_ALGORITHM_LIST;
```

<a name="members"></a>メンバー
-------

**AlgorithmsCount**  
リスト内のアルゴリズムの数。

**アルゴリズム**  
RNG アルゴリズムの一覧へのポインター。 各アルゴリズムは`sizeof(EFI_GUID)`バイト長。 EFI を使用してこのメモリを解放する呼び出し元の責任\_ブート\_サービス-&gt;FreePool() します。

<a name="remarks"></a>注釈
-------

実装では、RNG 値を指定する 1 つまたは複数の方法をサポート可能性があります。 サポートされている RNG アルゴリズムの一覧は、この構造体で表されます。

次の一覧は EFI の選択範囲の EFI GUID 値を提供\_RNG\_プロトコル アルゴリズム。 一覧は、すべてを網羅するものではありません、ベンダーや他の業界標準で補強することがあります。

```cpp
#define EFI_RNG_ALGORITHM_SP800_90_HASH_256_GUID   \
  {0xa7af67cb, 0x603b, 0x4d42, 0xba, 0x21, 0x70, 0xbf, 0xb6, 0x29,\
   0x3f, 0x96}
#define EFI_RNG_ALGORITHM_SP800_90_HMAC_256_GUID    \
  {0xc5149b43, 0xae85, 0x4f53, 0x99, 0x82, 0xb9, 0x43, 0x35, 0xd3,\
   0xa9, 0xe7}
#define EFI_RNG_ALGORITHM_SP800_90_CTR_256_GUID \
  {0x44f0de6e, 0x4d8c, 0x4045, 0xa8, 0xc7, 0x4d, 0xd1, 0x68, 0x85,\
   0x6b, 0x9e}
```

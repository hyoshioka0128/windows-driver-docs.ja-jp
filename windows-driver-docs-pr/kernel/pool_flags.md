---
title: POOL_FLAGS
description: プールメモリの種類、メモリに必要な属性、およびメモリが必要に応じて設定できる属性を示すフラグ。
ms.assetid: 1eaee689-69fb-4720-adbc-b9db5fdc113a
keywords:
- メモリ管理 WDK カーネル、システムによって割り当てられた領域
- システムによって割り当てられた領域 (WDK カーネル)
- システム領域メモリの割り当て
- i/o バッファーメモリの割り当て
- I/o バッファーメモリ割り当て (WDK カーネル)
- バッファーメモリ割り当て (WDK カーネル)
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7e8c4c6a8d5f305af00d5e649de9e14e282c47a2
ms.sourcegitcommit: b481c9513a9ea7f824ecabd1ae18876548032252
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882325"
---
# <a name="pool_flags"></a>POOL_FLAGS

必須およびオプションの属性と共にプールメモリの種類を指定する ULONG64 型の値。 複数のフラグ値は、ビットごとの OR を使用して組み合わせることができます。

```cpp
//
// POOL_FLAG values
//
// Low 32-bits of ULONG64 are for required parameters (allocation fails if they
// cannot be satisfied).
// High 32-bits of ULONG64 is for optional parameters (allocation succeeds if
// they cannot be satisfied or are unrecognized).
//

#define POOL_FLAG_REQUIRED_START          0x0000000000000001UI64
#define POOL_FLAG_USE_QUOTA               0x0000000000000001UI64     // Charge quota
#define POOL_FLAG_UNINITIALIZED           0x0000000000000002UI64     // Don't zero-initialize allocation
#define POOL_FLAG_SESSION                 0x0000000000000004UI64     // Use session specific pool
#define POOL_FLAG_CACHE_ALIGNED           0x0000000000000008UI64     // Cache aligned allocation
#define POOL_FLAG_RESERVED1               0x0000000000000010UI64     // Reserved for system use
#define POOL_FLAG_RAISE_ON_FAILURE        0x0000000000000020UI64     // Raise exception on failure
#define POOL_FLAG_NON_PAGED               0x0000000000000040UI64     // Non paged pool NX
#define POOL_FLAG_NON_PAGED_EXECUTE       0x0000000000000080UI64     // Non paged pool executable
#define POOL_FLAG_PAGED                   0x0000000000000100UI64     // Paged pool
#define POOL_FLAG_RESERVED2               0x0000000000000200UI64     // Reserved for system use
#define POOL_FLAG_RESERVED3               0x0000000000000400UI64     // Reserved for system use
#define POOL_FLAG_REQUIRED_END            0x0000000080000000UI64
#define POOL_FLAG_OPTIONAL_START          0x0000000100000000UI64
#define POOL_FLAG_SPECIAL_POOL            0x0000000100000000UI64     // Make special pool allocation
#define POOL_FLAG_OPTIONAL_END            0x8000000000000000UI64
```

## <a name="required-flags"></a>必須フラグ

プールアロケーターによって、必要なフラグが認識され、満たされる必要があります。 アロケーターがフラグを認識しない場合、またはすべての必須フラグを満たす割り当てを行うことができない場合は、割り当てが失敗します。

|名前|説明|
|-|-|
|POOL_FLAG_USE_QUOTA|このフラグは、最初に i/o 要求を行ったプロセスのコンテキストで要求を満たすためにメモリを割り当てる最上位レベルのドライバーによって渡されます。 下位レベルのドライバーでは、このフラグを指定する必要はありません。|
|POOL_FLAG_UNINITIALIZED|割り当てを初期化せずに残します。 割り当ての内容を決定していません。 ドライバーは、未初期化のメモリを信頼されていない宛先 (ユーザーモード、ネットワーク経由など) にコピーしないように注意する必要があります。|
|POOL_FLAG_SESSION|オペレーティングシステム用に予約されています。|
|POOL_FLAG_CACHE_ALIGNED|キャッシュはプール割り当てをアラインします。 警告: このフラグはベストエフォートとして扱われます。プログラムの正確性のためにキャッシュによって固定された割り当てが必要な場合は使用しないでください。|
|POOL_FLAG_RESERVED1|内部使用のために予約されています。|
|POOL_FLAG_RAISE_ON_FAILURE|割り当てを満たすことができない場合は、例外を発生させます。|
|POOL_FLAG_NON_PAGED|非ページプールで割り当てを行います。|
|POOL_FLAG_NON_PAGED_EXECUTE|ページングされていない実行可能ファイルプールで割り当てを行います。|
|POOL_FLAG_PAGED|ページプールで割り当てを行います。 これは、他のすべてのプラットフォームで x86、実行可能ファイル以外の実行可能ファイルです。|
|POOL_FLAG_RESERVED2|内部使用のために予約されています。|
|POOL_FLAG_RESERVED3|内部使用のために予約されています。|

## <a name="optional-flags"></a>省略可能なフラグ

オプションのフラグは、プールアロケーターさせるによって満たされます。 アロケーターがオプションのフラグを認識しない場合は、無視されます。 アロケーターがオプションのフラグを満たすことができない場合、特定のフラグのセマンティクスによっては成功する場合と失敗する場合があります。

|名前|説明|
|-|-|
|POOL_FLAG_SPECIAL_POOL|(デバッグに使用される) 特別なプールで割り当てを行います。 特別なプールを使用できない場合、アロケーターは通常のプールを使用しようとします。|

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| ---- |:---- |
|ヘッダー|wdm (Wdm、Ntddk、Ntifs、Wudfwdm などを含む) を指定します。|

## <a name="see-also"></a>参照

[**ExAllocatePool2**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2)

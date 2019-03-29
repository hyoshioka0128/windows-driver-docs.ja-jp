---
title: EFI_RNG_SERVICE_BINDING_PROTOCOL
description: ドライバーによって提供される RNG サービスを検索および作成し、複数のドライバーは、基になる RNG サービスを使用できるように、インスタンスを破棄するために使用します。
ms.assetid: 3CAD0FD8-DD26-4D26-A9E9-4B2750985E00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ffb9e550304f102452a6ab2368548b04450310b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573021"
---
# <a name="efirngservicebindingprotocol"></a>EFI\_RNG\_サービス\_バインド\_プロトコル


EFI\_RNG\_サービス\_バインド\_プロトコルを使用して、ドライバーによって提供されるランダムな数の生成 (RNG) サービスを検索して、作成および、EFI のインスタンスを破棄する\_RNG\_プロトコルの複数のドライバーは、基になる RNG サービスを使用できるようにします。

ジェネリックの EFI\_サービス\_バインド\_プロトコルは 2.5.8 および UEFI 仕様の 10.6 のセクションで説明します。 このセクションでは、EFI の固有の情報\_RNG\_サービス\_バインド\_プロトコル。

## <a name="guid"></a>GUID


```cpp
// {E417A4A2-0843-4619-BF11-5CE82AFCFC59}
#define EFI_RNG_SERVICE_BINDING_PROTOCOL_GUID \
  {0xe417a4a2, 0x0843, 0x4619, 0xbf, 0x11, 0x5c, 0xe8, 0x2a, 0xfc, 0xfc, 0x59};
```

## <a name="remarks"></a>コメント


アプリケーションまたは RNG サービスが必要なドライバーは EFI など、プロトコル ハンドラーのサービスのいずれかで使用できる\_ブート\_サービス -&gt;、EFI を公開するデバイスを検索、LocateHandleBuffer()\_RNG\_サービス\_バインド\_プロトコル。 パブリッシュされた efi を搭載した各デバイス\_RNG\_サービス\_バインド\_プロトコルのサポートは、EFI\_RNG\_プロトコルし使用するために使用できるようにします。

EFI に成功した呼び出しの後に\_RNG\_サービス\_バインド\_プロトコル。CreateChild() 関数、子 EFI\_RNG\_プロトコル ドライバーのインスタンスが使用できるようにします。

アプリケーションはすべて、EFI の成功した呼び出しの実行を終了する前に\_RNG\_サービス\_バインド\_プロトコル。CreateChild() 関数は、EFI への呼び出しと一致する必要があります\_RNG\_サービス\_バインド\_プロトコル。DestroyChild() 関数。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 





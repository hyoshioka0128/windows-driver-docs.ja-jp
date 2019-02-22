---
title: '[省略可能]コールバック ルーチンを登録します。'
description: '[省略可能]コールバック ルーチンを登録します。'
ms.assetid: 59d15b37-e31e-45fc-bdb0-fed6f791839c
keywords:
- コールバック ルーチンを登録します。
- コールバック ルーチン WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6a020b27dd40fcabfb4a10d3b1aad20144895d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536435"
---
# <a name="optional-registering-callback-routines"></a>\[省略可能な\]コールバック ルーチンを登録します。


## <span id="ddk_registering_callback_routines_if"></span><span id="DDK_REGISTERING_CALLBACK_ROUTINES_IF"></span>


フィルター ドライバーが呼び出せる[ **IoRegisterFsRegistrationChange** ](https://msdn.microsoft.com/library/windows/hardware/ff548499)ファイル システム ドライバーを呼び出すたびに呼び出されるコールバック ルーチンを登録する[ **IoRegisterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff548494)または[ **IoUnregisterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff548552)を登録または登録解除します。 フィルター ドライバーは、新しいファイル システム、システムを入力し、選択にアタッチするかどうかを確認できるように、このコールバック ルーチンを登録します。

**注**  ファイル システム フィルター ドライバーは呼び出す必要がありますしない[ **IoRegisterFileSystem** ](https://msdn.microsoft.com/library/windows/hardware/ff548494)または[ **IoUnregisterFileSystem**](https://msdn.microsoft.com/library/windows/hardware/ff548552). これらのルーチンは、ファイル システム専用です。

 

(たとえば、ユーザー モード アプリケーション) を明示的に指定されている場合にのみ、ボリュームに接続されているフィルター ドライバーは呼び出さないでください[ **IoRegisterFsRegistrationChange**](https://msdn.microsoft.com/library/windows/hardware/ff548499)します。 ただし、このルーチンを使用するフィルターがそのボリュームがマウントされている後すぐに、特定のボリュームにアタッチする機能を持つことに注意してください。 このルーチンを使用しても、ボリュームのデバイス オブジェクトに直接、フィルターをアタッチすることとは限りません。 このようなフィルターを確認する前に (そして下) にアタッチしますすべてのフィルターのみ、ファイル システム ボリューム デバイスの現在のスタックの上部にあるフィルターをアタッチできるため、代わりに、ユーザー モード アプリケーションからのコマンドの待機をします。

 

 





---
title: 保護モードのアクティブ化
description: 保護モードのアクティブ化
ms.assetid: bb7cd081-f032-4af4-bb4d-efa96917088b
keywords:
- 保護モードをアクティブ化する方法
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc2807ce8c10d103b59eb6818cb985024fbb0976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354414"
---
# <a name="activating-secure-mode"></a>保護モードのアクティブ化


## <span id="ddk_activating_secure_mode_dbg"></span><span id="DDK_ACTIVATING_SECURE_MODE_DBG"></span>


セキュリティで保護されたモードでは、カーネル モードのデバッグに使用できるのみです。 これは、デバッガーのコマンドラインで、またはデバッガーが完全に休止状態と、まだサーバーとして使用されていない - デバッグ セッションの開始前にアクティブ化する必要があります。

保護モードをアクティブ化するには、次のメソッドのいずれかを使用します。

-   **-セキュリティで保護された**[コマンド ライン オプション](command-line-options.md)

-   [ **.Secure 1** ](-secure--activate-secure-mode-.md)コマンド

-   [ **.Symopt + 0x40000** ](-symopt--set-symbol-options-.md)コマンド

セキュリティで保護モードで使用しているかどうかを調べる必要があり、既存のカーネル デバッグ セッションをした場合、 [ **.secure** ](-secure--activate-secure-mode-.md)引数なしでコマンド。 保護モードの現在の状態が通知されます。

保護モードを有効にしたら、オフにすることはできません。 デバッグ セッションを終了してもオフにできないことです。 セキュリティで保護されたモードでは、デバッガー自体が実行されている限り永続化します。

 

 






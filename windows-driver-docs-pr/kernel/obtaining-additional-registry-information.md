---
title: 追加のレジストリ情報の取得
description: 追加のレジストリ情報の取得
ms.assetid: 989acf63-3bb1-4d9a-a7a8-3eea1e2bc68a
keywords:
- レジストリの呼び出しの WDK カーネル、追加の情報を取得するフィルター処理
- レジストリのフィルター ドライバー WDK カーネルでは、追加の情報を取得するには
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ec1cf6ec13abbb838da16542d3ab614e231ae3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384938"
---
# <a name="obtaining-additional-registry-information"></a>追加のレジストリ情報の取得


Windows Vista およびそれ以降のオペレーティング システム バージョンで実行されるドライバーをフィルタ リング レジストリは、レジストリの操作に関する追加情報を取得できます。

-   オブジェクト識別子と名

    [ **CmCallbackGetKeyObjectIDEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmcallbackgetkeyobjectidex)ルーチンは、レジストリ キー識別子とオブジェクトの名前を指定したレジストリ キー オブジェクトに関連付けられたを取得します。

-   トランザクション オブジェクト

    [ **CmGetBoundTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmgetboundtransaction)ルーチンが表すトランザクション オブジェクトへのポインターを返します、[トランザクション](using-kernel-transaction-manager.md)あるレジストリ キーに関連付けられている場合、オブジェクト。

-   バージョン情報

    [ **CmGetCallbackVersion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmgetcallbackversion)ルーチンは、configuration manager のレジストリのコールバック機能の現在のバージョンのメジャーおよびマイナー バージョン番号を取得します。

 

 





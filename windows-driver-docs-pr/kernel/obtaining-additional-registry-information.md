---
title: 追加のレジストリ情報を取得します。
description: 追加のレジストリ情報を取得します。
ms.assetid: 989acf63-3bb1-4d9a-a7a8-3eea1e2bc68a
keywords:
- レジストリの呼び出しの WDK カーネル、追加の情報を取得するフィルター処理
- レジストリのフィルター ドライバー WDK カーネルでは、追加の情報を取得するには
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa93162f0f9e189e34d63a2003b9fe8d0de15792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527569"
---
# <a name="obtaining-additional-registry-information"></a>追加のレジストリ情報を取得します。


Windows Vista およびそれ以降のオペレーティング システム バージョンで実行されるドライバーをフィルタ リング レジストリは、レジストリの操作に関する追加情報を取得できます。

-   オブジェクト識別子と名

    [ **CmCallbackGetKeyObjectIDEx** ](https://msdn.microsoft.com/library/windows/hardware/jj215789)ルーチンは、レジストリ キー識別子とオブジェクトの名前を指定したレジストリ キー オブジェクトに関連付けられたを取得します。

-   トランザクション オブジェクト

    [ **CmGetBoundTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff541905)ルーチンが表すトランザクション オブジェクトへのポインターを返します、[トランザクション](using-kernel-transaction-manager.md)あるレジストリ キーに関連付けられている場合、オブジェクト。

-   バージョン情報

    [ **CmGetCallbackVersion** ](https://msdn.microsoft.com/library/windows/hardware/ff541912)ルーチンは、configuration manager のレジストリのコールバック機能の現在のバージョンのメジャーおよびマイナー バージョン番号を取得します。

 

 





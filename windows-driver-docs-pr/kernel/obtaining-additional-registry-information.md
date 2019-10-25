---
title: 追加のレジストリ情報の取得
description: 追加のレジストリ情報の取得
ms.assetid: 989acf63-3bb1-4d9a-a7a8-3eea1e2bc68a
keywords:
- レジストリをフィルター処理することで、WDK カーネルを呼び出し、追加情報を取得します。
- レジストリフィルタリングドライバー WDK カーネル、取得する追加情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c09a7547bb37ccb81948d6f0de13c8c00d8333e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838527"
---
# <a name="obtaining-additional-registry-information"></a>追加のレジストリ情報の取得


Windows Vista 以降のバージョンのオペレーティングシステムで実行されるレジストリフィルタリングドライバーは、次のレジストリ操作に関する追加情報を取得できます。

-   オブジェクトの識別子と名前

    [**Cm/Getkeywhere-object Tidex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmcallbackgetkeyobjectidex)ルーチンは、指定されたレジストリキーオブジェクトに関連付けられているレジストリキー識別子とオブジェクト名を取得します。

-   トランザクションオブジェクト

    [**Cmgetboundtransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetboundtransaction)ルーチンは、レジストリキーオブジェクトに関連付けられている[トランザクション](using-kernel-transaction-manager.md)(存在する場合) を表すトランザクションオブジェクトへのポインターを返します。

-   バージョン情報

    [**Cmgetcallback バージョン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmgetcallbackversion)のルーチンは、現在のバージョンの configuration manager のレジストリコールバック機能のメジャーバージョン番号とマイナーバージョン番号を取得します。

 

 





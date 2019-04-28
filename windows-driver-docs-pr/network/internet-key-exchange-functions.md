---
title: インターネット キー交換関数
description: このセクションでは、インターネット キー交換機能について説明します。
ms.assetid: 993a6db0-018c-4529-bccc-46b522e74c79
keywords:
- ネットワーク ドライバーのインターネット キー交換関数
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67173175b6e885c05071e2d021b47b9677f89b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380604"
---
# <a name="internet-key-exchange-functions"></a>インターネット キー交換関数

次の関数のセマンティクスは、正確に同じ戻り値の型は、Win32 エラー コードではなく、NTSTATUS コードがユーザー モード アプリケーションから呼び出されたときに、コールアウト ドライバーとしてから呼び出された場合です。 これらの各関数については、次を参照してください。、 [Windows フィルタ リング プラットフォーム](https://go.microsoft.com/fwlink/p/?linkid=210226)、Microsoft Windows SDK のドキュメント セクション。

これらの関数の呼び出し元は、IRQL で実行する必要があります PASSIVE_LEVEL を = です。

- IkeextGetStatistics0
- IkeextSaCreateEnumHandle0
- IkeextSaDbGetSecurityInfo0
- IkeextSaDbSetSecurityInfo0
- IkeextSaDeleteById0
- IkeextSaDestroyEnumHandle0
- IkeextSaEnum0
- IkeextSaGetById0


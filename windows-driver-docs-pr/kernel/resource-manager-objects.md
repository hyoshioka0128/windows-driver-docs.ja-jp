---
title: リソース マネージャー オブジェクト
description: リソース マネージャー オブジェクト
ms.assetid: b44f2035-ee9f-453b-b12d-89ca36a8b280
keywords:
- リソースマネージャー WDK KTM、オブジェクト
- リソースマネージャーの WDK KTM
- リソースマネージャー WDK KTM、ルーチン
- カーネルトランザクションマネージャー WDK、リソースマネージャー
- KTM WDK、リソースマネージャー
- resource manager オブジェクト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a94ba8f32324703715e2c4393c6ec332b0e7f50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836419"
---
# <a name="resource-manager-objects"></a>リソース マネージャー オブジェクト


*Resource manager オブジェクト*は、リソースマネージャーを表します。 各リソースマネージャーは、 [**Zwcreateresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)を呼び出して、それ自体を KTM に登録する必要があります。

KTM は、カーネルモードのリソースマネージャーが呼び出すことができる[resource manager オブジェクトルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のセットを提供します。 また、KTM は、ユーザーモードアプリケーションが呼び出すことができる同様のユーザーモードルーチンのセットも提供します。 ユーザーモードルーチンの詳細については、「Microsoft Windows SDK」を参照してください。

リソースマネージャーが**Zwcreateresourcemanager**を呼び出すと、KTM によって resource manager オブジェクトが作成されます。

[Tp コンポーネント](understanding-tps-components.md)は、 [**Zwopenresourcemanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)を呼び出して、resource manager オブジェクトへの追加ハンドルを開くことができます。 ただし、ほとんどの TPS デザインでは、追加の開いているハンドルは必要ありません。

リソースマネージャーは、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出すことによって、リソースマネージャーオブジェクトのハンドルを閉じます。 最後のハンドルが閉じていても、まだコミットされていないトランザクションにリソースマネージャーが参加している場合、KTM は\_トランザクションを送信して、関連付けられているトランザクションのすべてのリソースマネージャーにロールバック通知\_通知します。参加させることができます。

最後のハンドルが閉じられ、KTM によってオブジェクトへのすべての参照が解放された後、オペレーティングシステムによってオブジェクトが削除されます。

 

 





---
title: トランザクション マネージャー オブジェクト
description: トランザクション マネージャー オブジェクト
ms.assetid: af53cda4-e2ab-47df-9311-a4da2a2ee08d
keywords:
- ログストリーム WDK KTM、作成
- トランザクションマネージャーオブジェクトの仮想クロック値 WDK KTM
- カーネルトランザクションマネージャー WDK、トランザクションマネージャー
- トランザクションマネージャーオブジェクト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1443500d56b756d1415ed0fee1071f8b8a56c25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838386"
---
# <a name="transaction-manager-objects"></a>トランザクション マネージャー オブジェクト


*トランザクションマネージャーオブジェクト*の主な目的は、KTM がトランザクションに関する状態情報を記録するために使用する[共通ログファイルシステム](using-common-log-file-system.md)(CLFS) ログストリームを作成して維持することです。

また、トランザクションマネージャーオブジェクトには、KTM によって保持され、オブジェクトのログストリーム内の情報をシーケンス処理するために使用される[仮想クロック値](using-virtual-clock-values.md)も含まれます。

KTM には、カーネルモードの[tp コンポーネント](understanding-tps-components.md)が呼び出すことのできる一連の[トランザクションマネージャーオブジェクトルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)が用意されています。 また、KTM は、ユーザーモードアプリケーションが呼び出すことができる同様のユーザーモードルーチンのセットも提供します。 ユーザーモードルーチンの詳細については、「Microsoft Windows SDK」を参照してください。

リソースマネージャーが[**Zwcreatetransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)を呼び出すときに、KTM はトランザクションマネージャーオブジェクトを作成します。 通常、TP 内の各リソースマネージャーは、トランザクションマネージャーオブジェクトを作成します。 ただし、複数のリソースマネージャーが1つのトランザクションマネージャーオブジェクトを共有する TP を設計することもできます。

TP コンポーネントは、 [**Zwopentransactionmanager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)を呼び出すことによって、既存のトランザクションマネージャーオブジェクトへの追加ハンドルを開くことができます。 たとえば、1つのトランザクションマネージャーオブジェクトを共有する複数のリソースマネージャーが TP に存在する場合、1つのリソースマネージャーが**Zwcreatetransactionmanager**を呼び出し、オブジェクト GUID を他のリソースマネージャーに渡して、を呼び出す**ことができるようにします。ZwOpenTransactionManager**。

リソースマネージャーは、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、トランザクションマネージャーオブジェクトのハンドルを閉じます。

最後のハンドルが閉じられ、KTM によってオブジェクトへのすべての参照が解放された後、オペレーティングシステムによってオブジェクトが削除されます。

 

 





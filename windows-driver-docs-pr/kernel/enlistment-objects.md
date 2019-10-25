---
title: 登録オブジェクト
description: 登録オブジェクト
ms.assetid: 80e61475-4bb7-4eaa-b9f1-ff95eac9bc77
keywords:
- 、WDK KTM の参加
- 、WDK KTM、オブジェクトの参加
- リソースマネージャー WDK KTM、参加リストの作成
- カーネルトランザクションマネージャー WDK、参加リスト
- KTM WDK、参加リスト
- 参加オブジェクト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d33be4b8366fb9adc7f90b73ce443278c53b01d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836745"
---
# <a name="enlistment-objects"></a>登録オブジェクト


*参加オブジェクト*は、リソースマネージャーによるトランザクションへの[*参加*](transaction-processing-terms.md#ktm-term-enlistment)を表します。 リソースマネージャーは、トランザクションのイベントに関する通知を受信する前に、 [**Zwcreateenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)を呼び出して、トランザクションへの参加を作成する必要があります。

KTM には、カーネルモードのリソースマネージャーが呼び出すことができる[参加オブジェクトルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のセットが用意されています。 また、KTM は、ユーザーモードアプリケーションが呼び出すことができる同様のユーザーモードルーチンのセットも提供します。 ユーザーモードルーチンの詳細については、「Microsoft Windows SDK」を参照してください。

リソースマネージャーが**Zwcreateenlistment**を呼び出して、リソースマネージャーが受信した (通常はトランザクションクライアントからの) トランザクションに参加する場合、KTM は参加オブジェクトを作成します。

[Tp コンポーネント](understanding-tps-components.md)は、 [**zwopenenlistment リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenenlistment)を呼び出して、参加オブジェクトに対する追加ハンドルを開くことができます。 ただし、ほとんどの TPS デザインでは、追加の開いているハンドルは必要ありません。

リソースマネージャーは、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、そのハンドルを参加オブジェクトに対して閉じます。 関連付けられているトランザクションオブジェクトがコミットされる前に最後のハンドルが閉じられた場合、KTM はトランザクションを送信して、トランザクションの参加リストを持つすべてのリソースマネージャーに\_ロールバック通知を通知\_ます。

最後のハンドルが閉じられ、KTM によってオブジェクトへのすべての参照が解放された後、オペレーティングシステムによってオブジェクトが削除されます。

 

 





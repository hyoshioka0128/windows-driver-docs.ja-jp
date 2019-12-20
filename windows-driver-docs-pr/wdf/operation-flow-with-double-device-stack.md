---
title: ダブル デバイス スタックでの操作フロー
description: ダブル デバイス スタックでの操作フロー
ms.assetid: a717b9c0-b24a-4347-8b0a-254a17238b5f
keywords:
- 操作フロー WDK UMDF
- I/o 要求 WDK UMDF、操作フロー
- 要求の処理 WDK UMDF、操作フロー
- ダブルデバイススタックフロー WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaa439033553356082f5b8bf4f670151e6c56988
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210878"
---
# <a name="operation-flow-with-double-device-stack"></a>ダブル デバイス スタックでの操作フロー


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次の図は、2つのデバイススタックで、UMDF フィルターと機能ドライバーの間で発生する操作の流れを示しています。

![umdf フィルタードライバーおよび umdf 関数ドライバーの umdf i/o 呼び出しシーケンス](images/umdfflow2.gif)

アプリケーションによって開始されるすべての i/o は、前の図にはこのような状況が示されていませんが、「UMDF」セクション[のアーキテクチャ](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))の図に示すように、カーネルモード経由でルーティングさ**れる   ます**。

 

UMDF フィルターおよび関数ドライバーは、読み取り要求に関連付けられているファイルに関する情報が必要な場合に、 [**IWDFIoRequest:: GetCreateParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)メソッドも呼び出すことができます。 UMDF フィルターおよび関数ドライバーは、読み取り要求に関する詳細な情報が必要な場合に、 [**IWDFIoRequest:: GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)メソッドも呼び出すことができます。

UMDF 機能ドライバーは、 [**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドを呼び出して、読み取り操作で実行されることをフィルタードライバーに通知します。 また、読み取り要求を完了するためにより多くの情報が必要な場合は、UMDF filter ドライバーで[IWDFIoRequestCompletionParams](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequestcompletionparams)インターフェイスのメソッドを呼び出すこともできます。 UMDF フィルタードライバーは、読み取り操作が完了したことを通知するために、 **complete**または**completewithinformation**を呼び出します。その後、アプリケーションは読み取りデータにアクセスできます。

 

 






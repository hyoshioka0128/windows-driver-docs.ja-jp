---
title: フィルター モジュール状態表示
description: フィルター モジュール状態表示
ms.assetid: b39c6cda-dac7-4538-8ea6-513a52601b1f
keywords:
- フィルター モジュールの WDK ネットワー キング、状態インジケーター
- フィルター ドライバー WDK ネットワー キング、状態インジケーター
- NDIS フィルター ドライバー WDK、状態インジケーター
- 状態インジケーターの WDK ネットワー キング、フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 690e821a56e75e7a8ae736fa58032bf26c801c74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350028"
---
# <a name="filter-module-status-indications"></a>フィルター モジュール状態表示





フィルター ドライバーを指定できます、 [ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973) NDIS が、基になるドライバーの状態を報告したときに呼び出す関数です。 フィルター ドライバーは、状態インジケーターを開始することもできます。

次の図は、フィルター選択された状態を示す値を示します。

![フィルター選択された状態を示す値を示す図](images/statusfilter.png)

NDIS フィルター ドライバーを呼び出す[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)関数は、状態を示す値の関数を呼び出して、基になるドライバーから ([**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)または[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824))。 ミニポート ドライバーからの状態を示す方法の詳細については、次を参照してください。[アダプター状態のインジケーター](miniport-adapter-status-indications.md)します。

フィルター ドライバーは呼び出し**NdisFIndicateStatus**でその[ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)ドライバーに関連する、フィルター選択された状態を示す値を渡すの関数。 フィルター ドライバーは、状態インジケーターをフィルター処理できます (呼び出さなかったことで[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824)) を呼び出す前に、指定されたステータスを変更または**NdisFIndicateStatus**します。

状態インジケーターを発信するには、フィルター ドライバー呼び出し[ **NdisFIndicateStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff561824)を事前に呼び出さずに[ *FilterStatus*](https://msdn.microsoft.com/library/windows/hardware/ff549973)します。

この場合、フィルター ドライバーを設定する必要があります、 **SourceHandle**に渡される NDIS ハンドルへのメンバー、 *NdisFilterHandle*のパラメーター、 [ *FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)関数。 状態の表示が OID 要求に関連付けられている場合は、フィルター ドライバーを設定できます、 **DestinationHandle**と**RequestId**その NDIS は、特定のプロトコルを状態を示す値を提供できるように、メンバーバインディング。

フィルター ドライバーを呼び出してから[ **NdisFIndicateStatus**](https://msdn.microsoft.com/library/windows/hardware/ff561824)、NDIS ステータス関数を呼び出します ([**ProtocolStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570270)または*FilterStatus*) [次へ] の上にあるドライバーの。

 

 






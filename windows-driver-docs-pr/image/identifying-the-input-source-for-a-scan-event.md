---
title: スキャン イベントの入力ソースの識別
description: スキャン イベントの入力ソースの識別
ms.assetid: aaa0bbf4-6866-45d7-8150-c6a74d6c46c1
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: abb2835d5953f464874902b91bb7187d84ff99bf
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223557"
---
# <a name="identifying-the-input-source-for-a-scan-event"></a>スキャン イベントの入力ソースの識別

*プッシュスキャン*操作は、ユーザーがデスクトップコンピューターで実行されている wia アプリケーションのユーザーインターフェイスからではなく、wia スキャナーデバイスから開始するスキャン操作です。 ユーザーがデバイスの [開始-スキャン] ボタンを押すと、アプリケーションは、ユーザーがスキャン操作を要求したことを通知するスキャンイベントを受け取ります。 このイベントに応答して、アプリケーションは次の2つの方法のいずれかでプッシュスキャン操作を実行できます。

- デバイスで[自動構成スキャン](auto-configured-scanning.md)がサポートされている場合、アプリケーションは、[[自動] 項目](auto-item.md)からのデータ転送を要求して、現在選択されている入力ソース (フラット、自動ドキュメントフィーダー、またはフィルムスキャンアダプター) からイメージを取得することができます。 応答として、デバイスはスキャンの設定を自動的に構成します (これは、「[自動項目でサポートされる WIA プロパティ](wia-properties-supported-by-an-auto-item.md)」で説明されている、アプリケーションによってのみ構成できるいくつかのプロパティを除く)、その後、イメージを取得します。

- アプリケーションでは、プログラムの直接制御の下でスキャン操作を実行できます。 まず、アプリケーションは、現在選択されている入力ソースを表す WIA 項目 (フラットアイテム、フィーダー項目、またはフィルム項目) のプロパティを構成します。 次に、アプリケーションはこの項目からのデータ転送を要求することによってイメージを取得します。

WIA 項目の詳細については、「 [Wia 項目のカテゴリ](wia-item-categories.md)」を参照してください。

スキャンイベントが発生すると、アプリケーションは、イベントの性質を指定するために、WIA イベント識別子 (GUID 値) を含む通知を受信します。 WIA ミニドライバーは、カスタムの WIA イベント識別子 GUID をイベントに割り当てることができます。また、ミニドライバーは、 \_ \_ \_ ヘッダーファイル*Wiadef*で定義されている wia イベントスキャン*XXX* GUID 定数の1つを使用できます。 これらの定数の詳細については、「 [WIA イベント識別子](https://docs.microsoft.com/windows/win32/wia/-wia-wia-event-identifiers)」を参照してください。

スキャンイベントの WIA イベント識別子では、イベントに関する情報が提供されますが、スキャン操作に使用する入力ソースは識別されません。 自動構成されたスキャンの場合、アプリケーションはこの情報を必要としません。 ただし、プログラムの直接制御でスキャンを実行するには、使用する入力ソースをアプリケーションが認識している必要があります。 デバイスに複数の入力ソースがあり、ユーザーがアプリケーションのユーザーインターフェイスではなくデバイスから入力ソースを選択できる場合は、アプリケーションにデバイスからこの情報を取得する方法が必要です。 デバイスから入力ソースを選択する場合、ユーザーは、(デバイスの前面にあるボタンを押すことによって) 明示的にソースを選択するか、または暗黙的に (たとえば、デバイスのフィーダーにドキュメントを挿入することによって) 選択できます。

スキャンイベントが発生すると、デバイスがこのプロパティをサポートしている場合、アプリケーションは WIA スキャナーデバイスの WIA \_ DPS scan AVAILABLE ITEM プロパティを照会して、 \_ 選択された \_ \_ 入力ソースを識別できます。 WIA \_ DPS \_ SCAN \_ AVAILABLE \_ 項目は、デバイスの wia 項目ツリーのルート項目のオプションのプロパティです。 このプロパティの詳細については、「 [**WIA \_ DPS \_ SCAN \_ AVAILABLE \_ ITEM**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-scan-available-item)」を参照してください。

WSD scan クラスドライバーは、 \_ \_ \_ \_ カスタムドライバー拡張機能としてではなく、前の段落で説明したように、WIA DPS scan AVAILABLE ITEM プロパティを標準ドライバー機能として実装します。 WSD scan クラスドライバーの詳細については、「 [WIA With Web Services For Devices](wia-with-web-services-for-devices.md)」を参照してください。 スキャナーの WDP の詳細については、「 [Web Services For Devices Scan Service Schema](https://docs.microsoft.com/windows-hardware/drivers/image/scan-service--ws-scan--schema)」を参照してください。

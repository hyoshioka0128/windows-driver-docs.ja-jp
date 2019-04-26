---
title: IHV ポート モニターの自動構成
description: IHV ポート モニターの自動構成
ms.assetid: c41c8502-902a-448c-8f96-fb196e68ee6e
keywords:
- IHV ポート モニターの自動構成の WDK プリンター
- 自動構成の WDK プリンター、IHV ポート モニター
- プリンターの自動構成の WDK プリンター、IHV ポート モニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2591eaa8bbd8b465a65e07d1911ba462d8d4fe88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350751"
---
# <a name="autoconfiguration-in-an-ihv-port-monitor"></a>IHV ポート モニターの自動構成


IHV ポート モニターを開発しようとしています。 ユーザーは、自動構成をサポートするように設計する必要があります。 IHV のポート モニターでの自動構成のサポートを提供するには、次のガイドラインに従います。

-   実装、 [ **SendRecvBidiDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562071)関数では、この関数のアドレスに置き、 **pfnSendRecvBidiDataFromPort**のメンバー、 [**MONITOR2** ](https://msdn.microsoft.com/library/windows/hardware/ff557532)構造体。

-   サポート、[双方向通信スキーマ](https://msdn.microsoft.com/library/windows/hardware/ff545175)します。

-   双方向の通知をサポートします。

IHV は、インボックス サポートのための十分な場合は、ポート モニターを開発する必要はありません。 (詳細については、次を参照してください[自動構成のインボックス サポート](in-box-support-for-autoconfiguration.md)。)。組み込みのサポートが、標準の TCP/IP ポート モニターと、Web Services for Devices (WSD) ポート モニターに対してのみ提供されることに注意します。 Ihv 向けのローカル プリンターの自動構成は、ポート モニターを提供する必要がありますを使用するユーザー。

 

 





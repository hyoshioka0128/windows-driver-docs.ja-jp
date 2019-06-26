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
ms.openlocfilehash: b52d57bef2f3bf0171a564a0d2123ea751a97986
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370465"
---
# <a name="autoconfiguration-in-an-ihv-port-monitor"></a>IHV ポート モニターの自動構成


IHV ポート モニターを開発しようとしています。 ユーザーは、自動構成をサポートするように設計する必要があります。 IHV のポート モニターでの自動構成のサポートを提供するには、次のガイドラインに従います。

-   実装、 [ **SendRecvBidiDataFromPort** ](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))関数では、この関数のアドレスに置き、 **pfnSendRecvBidiDataFromPort**のメンバー、 [**MONITOR2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_monitor2)構造体。

-   サポート、[双方向通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)します。

-   双方向の通知をサポートします。

IHV は、インボックス サポートのための十分な場合は、ポート モニターを開発する必要はありません。 (詳細については、次を参照してください[自動構成のインボックス サポート](in-box-support-for-autoconfiguration.md)。)。組み込みのサポートが、標準の TCP/IP ポート モニターと、Web Services for Devices (WSD) ポート モニターに対してのみ提供されることに注意します。 Ihv 向けのローカル プリンターの自動構成は、ポート モニターを提供する必要がありますを使用するユーザー。

 

 





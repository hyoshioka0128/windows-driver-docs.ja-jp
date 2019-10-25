---
title: IHV ポート モニターの自動構成
description: IHV ポート モニターの自動構成
ms.assetid: c41c8502-902a-448c-8f96-fb196e68ee6e
keywords:
- IHV ポートモニタ自動構成 WDK プリンタ
- 自動構成 WDK プリンター、IHV ポートモニター
- プリンター自動構成 WDK プリンター、IHV ポートモニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7687f219b909a9f0eef1ad187384eddd60b24eef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842835"
---
# <a name="autoconfiguration-in-an-ihv-port-monitor"></a>IHV ポート モニターの自動構成


ポートモニターの開発を予定している IHV は、自動構成をサポートするようにそれを設計する必要があります。 IHV ポートモニターで自動構成のサポートを提供するには、次のガイドラインに従います。

-   [**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))関数を実装し、この関数のアドレスを[**MONITOR2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitor2)構造体の**pfnSendRecvBidiDataFromPort**メンバーに配置します。

-   [Bidi 通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)をサポートします。

-   Bidi 通知をサポートします。

インボックスサポートで十分な場合は、ポートモニターの開発に IHV が必要ありません。 (詳細については、「[自動構成のインボックスサポート](in-box-support-for-autoconfiguration.md)」を参照してください)。インボックスサポートは、標準の TCP/IP ポートモニターと Web Services for Devices (WSD) ポートモニターに対してのみ提供されることに注意してください。 ローカルプリンターの自動構成を提供する Ihv は、ポートモニターを提供する必要があります。

 

 





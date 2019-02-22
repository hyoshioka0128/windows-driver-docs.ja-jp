---
title: ユーザー モードの Power サービス
description: ユーザー モードの Power サービス
ms.assetid: 57f3affd-18cc-440c-ba18-9ba89fd3c84f
keywords:
- 使用状況測定予算の WDK では、ユーザー モードの Power サービスの電源します。
- ユーザー モード Power サービス WDK 電源メーター
- UMPS WDK 電源メーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d03f1e10a009d8c169b71457287a6fce2deb83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548911"
---
# <a name="user-mode-power-service"></a>ユーザー モードの Power サービス


ユーザー モード Power サービス (UMPS) 以降では、Windows 7 および Windows Server 2008 R2 は、ユーザー モード サービスおよびアプリケーションに電源管理のすべての側面のインターフェイスを提供します。 このインターフェイスには、電力使用状況測定と電源関連の情報の予算 (PMB) インフラストラクチャのサポートが含まれています。 この情報は、電源管理とレポートの Windows パフォーマンス モニター (PerfMon) などのアプリケーションによって使用されます。

UMPS は、PMB WMI クラスのセットを使用して PMB 情報へのアクセスを提供します。 これらの WMI クラスは、Distributed Management Task Force (DMTF) の電源プロファイルのバージョン 1.1.0 に準拠します。 詳細については、次を参照してください。、 [DMTF の電源を提供するプロファイル](https://go.microsoft.com/fwlink/p/?linkid=145048)します。

PMB WMI クラスは、次のサポートを提供します。

-   現在の電力使用状況測定と電源メーター デバイスの予算情報のクエリ。

-   メーターの電力のしきい値や予算を超えたときに、コールバック通知を登録します。

UPMS PMB WMI 要求にサービスを PMI でサポートされている I/O 要求パケット (Irp) を通じて電源メーター インターフェイス (PMI) を呼び出します。 PMI の詳細については、次を参照してください。[電力メーター インターフェイス](power-meter-interface.md)します。

PMB WMI クラスに関する詳細については、Windows SDK のドキュメントを参照してください。

 

 





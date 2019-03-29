---
title: ACPI IPMI 操作領域
description: ACPI IPMI 操作領域
ms.assetid: fb953ee1-2628-4cd1-a2d3-a725cf59cc9f
keywords:
- 使用状況の測定と予算の WDK、ACPI IPMI 営業地域を電源します。
- ACPI IPMI 営業地域 WDK 電源メーター
- IPMI WDK 電源メーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9439156eabf8452f21fc7aa0a26056bf439a2b85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581145"
---
# <a name="acpi-ipmi-operation-region"></a>ACPI IPMI 操作領域


多くのシステムでは、Intelligent Platform Management Interface (IPMI) を使用してサービス プロセッサやベースボード管理コント ローラー (BMC) と通信します。

オペレーティング システム以降 Windows 7 および Windows Server 2008 R2 では、サービスのプロセッサまたは Bmc に IPMI アクセス標準化された ACPI IPMI 操作領域を提供します。 これはデバイスを ACPI 機械語 (AML)、IPMI のデータにアクセスできるようにし、ACPI のファームウェアを使用して IPMI 要求を発行するためのハードウェア プラットフォームを有効にします。

オペレーティング システムでは、ACPI IPMI 操作の領域をサポートする IPMI ドライバーを提供します。 ドライバーはサービス IPMI 要求は、キーボード コント ローラーのスタイル (KCS) プロトコルを使用して行う必要があります。

詳細についてを参照してください、 [IPMI version 2.0 仕様](https://go.microsoft.com/fwlink/p/?linkid=69485)します。

 

 





---
title: Windows Hardware Error Architecture の新情報
description: Windows Hardware Error Architecture の新情報
ms.assetid: 258dca19-3988-4fab-bc9f-a93035cbbd0e
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK、新しい情報
- WHEA WDK、新しい情報
- ハードウェア エラー WDK WHEA、新しい情報
- エラー WDK WHEA、WHEA に関する新しい情報
- ソース情報 WDK WHEA では、新しい
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab4920ac3ad03f16e9485d620c00083a0d541107
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386457"
---
# <a name="new-information-for-windows-hardware-error-architecture"></a>Windows Hardware Error Architecture の新情報


このセクションでは、主要な追加機能と改訂 Windows ハードウェア エラー アーキテクチャ (WHEA) をまとめたものです。 このセクションの各トピックでは、WHEA に Windows オペレーティング システムのリリースごとに行われた変更について説明します。

ここでは、次のトピックについて説明します。

[Windows Server 2008 と Windows Vista SP1 の WHEA 変更](whea-changes-for-windows-server-2008-and-windows-vista-sp1.md)

[Windows 7 の WHEA の変更](whea-changes-for-windows-7.md)

## <a name="new-whea-changes-for-windows8"></a>(*新しい*) for Windows 8 の WHEA の変更


Windows 8 以降、次の変更が行われた Windows ハードウェア エラー アーキテクチャ (WHEA) に

-   新しい WMI プロバイダー クラス[ **WHEAPolicyManagementMethods**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)します。
-   WHEA のポリシーを指定できますいずれかが管理されている[ **WHEAPolicyManagementMethods** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)または WHEA Powershell モジュールを使用します。 これらのモードのいずれかで、ポリシーが更新され、ポリシーの値が直ちに有効にします。
-   WHEA の WMI メソッド[ **WHEAErrorSourceMethods::SetErrorSourceInfoRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)は非推奨とされます。

 

 





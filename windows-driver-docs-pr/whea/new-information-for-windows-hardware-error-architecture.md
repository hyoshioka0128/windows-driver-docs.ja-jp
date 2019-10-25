---
title: Windows Hardware Error Architecture の新情報
description: Windows Hardware Error Architecture の新情報
ms.assetid: 258dca19-3988-4fab-bc9f-a93035cbbd0e
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、新しい情報
- WHEA WDK、新しい情報
- ハードウェアエラー WDK WHEA、新しい情報
- エラー WDK WHEA、WHEA に関する新しい情報
- ソース情報 WDK WHEA、新規
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 640ea8e9cd6b6733b2f2b51283f5981f03af7bcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843553"
---
# <a name="new-information-for-windows-hardware-error-architecture"></a>Windows Hardware Error Architecture の新情報


このセクションでは、Windows ハードウェアエラーアーキテクチャ (WHEA) の主な追加とリビジョンについて説明します。 このセクションの各トピックでは、Windows オペレーティングシステムのリリースごとに、WHEA に加えられた変更について説明します。

ここでは、次のトピックについて説明します。

[Windows Server 2008 および Windows Vista SP1 の WHEA 変更](whea-changes-for-windows-server-2008-and-windows-vista-sp1.md)

[Windows 7 の WHEA の変更点](whea-changes-for-windows-7.md)

## <a name="new-whea-changes-for-windows8"></a>(*新規*)Windows 8 の WHEA の変更点


Windows 8 以降では、Windows ハードウェアエラーアーキテクチャ (WHEA) に対して次の変更が加えられました。

-   新しい WMI プロバイダークラス[**WHEAPolicyManagementMethods**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)。
-   WHEA ポリシーは、 [**WHEAPolicyManagementMethods**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)または whea Powershell モジュールを使用して管理できます。 これらのモードのいずれかを使用してポリシーを更新した場合、ポリシーの値は直ちに有効になります。
-   WHEA WMI メソッド[**WHEAErrorSourceMethods:: SetErrorSourceInfoRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)は非推奨とされます。

 

 





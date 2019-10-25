---
title: 推奨される VidPN トポロジへのシステム コール
description: 推奨される VidPN トポロジへのシステム コール
ms.assetid: cc23be93-be31-4069-960c-268a8b151063
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba2a559dabddfb1a65c13c207d29cbd57397c078
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829333"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>推奨される VidPN トポロジへのシステム コール


Windows 7 を実行しているコンピューターでは、表示モードマネージャー (DMM) によって、CCD データベースの VidPN 履歴データを使用して適用する適切な VidPN トポロジが決定されます。 DMM では、Windows Vista と同じように、前回正常起動時のトポロジに基づいて、VidPN トポロジが決定されなくなりました。 その結果、Windows 7 では、DMM は[**DxgkDdiRecommendVidPnTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)関数を呼び出しません。

Windows Vista とそのサービスパックでは、DMM は引き続き*DxgkDdiRecommendVidPnTopology*を呼び出して、推奨されている機能的な VidPN トポロジをドライバーが提供するように要求します。

 

 






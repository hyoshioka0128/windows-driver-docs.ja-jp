---
title: GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX について説明します。
ms.assetid: 34839471-5b3b-4a95-a610-bc35e7774c14
keywords:
- GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX、WDK GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33a21649e20b3b48f9afbf2c14f80f0e09bd3d79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366719"
---
# <a name="guidndisstatusmediaspecificindicationex"></a>GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX

GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX イベント GUID では、メディア固有の状態を示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

ミニポート ドライバーでは、メディア固有の状態を示します、NDIS は、WMI GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX を示す値を WMI クライアントの状態表示を変換します。

ミニポート ドライバーでは、メディア固有の状態インジケーターを行う呼び出すことによって、 [NdisMIndicateStatusEx](https://msdn.microsoft.com/library/windows/hardware/ff563600)関数と、 **StatusCode**のメンバー、 [NDIS_STATUS_INDICATION](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体、 *StatusIndication*パラメーターが指す NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX に設定します。 **StatusBuffer**この構造体のメンバーがで指定されている状態の表示に固有の形式でデータが含まれるドライバーに割り当てられたバッファーを指す**StatusCode**します。

、特定のメディアを示す値の種類に応じて GUID ヘッダーをメディアに固有の表示に固有のデータを後に可能性があります。 この GUID を持つ NDIS を提供するデータ バッファーが含まれています、 [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)存在する場合、メディア固有のデータは後に構造体。


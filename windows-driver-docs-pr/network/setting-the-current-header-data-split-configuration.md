---
title: 現在のヘッダー データの分割構成の設定
description: 現在のヘッダー データの分割構成の設定
ms.assetid: b5b20ce8-1522-4729-8d0a-bc2d2c5afff2
keywords:
- ヘッダー-データ分割 WDK、構成
- 現在のヘッダー-データ分割構成の WDK ネットワーク
- 状態情報 WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3df77ac3693a61a508eae1adfc730c5e7af901ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841934"
---
# <a name="setting-the-current-header-data-split-configuration"></a>現在のヘッダー データの分割構成の設定





NDIS およびそれ以降のドライバーまたはユーザーモードアプリケーションでは、 [oid\_GEN\_HD\_分割\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters) oid を使用して、ミニポートアダプターの現在のヘッダーデータ分割設定を設定します。 ヘッダーデータ分割サービスが提供する NDIS 6.1 およびそれ以降のミニポートドライバーは、この OID をサポートする必要があります。 それ以外の場合、この OID は省略可能です。

システム管理者は、WMI インターフェイスを使用して、この OID に関連付けられている GUID を使用できます。 ヘッダーデータの分割 WMI Guid の詳細については、「 [wmi によるヘッダーデータの分割](wmi-support-for-header-data-split.md)」を参照してください。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_HD\_SPLIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)構造体が含まれています。

NDIS\_HD\_SPLIT\_を\_組み合わせると、NDIS\_HD の**Hdsplit連結 Eflags**メンバー内のすべての\_HEADERS フラグが設定されます。これにより、ミニポートアダプターはすべての分割フレームを結合する必要があります。 ハードウェアでヘッダーデータの分割が有効になっている場合、ドライバーが NDIS にフレームを示す前に、ミニポートドライバーがヘッダーとデータを結合する必要があります。

たとえば、ndis では、OID\_GEN\_HD\_SPLIT\_PARAMETERS OID を使用して、ndis 5 の場合に\_すべての\_ヘッダーフラグを組み合わせる\_を設定することができます。*x*プロトコルドライバーは、NDIS 6.1 ミニポートアダプターにバインドされます。 NDIS は、この OID を処理してからミニポートドライバーに OID を渡し、必要に応じて、ミニポートアダプターの **\*HeaderDataSplit**標準化されたキーワードを更新します。 ヘッダーデータの分割が無効になっている場合、NDIS はこの OID をミニポートアダプターに送信しません。

 

 






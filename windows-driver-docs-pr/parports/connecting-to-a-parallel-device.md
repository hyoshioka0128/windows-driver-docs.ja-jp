---
title: パラレル デバイスへの接続
description: パラレル デバイスへの接続
ms.assetid: c05a1a1e-308a-4b9f-af43-761c4c14d6af
keywords:
- パラレルデバイス WDK、接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef03735a642e8a5ab89617fda48c71316d9bd021
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844801"
---
# <a name="connecting-to-a-parallel-device"></a>パラレル デバイスへの接続





クライアントは、 [**IOCTL\_内部\_parclass\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect)要求を使用して、次を含む[**PARCLASS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information)構造体を取得します。

-   パラレルポートに割り当てられている i/o リソース

-   パラレルポートのハードウェア機能

-   カーネルモードドライバーが並列デバイスの IEEE 1284 動作モードを設定するために使用できるコールバックルーチンへのポインター。「[パラレルデバイスの通信モードの設定とクリア](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)」を参照してください。

-   カーネルモードドライバーが並列デバイスの読み書きに使用できるコールバックルーチンへのポインター。「[並列デバイスの読み取りと書き込み](reading-and-writing-a-parallel-device.md)」を参照してください。

コールバックルーチンは、一般的な関数ドライバーが必要とする機能を提供します。 コールバックルーチンの使用は、同等のデバイス制御要求を使用するよりも効率的です。

クライアントは、 [**IOCTL\_内部\_PARCLASS\_切断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_disconnect)要求を使用して、デバイスから切断します。

 

 





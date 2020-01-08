---
title: ストレージフィルタードライバーの概要
description: 記憶域フィルター ドライバー
ms.assetid: 615e8ff1-d5b2-49da-b024-83bbaff70ded
keywords:
- 記憶域フィルタードライバー WDK
- フィルタードライバーの WDK ストレージ
- 記憶域ドライバー WDK、フィルタードライバー
- SFD WDK storage
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 688786b6f42ba6c23a899ad204bf2ce1940bedda
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606558"
---
# <a name="introduction-to-storage-filter-drivers"></a>ストレージフィルタードライバーの概要

記憶域フィルタードライバーは、システム提供のストレージクラスドライバーでは提供されないデバイス固有の機能をサポートしています。

ここでは、次の情報について説明します。

[ストレージフィルタードライバーによる i/o 要求のサポート](storage-filter-driver-s-support-of-i-o-requests.md)

[ストレージフィルタードライバーのデバイスの種類固有の機能](storage-filter-driver-s-device-type-specific-functionality.md)

[記憶域フィルタードライバーの DriverEntry ルーチン](storage-filter-driver-s-driverentry-routine.md)

[記憶域フィルタードライバーの AddDevice ルーチン](storage-filter-driver-s-adddevice-routine.md)

[ストレージフィルタードライバーでの PnP 開始の処理](handling-pnp-start-in-a-storage-filter-driver.md)

[ストレージフィルタードライバーのディスパッチルーチン](storage-filter-driver-s-dispatch-routines.md)

[ストレージフィルタードライバーの IoCompletion ルーチン](storage-filter-driver-s-iocompletion-routines.md)

[PnP ページング要求の処理](handling-pnp-paging-requests.md)

特定の種類のデバイスに対して記憶域クラスドライバーが既に存在する場合は、同じ種類の新しいデバイス用のドライバーを作成する必要がないことがあります。 システム提供の各ストレージクラスドライバーは、特定の種類の周辺機器をサポートするように設計されており、多数のベンダーデバイスに対してテストされます。 そのため、システムによって提供されるすべてのストレージクラスドライバーは、その種類のニーズに対応する別のデバイスをサポートしている可能性があります。

既存のストレージクラスドライバーが、その種類の新しいデバイスを完全にサポートしていない場合、新しいドライバーは、システムによって提供される既存のクラスドライバーの上または下にあるストレージフィルタードライバー (SFD) として書き込むことができます。 SFD は、読み取り/書き込み要求のデータを変換し、追加の i/o 制御コード (Ioctl) を定義します。これにより、ユーザーアプリケーションは特定のデバイスの追加機能を利用できます。また、デバイス固有の問題を回避するには、汎用クラスまたはポートドライバーにハードウェア固有の変更を必要としません。

新しいデバイスでは、すべての要求をデバイス固有の方法で処理する必要がある場合を除き、ストレージフィルタードライバーは新しいストレージクラスドライバーよりもはるかに短時間で開発できます。

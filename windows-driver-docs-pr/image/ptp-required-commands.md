---
title: PTP 必須コマンド
description: PTP 必須コマンド
ms.assetid: 98f4be09-0f13-45a1-b28a-c027e57c0dd7
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7346805e223bc4f4548e4cfe4ee5e7899079711f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379620"
---
# <a name="ptp-required-commands"></a>PTP 必須コマンド

PTP ドライバーで必須としてマークされているコマンドをサポートする必要があります、*準拠セクション*(14 章) PIMA15740 仕様の。 唯一の例外は、 **GetNumObjects**コマンドは使用されません。

必要な PTP コマンドの完全な一覧です。

0x1001 **GetDeviceInfo**

0x1002 **OpenSession**

0x1003 **CloseSession**

0x1004 **GetStorageIDs**

0x1005 **GetStorageInfo**

0x1007 **GetObjectHandles**

0x1008 **GetObjectInfo**

0x1009 **GetObject**

0x100A **GetThumb**


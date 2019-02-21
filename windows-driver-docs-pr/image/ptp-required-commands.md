---
title: PTP に必要なコマンド
description: PTP に必要なコマンド
ms.assetid: 98f4be09-0f13-45a1-b28a-c027e57c0dd7
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7346805e223bc4f4548e4cfe4ee5e7899079711f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538985"
---
# <a name="ptp-required-commands"></a>PTP に必要なコマンド

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


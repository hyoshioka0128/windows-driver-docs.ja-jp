---
title: アイドル状態の電源管理の前提条件
description: アイドル状態の電源管理の前提条件
ms.assetid: 3c8d8121-9987-43d3-b573-4ca1d26fef7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0a519cdaccb34e5866d8edfe6c51a1246fb2e9d
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606380"
---
# <a name="idle-power-management-assumptions"></a>アイドル状態の電源管理の前提条件

ディスクのスピンアップ操作は、SCSI の開始単位コマンドが LUN に発行されてから240秒 (4 分) 以内に完了します。

次の SCSI コマンド (SRB_FUNCTION_EXECUTE_SCSI 操作) は、ディスクのスピンアップを必要とせずに完了することが想定されています。 つまり、以前の SCSI 開始単位コマンドは必要ありません。

- 照会

- レポート LUN

ミニポートドライバーは、LUN が低電力状態のときに、SRB_FUNCTION_IO_CONTROL、SRB_FUNCTION_FLUSH、および SRB_FUNCTION_SHUTDOWN を除くすべての SRBs を完了することが期待されます。
